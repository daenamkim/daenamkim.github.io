---
layout: post
comments: true
title: "Shell Script로 실행 결과를 시간과 함께 저장하기"
date: 2017-02-22 03:36:51
image: '/assets/img/'
description: 'Shell Script 로 간단한 반복 테스트 로직 사용 시 시간과 함께 실행 로그를 기록 해보자.'
main-class: 'misc'
color:
tags:
- misc
- shellscript
categories:
twitter_text: 'Shell Script로 실행 결과를 시간과 함께 저장하기'
introduction: 'Shell Script 로 간단한 반복 테스트 로직 사용 시 시간과 함께 실행 로그를 기록 해보자.'
---

## 작성 및 실행

개발을 하다보면 가끔 같은 동작의 실행을 스크립트로 작성 후 실행 결과를 나중에 확인 할 필요가 있다.
이 때, 실행된 시간까지 같이 기록하면 좋겠다는 생각에 내용을 정리해 보았다.

예제로 git pull 을 주기적으로 실행 하도록 해보겠다.

우선 **update.sh**를 작성한다.
{% highlight shell %}
$ vi update.sh
{% endhighlight %}

아래와 같이 주기적으로 실행할 코드를 작성한다.
주의 할 점은 가능한 절대 경로를 지정하자.
실제로 발생하는 많은 오류의 경우가 경로 및 실행 권한이다.

{% highlight shell %}
#!/bin/sh

echo_timestamp() {
    echo "["`date "+%m-%d-%Y %H:%M:%S %z %Z"`"]" $*
}

echo_timestamp `/usr/bin/git pull` >> /home/dev/update.log
{% endhighlight %}

작성 후 저장하는 것은 필수이다.

{% highlight shell %}
:wq
{% endhighlight %}

**sh** 명령어와 함께 쓰지 않기 위해서 실행 권한도 부여한다.

{% highlight shell %}
$ chmod 775 update.sh
$ ls -al
drwxrwxr-x 4 dev dev 4096 Feb 22 12:58 .
drwxr-xr-x 3 dev dev 4096 Feb 13 00:43 ..
...
-rwxrwxr-x 1 dev dev  262 Feb 22 12:26 update.sh
...
{% endhighlight %}

이제 **crontab**을 수정하자.

{% highlight shell %}
$ crontab -e
{% endhighlight %}

맨 아래 부분에 실행 주기와 실행할 스크립트를 추가한다.
설정 내용은 매 1분 마다 실행하도록 하였다.
{% highlight shell %}
# m h  dom mon dow   command
*/1 * * * * cd /home/dev/repo/; ./update.sh >/dev/null 2>&1
{% endhighlight %}

저장하고 나가면 **crontab**이 가동된다.

{% highlight shell %}
:wq
{% endhighlight %}

{% highlight shell %}
$ crontab -e
crontab: installing new crontab
{% endhighlight %}

실행 결과가 매 1분 마다 기록되는 것을 확인할 수 있다.

{% highlight shell %}
$ tail -n 5 /home/dev/update.log 
[02-22-2017 12:54:09 +0900 JST] Already up-to-date.
[02-22-2017 12:55:09 +0900 JST] Already up-to-date.
[02-22-2017 12:56:08 +0900 JST] Already up-to-date.
[02-22-2017 12:57:09 +0900 JST] Already up-to-date.
[02-22-2017 12:58:08 +0900 JST] Updating 60b1ff9..ecaa7bf Fast-forward README.md | 3 +++ 1 file changed, 3 insertions(+)
{% endhighlight%}

특별히 검토하지 않고 지속적으로 병합 해도 문제 없는 소스의 경우에는 활용하면 좋을 것 같다.
GitHub에서 많은 소스를 fork해서 로컬에 clone했을 경우 지속적인 최신 소소의 fetch를 예로 들 수 있겠다.


## 참고
- [Prefixing logs with date in shell script](http://stackoverflow.com/questions/1705743/prefixing-logs-with-date-in-shell-script)
