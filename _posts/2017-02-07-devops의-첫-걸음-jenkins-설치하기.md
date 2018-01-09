---
layout: post
title: "DevOps의 첫 걸음 Jenkins 설치하기"
date: 2017-02-07 06:47:54
image: '/assets/img/'
description: 'Jenkins 설치가 얼마나 간단한지 알아보자.'
main-class: 'devops'
color:
tags:
- devops
- jenkins
categories:
- "Challenging DevOps."
twitter_text: 'DevOps의 첫 걸음 Jenkins 설치하기'
introduction: 'Jenkins 설치가 얼마나 간단한지 알아보자.'
---

## 설치 환경
- Ubuntu 16.04.1 LTS
- Jenkins 2.32.2

## 설치 시작
- apt에 필요한 키와 소스 리스트를 등록 후 바로 설치까지 진행하면 된다.

{% highlight shell %}
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
$ sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
$ sudo apt-get update
$ sudo apt-get install jenkins
{% endhighlight %}

나만 그랬었는지 모르겠으나 JST 기준으로 2017년 2월 6일까지 설치 시도 시 아래와 같은 오류가 났었으며 구글링을 해도 별다른 해답을 찾지 못했는데 2017년 2월 7일에 다시 시도 해보니 설치가 정상적으로 되었다.

{% highlight shell %}
Failed to fetch http://archives.jenkins-ci.org/debian-stable/jenkins_2.32.2_all.deb
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
{% endhighlight %}

지금은 발생하지 않으니 그냥 넘어간다. ㅎㅎ

- 브라우저로 Jenkins에 접속한다.

정상적으로 설치를 하고 나서 Jenkins Wiki에는 이것저것 여러가지가 씌여 있으나 그냥 IP:8080로 접속하면 된다.
현재 작업용 서버인 192.168.7.5:8080으로 접속하면 다음과 같이 Unlock Jenkins 화면이 나온다.
![Unlock Jenkins](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/unlock-jenkins-1.png)
갑자기 위와 같은 화면이 나와서 잠깐 긴장했으나 **/var/lib/jenkins/secrets/initialAdminPassword** 파일에 Administrator password가 있다. 반드시 sudo를 사용해서 조회해야 한다. 그렇지 않으면 Permission denied가 발생한다.

{% highlight shell %}
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
25aeeb0c894b4fba8a5ad7180c92ec8a
{% endhighlight %}

Administrator password를 넣고 **Continue**를 클릭한다.
![Unlock Jenkins](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/unlock-jenkins-2.png)

여기서는 아무 생각 없이 그냥 **Installed suggested plugins**를 눌렀는데 알아서 필요한 것을 잘 설치해 주리라 믿는다.
![Customize Jenkins](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/customize-jenkins.png)

어디보자... 역시 가장 많이 사용하는 플러그인들이 설치 된다. 모르는 것들도 몇 개 있네.
![Install Plugins](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/install-plugins.png)

사용자를 추가하는 화면인데 사용자 정보를 입력 후 **Save and Finish**를 클릭한다. 여기서 입력 하기가 극도로 귀찮은 사람은 Continue as admin을 클릭해서 넘어가도 된다.
나중에 로그인 아웃 후 다시 로그인 시에는 Unlock 시 사용한 Administrator password를 사용하면 된다.
![Create User](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/create-user.png)

자! 끝났다. **Start using Jekings**를 클릭하면 대시보드가 표시된다.
![Jenkins Is Ready](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/jenkins-is-ready.png)
![Jenkins Dashboard](http://cdn.oootoko.net/blog/assets/img/devops의-첫-걸음-jenkins-설치하기/jenkins-dashboard.png)

## 다음 할 일
- GitHub와 연동하여 Test, Pull Request, Merge, Deploy 테스트.

## 참고
- [Installing Jenkins on Ubuntu](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)