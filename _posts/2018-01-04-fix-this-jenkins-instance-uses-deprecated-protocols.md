---
layout: post
comments: true
title: "Fix \"This Jenkins instance uses deprecated protocols\""
date: 2018-01-04 09:58:31
image: '/assets/img/'
description: 'Jenkins 업데이트 후에 발생하는 프로토콜 경고 없애기.'
main-class: 'misc'
color:
tags:
- misc
- jenkins
categories:
twitter_text: 'Jenkins 업데이트 후에 발생하는 프로토콜 경고 없애기.'
introduction: 'Jenkins 업데이트 후에 발생하는 프로토콜 경고 없애기.'
---

기억 하기로는 Jenkins를 2.89로 업데이트 후에 프로토콜 관련 경고가 표시되기 시작했다. 사실 이미 [Jenkins Blog](https://jenkins.io/blog/2017/08/11/remoting-update/)에서는 2017년 8월에 삭제 안내가 올라와 있었다. 하여튼, 이 경고를 없애보자. 아주 단순한 것을 삽질한 바람에 몇 자 적어본다.

## 해결 과정

#### 경고 클릭
![Security Alert](http://cdn.oootoko.net/blog/assets/img/fix-this-jenkins-instance-uses-deprecated-protocols/security-alert.png)

#### 프로토콜 상세 확인
![Security Alert](http://cdn.oootoko.net/blog/assets/img/fix-this-jenkins-instance-uses-deprecated-protocols/agent-protocols.png)

![Security Alert](http://cdn.oootoko.net/blog/assets/img/fix-this-jenkins-instance-uses-deprecated-protocols/agent-protocols-before.png)

#### 구 프로토콜의 사용 해제
![Security Alert](http://cdn.oootoko.net/blog/assets/img/fix-this-jenkins-instance-uses-deprecated-protocols/agent-protocols-after.png)
저장하면 경고가 사라진다! >.<

## 참고
- [Remoting Update. Protocols deprecation, Java 8 requirement and plans](https://jenkins.io/blog/2017/08/11/remoting-update/)
- [Jenkins の警告 (古いプロトコル) が出ないようにする方法](https://m-tmatma.github.io/Jenkins/jenkins-deprecated-protocol.html)
