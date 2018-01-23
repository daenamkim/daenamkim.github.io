---
layout: post
comments: true
title: "설치형 Wordpress에서 테마 및 파일 업로드 오류 해결하기"
date: 2017-02-10 08:02:50
image: '/assets/img/'
description: '설치형 Wordpress를 사용 시 가장 많이 겪는 파일 용량 문제 해결 방법을 알아보자.'
main-class: 'misc'
color:
tags:
- misc
- wordpress
categories:
twitter_text: '설치형 Wordpress에서 테마 및 파일 업로드 오류 해결하기'
introduction: '설치형 Wordpress를 사용 시 가장 많이 겪는 파일 용량 문제 해결 방법을 알아보자.'
---

## 테마 업로드 경로
- 외모 > 테마 > 새로추가 > 테마 업로드 > zip 파일 업로드 > 지금 설치하기
![Install Theme](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/install-theme-1.png)
![Install Theme](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/install-theme-2.png)

**지금 설치하기**를 클릭하면 당연히 될 줄 알았으나 (깨끗한 서버에서 시작했을 경우 보통은) 아래와 같은 오류가 발생한다.
![Install Theme Error](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/install-theme-error-1.png)

자! 이제부터 손을 좀 봐주자.

## php.ini 수정
작업하기 전에 php 모듈이 어떤 설정 파일을 참조하고 있는지 꼭 확인하자.
엉뚱한 파일을 수정하게 되면 당연히 설정이 반영되지 않으므로 주의하자.
확인 방법은 아주 간단하다. 웹 루트 디렉토리의 index.php를 만들고 phpinfo()를 아래와 같이 작성한 후 해당 도메인으로 접속하면된다.

{% highlight php %}
<?php
phpinfo();
{% endhighlight %}

참고로 코드 전체가 php로만 작성될 경우 마지막에 **?>**는 넣지 않아도 된다.
혹시 여러가지 vhost 설정으로 설정 수정이 번거러울 경우에는 다음과 같이 shell 에서 직접 확인 가능하다.
{% highlight shell %}
$ echo "<?php phpinfo();" > test.php
$ php test.php | grep Configuration
Configuration File (php.ini) Path => /etc/php5/cli
Loaded Configuration File => /etc/php5/cli/php.ini
Configuration
{% endhighlight %}

위치를 확인 했으니 설정을 수정하자.
{% highlight shell %}
$ sudo vi /etc/php5/cli/php.ini
{% endhighlight %}

아래와 같이 수정하자.
{% highlight ini %}
post_max_size = 1024M
upload_max_filesize = 1024M
{% endhighlight %}

설정을 저장하고 나서 웹 서버를 재기동하고 반영까지 잘 되어 있는지 꼭 확인하자.
잘 되었군.
{% highlight shell %}
$ sudo service apache2 restart
$ php test.php | grep _max
log_errors_max_len => 1024 => 1024
post_max_size => 1024M => 1024M
upload_max_filesize => 1024M => 1024M
session.gc_maxlifetime => 1440 => 1440
{% endhighlight %}

보통은 이렇게 해결 했는데 이번에는 해결되지 않았다. ;;

## .htaccess 수정
Wordpress가 설치된 루트 디렉토리 내부의 .htaccess를 수정 해주자. (디렉토리의 소유자가 다를 경우 sudo를 같이 사용하자.)
{% highlight shell %}
$ sudo vi .htaccess
{% endhighlight %}

가장 아래 줄에 다음과 같이 설정을 추가한다. 덤으로 실행 시간까지 충분히 늘려주자.
{% highlight shell %}
php_value upload_max_filesize 1024M
php_value post_max_size 1024M
php_value max_execution_time 300
php_value max_input_time 300
{% endhighlight %}

다시 웹 서버를 재기동 하였으나 여전히 해결되지 않았다. 조금 더 조사해본 결과...
**LimitRequestBody**라는 항목도 바꿔줄 필요가 있다는 것을 알았다.
다음과 같이 수정하자.
{% highlight shell %}
LimitRequestBody 1024000000
{% endhighlight %}

다시 웹 서버를 재기동하고 업로드를 시도하니 성공! 그러나...
![Install Theme Error](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/install-theme-error-2.png)

이것도 조사를 해보니 테마를 구입 후에 바로 받아서 업로드 시 사용하면 안되고 한 번 압축을 풀어서 안에 있는 실제 테마 파일만 올려야 한다.
![Theme File](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/theme-file.png)

테마 파일로 다시 업로드 하니 이번에는 성공!
![Install Theme Success](http://cdn.oootoko.net/blog/assets/img/wordpress에서-테마-및-파일-업로드-오류-해결하기/install-theme-success.png)


## 호스팅 업체에 문의
위에 있는 모든 설정을 했는데도 안된다면 호스팅 업체에 연락해서 문의하자. ;;

## 참고
- [PHP Increase Upload File Size Limit](https://www.cyberciti.biz/faq/linux-unix-apache-increase-php-upload-limit/)
- [LimitRequestBody](https://www.cyberciti.biz/faq/apache-limiting-upload-size/)
- [[워드프레스] 유료 테마/플러그인을 설치하는 방법](http://www.thewordcracker.com/basic/how-to-install-premium-wordpress-themes-and-plugins/)