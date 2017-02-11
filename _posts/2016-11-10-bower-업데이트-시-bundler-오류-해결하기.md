---
layout: post
title: "Bower 업데이트 bundler 오류 해결하기"
date: 2016-11-10 13:26:48
image: '/assets/img/'
description:
main-class: 'js'
color:
tags:
- js
- angularjs
- bower
categories:
twitter_text:
introduction:
---

AngularJS로 개발을 하다보면 자주 Bower 업데이트를 자주 실행하게된다.
업데이트 작업 시 bundler가 없다는 오류가 발생하였다. 내가 뭔가 이상한 짓을 한 것 같다. ;;

Mac에서 개발중인 나는 bundler를 다시 설치 하기 위해서 별 생각 없이 다음과 같이 실행 하였다.
{% highlight shell %}
$ sudo gem install bundler
{% endhighlight %}
위와 같이 실행 했을 경우 /usr/bin/에 설치가 되는데 sudo로 실행했음에도 불구하고 퍼미션 오류가 발생한다. macOS Sierra 로 업데이트 하고 나서 뭔가 보안 정책이 많이 바뀐 것 같다.


{% highlight shell %}
sudo gem install bundler -n /usr/local/bin/
{% endhighlight %}
 
rbenv 를 설치할 경우 현재 쉘 유저를 그대로 사용하기 때문에 sudo 없이 그냥
gem install bundler 를 하면 됨.
