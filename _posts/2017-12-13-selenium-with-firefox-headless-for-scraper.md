---
layout: post
comments: true
title: "Selenium with Firefox Headless for Scraper"
date: 2017-12-13 01:34:14
image: '/assets/img/'
description: 'Selenium과 Firefox Headless로 Web Scraper 시작하기.'
main-class: 'data'
color:
tags:
- data
- selenium
- firefox
- scraper
- python
twitter_text: 'Selenium과 Firefox Headless로 Web Scraper 시작하기.'
introduction: 'Selenium과 Firefox Headless로 Web Scraper 시작하기.'
---

## 도입 배경
Web Scraping을 [urllib](https://docs.python.org/3/library/urllib.html)이나 [Requests](http://docs.python-requests.org/en/master/)를 사용할 경우 상대적으로 빠른 이점이 있으나 동적으로 로딩되는 템플릿 데이터를 정상적으로 취득하지 못하는 경우가 발생한다. 이 때, 가상 브라우저를 사용하면 문제를 해결 할 수 있으며 (반면에 메모리 사용량 증가 및 속도가 느려지는 단점이 있다.) 대표적인 가상 브라우저 도구인 [Selenium](http://www.seleniumhq.org/)을 적용해 보도록 하자.

![Selenium Logo](https://cdn.oootoko.net/blog/assets/img/selenium-with-firefox-headless-for-scraper/selenium-logo.png)

Selenium을 사용해서 [Headless Browser](https://en.wikipedia.org/wiki/Headless_browser)로 웹 화면을 읽어오기 위해서는 외부 Web Driver를 연동해야 하는데 내장되어 있지 않으므로 별도로 설치를 해주어야 한다. 대표적인 Web Driver는 다음과 같다.
- Firefox + [Gecko Driver](https://github.com/mozilla/geckodriver/releases)
- [Chrome Driver](https://sites.google.com/a/chromium.org/chromedriver/downloads)
- [PhantomJS](http://phantomjs.org/download.html)

현재 몸담고 있는 회사에서 운영 중인 솔루션에서 이미 Chrome Driver를 사용하고 있었으나 원인 불명으로 계속해서 오류가 발생했다. 말 그대로 원인 불명이다. >.<

{% highlight shell %}
Message: unknown error: Chrome failed to start: crashed
  (Driver info: chromedriver=2.34.522913 (36222509aa6e819815938cbf2709b4849735537c),platform=Linux 3.13.0-24-generic x86_64)
{% endhighlight %}

여기서 일일이 열거하지는 않겠지만 서버를 새로 구축 하는 것 빼고는 다 해본 것 같다. Chrome Driver는 드라이버만 설치하면 되기 때문에 간단해서 좋았는데 이렇게 되어 버렸으니 Firefox + Gecko Driver로 교체해 보기로 하였다. 결론부터 말하면 교체 후에 **문제가 해결** 되었다.

Firefox + Gecko Driver를 사용하면 몇 가지 작업을 더 해주어야 하는데 모두 정리하면 다음과 같다. (Firefox를 이용한 여러가지 케이스를 시도해본 결과 이 방법이 문제없이 완벽하게 동작했다.)
- Gecko Driver 설치.
- Firefox 설치.
- [Xvfb](https://en.wikipedia.org/wiki/Xvfb) 설치 및 백그라운드 실행.
- Selenium 설치.

## Gecko Driver 설치
[Mozila](https://www.mozilla.org/ko/)가 GitHub에 공개해 놓은 파일을 내려 받아서 이동 시키기만 하면 된다.
{% highlight shell %}
$ wget https://github.com/mozilla/geckodriver/releases/download/v0.19.1/geckodriver-v0.19.1-linux64.tar.gz
$ tar -zxvf geckodriver-v0.19.1-linux64.tar.gz
$ sudo cp ./geckodriver /usr/local/bin
$ geckodriver --version
geckodriver 0.19.1

The source code of this program is available from
testing/geckodriver in https://hg.mozilla.org/mozilla-central.

This program is subject to the terms of the Mozilla Public License 2.0.
You can obtain a copy of the license at https://mozilla.org/MPL/2.0/.
{% endhighlight %}

## Firefox와 Xvfb 설치 (Ubuntu 기준)
Firefox [PPA](https://help.ubuntu.com/community/PPA)를 등록 후 Firefox와 Xvfb를 설치한다.
{% highlight shell %}
$ sudo echo -ne \'\n\' | apt-add-repository ppa:mozillateam/firefox-next
$ sudo apt-get update
$ sudo apt-get install -y firefox xvfb
$ firefox --version
Mozilla Firefox 58.0
{% endhighlight %}

Xvfb를 백그라운드로 실행하고 `DISPLAY` 환경 변수도 지정 해준다. `DISPLAY` 환경 변수는 Firefox가 실행 될 때 데이터를 출력할 화면의 번호를 의미한다. `:10`은 Firefox와 Xvfb를 연결할 화면 번호인데 반드시 같은 값으로 지정해 주어야 한다. 
{% highlight shell %}
$ export DISPLAY=:10
$ Xvfb :10 -ac &
[2] 13196
[1]   Done                    Xvfb :10 -ac
dev@lmtest01:~/lm_backend$ Initializing built-in extension Generic Event Extension
Initializing built-in extension SHAPE
Initializing built-in extension MIT-SHM
Initializing built-in extension XInputExtension
Initializing built-in extension XTEST
Initializing built-in extension BIG-REQUESTS
Initializing built-in extension SYNC
Initializing built-in extension XKEYBOARD
Initializing built-in extension XC-MISC
Initializing built-in extension SECURITY
Initializing built-in extension XINERAMA
Initializing built-in extension XFIXES
Initializing built-in extension RENDER
Initializing built-in extension RANDR
Initializing built-in extension COMPOSITE
Initializing built-in extension DAMAGE
Initializing built-in extension MIT-SCREEN-SAVER
Initializing built-in extension DOUBLE-BUFFER
...
{% endhighlight %}

`DISPLAY` 번호(:1)가 Xvfb 설정(:10)과 다를 경우 다음과 같은 오류가 발생한다.
{% highlight shell %}
$ firefox
Error: cannot open display: :1
{% endhighlight %}

정리하면 다음과 같다.
>*Firefox 실행 → 10번 화면 오픈 → 10번 화면 Frame Buffer (Xvfb)*

## Selenium 설치
Python 패키지 매니저인 [pip](https://ko.wikipedia.org/wiki/Pip_(%ED%8C%A8%ED%82%A4%EC%A7%80_%EA%B4%80%EB%A6%AC%EC%9E%90))을 이용해서 Selenium과 Web Scraping 시에 [Parser](https://ko.wikipedia.org/wiki/%EA%B5%AC%EB%AC%B8_%EB%B6%84%EC%84%9D)로 아주 유명한 [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/)도 같이 설치한다.
{% highlight shell %}
$ pip install selenium beautifulsoup4
{% endhighlight %}

본인의 경우 [pyenv](https://github.com/pyenv/pyenv)와 [virtualenv](https://github.com/pyenv/pyenv-virtualenv)를 사용해서 Python 기본 개발 환경을 구축했는데 장점은 다음과 같다.

- 사용하는 시스템에 따라 패키지의 의존성 문제나 충돌 문제가 사라짐.
- 다양한 버전의 패키지를 간단히 설치 및 삭제할 수 있다.
- 한 버전에 대해서 또 다른 가상 버전을 간단히 추가 및 삭제 할 수 있다.
- 특정 작업 디렉토리에 특정 버전 또는 가상 버전의 패키지를 연결 할 수 있다. (예: A 디렉토리는 Python 3.5, B 디렉토리는 anaconda 5.0.0)

시간이 된다면 **정신 건강**을 위해서라도 꼭 사용하길 권장한다.

## Selenium 동작 확인
이제 Selenium을 사용할 준비가 되었으니 동작을 확인할 테스트 코드를 작성하자. 위 과정을 진행하면서 문제가 없었다면 Python 코드 내에서 Firefox binary나 geckodriver 파일 위치를 수동으로 지정하지 않아도 된다. (수동으로 지정이 필요할 경우 [여기](https://stackoverflow.com/questions/40208051/selenium-using-python-geckodriver-executable-needs-to-be-in-path)를 참고하자.)
{% highlight python %}
# -*- coding: utf_8 -*-

from bs4 import BeautifulSoup
from selenium import webdriver

driver = webdriver.Firefox()
driver.get('http://oootoko.net')
soup = BeautifulSoup(driver.page_source, 'html.parser')
print('===============================================')
print(soup.find('title'))
print('===============================================')
driver.quit()
{% endhighlight %}

테스트 코드를 실행하면 다음과 같은 결과가 표시된다.
{% highlight shell %}
$ python test_selenium.py 
===============================================
<title>OOOTOKO</title>
===============================================
{% endhighlight %}

잘 동작한다!

Xvfb가 실행 중이 아닐 경우 다음과 같은 오류가 발생하므로 서버 배포 시에는 백그라운드에서 잘 실행될 수 있도록 하는 것과 기동 상태 감시 추가를 잊지 않도록 하자.
{% highlight shell %}
Traceback (most recent call last):
  File "test_selenium.py", line 13, in <module>
    driver = webdriver.Firefox()
  File "/home/dev/.pyenv/versions/3.5.2/lib/python3.5/site-packages/selenium/webdriver/firefox/webdriver.py", line 152, in __init__
    keep_alive=True)
  File "/home/dev/.pyenv/versions/3.5.2/lib/python3.5/site-packages/selenium/webdriver/remote/webdriver.py", line 98, in __init__
    self.start_session(desired_capabilities, browser_profile)
  File "/home/dev/.pyenv/versions/3.5.2/lib/python3.5/site-packages/selenium/webdriver/remote/webdriver.py", line 188, in start_session
    response = self.execute(Command.NEW_SESSION, parameters)
  File "/home/dev/.pyenv/versions/3.5.2/lib/python3.5/site-packages/selenium/webdriver/remote/webdriver.py", line 256, in execute
    self.error_handler.check_response(response)
  File "/home/dev/.pyenv/versions/3.5.2/lib/python3.5/site-packages/selenium/webdriver/remote/errorhandler.py", line 194, in check_response
    raise exception_class(message, screen, stacktrace)
selenium.common.exceptions.WebDriverException: Message: Process unexpectedly closed with status: 1
{% endhighlight %}

## 참고
- [Running Selenium WebDriver tests using Firefox headless mode on Ubuntu](https://medium.com/@griggheo/running-selenium-webdriver-tests-using-firefox-headless-mode-on-ubuntu-d32500bb6af2)
- [Selenium using Python - Geckodriver executable needs to be in PATH
](https://stackoverflow.com/questions/40208051/selenium-using-python-geckodriver-executable-needs-to-be-in-path)
