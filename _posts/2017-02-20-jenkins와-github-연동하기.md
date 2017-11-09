---
layout: post
title: "Jenkins와 GitHub 연동하기"
date: 2017-02-20 14:11:37
image: '/assets/img/'
description: 'Jenkins와 GitHub를 연동하여 빌드 자동화를 구축 해보자.'
main-class: 'devops'
color:
tags:
- devops
- jenkins
- github
categories:
twitter_text: 'Jenkins와 GitHub 연동하기'
introduction: 'Jenkins와 GitHub를 연동하여 빌드 자동화를 구축 해보자.'
---

## SSH 공개 키 생성 및 GitHub에 등록
Jenkins와의 연동을 위해서 비번은 넣지 않도록 한다.

```
$ ssh-keygen -t rsa -C "office@ascentnet.co.jp"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/dev/.ssh/id_rsa): 
Created directory '/home/dev/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/dev/.ssh/id_rsa.
Your public key has been saved in /home/dev/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:T3k+FRRIDaMx3whqaYYH0wu8C0QQb1ZzQLn9l+f7VZE office@ascentnet.co.jp
The key's randomart image is:
+---[RSA 2048]----+
|  o+.oB+. +.++o. |
|   ...+*.o *.=. .|
|   .+ .=B.. o oE |
|   o. o=o  .   ..|
|     . .S.o ... .|
|      .  o.oo.. .|
|          ..oo  .|
|             .. .|
|              .o.|
+----[SHA256]-----+

$ ls -al .ssh/
total 16
drwx------ 2 dev dev 4096 Feb 20 22:49 .
drwxr-xr-x 4 dev dev 4096 Feb 20 22:47 ..
-rw------- 1 dev dev 1675 Feb 20 22:49 id_rsa
-rw-r--r-- 1 dev dev  404 Feb 20 22:49 id_rsa.pub
```


id_rsa가 비밀 키이고, id_rsa.pub이 공개 키 이다.


```
$ cat ~/.ssh/id_rsa.pub 
ssh-rsa AAAAB3Nza ... ICzbcz1T4JXMPLV9ksjIS/neDtXcID office@ascentnet.co.jp
$ chmod 400 .ssh/id_rsa
```

공개 키를 취득한 후에 Key 입력 부분에 저장한다.

Add SSH key를 클릭하여 추가한다.

이후에 실제로 동작하는지 확인하자.

```
$ ssh -T git@github.com
The authenticity of host 'github.com (192.30.253.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8. <= Finger Print
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
Hi ascentadmin! You've successfully authenticated, but GitHub does not provide shell access.
```

생성한 SSH Key를 jenkins 유저 디렉토리 밑에 복사한다.
```
$ cd
$ sudo cp .ssh /var/lib/jenkins/
$ cd /var/lib/jenkins
$ sudo chown -R jenkins:jenkins .ssh
```

정상적으로 접속됨을 확인 하였다.


## 참고
- [소셜 코딩으로 이끄는 GitHub 실천 기술](http://jpub.tistory.com/467)