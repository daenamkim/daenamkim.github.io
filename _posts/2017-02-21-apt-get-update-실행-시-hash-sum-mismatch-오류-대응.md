---
layout: post
comments: true
title: "apt-get update 실행 시 Hash Sum mismatch 오류 대응"
date: 2017-02-21 01:52:17
image: '/assets/img/'
description: 'apt-get update 실행 시 Hash Sum mismatch 오류 발생 시 초간단 해결 방법을 알아보자.'
main-class: 'misc'
color:
tags:
- misc
- ubuntu
categories:
twitter_text: 'apt-get update 실행 시 Hash Sum mismatch 오류 대응'
introduction: 'apt-get update 실행 시 Hash Sum mismatch 오류 발생 시 초간단 해결 방법을 알아보자.'
---

## 오류 내용
`Ubuntu 14.04.5 LTS` 서버에서 패키지 정보를 업데이를 하던 중 아래와 같은 오류가 발생하였다.

{% highlight shell %}
$ sudo apt-get update
...
Hit http://security.ubuntu.com trusty-security/restricted Translation-en       
Hit http://security.ubuntu.com trusty-security/universe Translation-en         
Fetched 2,727 kB in 10s (251 kB/s)                                             
W: Failed to fetch http://jp.archive.ubuntu.com/ubuntu/dists/trusty-updates/main/binary-amd64/Packages  Hash Sum mismatch

W: Failed to fetch http://jp.archive.ubuntu.com/ubuntu/dists/trusty-updates/universe/binary-amd64/Packages  Hash Sum mismatch

W: Failed to fetch http://jp.archive.ubuntu.com/ubuntu/dists/trusty-updates/main/binary-i386/Packages  Hash Sum mismatch

W: Failed to fetch http://jp.archive.ubuntu.com/ubuntu/dists/trusty-updates/universe/binary-i386/Packages  Hash Sum mismatch

E: Some index files failed to download. They have been ignored, or old ones used instead.
{% endhighlight %}

## 조사 및 해결
갑자기 발생한 원인을 알 수 없어서 구글링을 하였다. 해결 방법은 두 가지가 있었는데 가장 간단한 방법으로 진행하기로 하였다.
기존에 저장되어 있는 리스트 정보를 싹 지워 준 후에 다시 업데이트를 진행 하였다.

{% highlight shell %}
$ sudo rm -rf /var/lib/apt/lists/*
$ sudo apt-get update
Ign http://jp.archive.ubuntu.com trusty InRelease                              
Get:1 http://jp.archive.ubuntu.com trusty-updates InRelease [65.9 kB]          
Get:2 http://jp.archive.ubuntu.com trusty-backports InRelease [65.9 kB]        
Get:3 http://jp.archive.ubuntu.com trusty Release.gpg [933 B]                  
Get:4 http://jp.archive.ubuntu.com trusty Release [58.5 kB] 
...
Get:71 http://security.ubuntu.com trusty-security/multiverse Translation-en [2,201 B]
Get:72 http://security.ubuntu.com trusty-security/restricted Translation-en [3,357 B]
Get:73 http://security.ubuntu.com trusty-security/universe Translation-en [89.3 kB]
Fetched 33.9 MB in 20s (1,633 kB/s)                                            
Reading package lists... Done
{% endhighlight %}
문제 없이 업데이트 되었다!

## 참고
- [Hash Sum mismatch エラー](http://qiita.com/TsutomuNakamura/items/93e4a4ea0e587160fcaf)