---
layout: post
comments: true
title: "Import a custom certificate on AWS Certificate Manager"
date: 2018-05-24 05:10:16
image: '/assets/img/'
description: 'AWS Certificate Manager에서 Custom Certificate를 등록하는 방법을 알아보자.'
main-class: 'dev'
color:
tags:
- dev
- aws
- ssl
categories:
twitter_text: 'AWS Certificate Manager에서 Custom Certificate를 등록하는 방법을 알아보자.'
introduction: 'AWS Certificate Manager에서 Custom Certificate를 등록하는 방법을 알아보자.'
---

## SSL Certificate 구입

SSL Certificate을 발행하는 방법은 여러가지가 있으며 클라우드 서비스나 서비스 형태에 따라서 무료로 제공하는 경우도 있다. 혹시 GitHub에서 개인 블로그를 운영 한다면 최근에 [GitHub Pages에서 SSL을 무료로 제공](https://blog.github.com/2018-05-01-github-pages-custom-domains-https/)하기 시작했으므로 참고하자.

증명서 발행 방법은 다음과 같다.

1. [Self-Signed Certificate](https://en.wikipedia.org/wiki/Self-signed_certificate): 돈이 정말 없거나 증명서 발행에 도저히 돈을 쓸 가치가 없다는 사람만 할 것. (최신 브라우저에서는 기본 차단됨.)
2. 온라인 발행 서비스에서 구입([여기서](https://www.ssl2buy.com/wildcard-ssl-certificate) 상당히 싼 증명서를 찾았음.)
3. SSL Certificate on Cloud(e.g. [ACM](https://aws.amazon.com/certificate-manager/?nc1=h_ls)): 클라우드 내에서 발생하는 기능으로 클라우드 내에서 모든 서비스의 구성, 도메인 및 증명서 관리를 한다면 상당히 편리할 수 있다.

나는 **2번**으로 진행했다. 앞으로 서브 도메인을 붙여서 AWS외에도 여러가지로 가지고 놀 생각으로 저렴한 [Wildcard Certificate](https://en.wikipedia.org/wiki/Wildcard_certificate)을 구입하길 원했기 때문이다.

[Certificate 종류](https://www.globalsign.com/en/ssl-information-center/types-of-ssl-certificate/)는 인증 레벨, 인증 범위, 발행 기관에 따라 가격이 천차 만별이므로 목적과 예산에 맞게 잘 정하도록 하자. 그리고 증명서를 구입했다고 끝나는 것이 아니라 발행 요청 철차(제공 서비스 마다 다를 수 있음)을 통해서 최종 증명서 데이터(암호화된 문자열)를 취득해야 한다.


## Certificate 발행

증명서를 구입한 곳에서 안내하는 순서대로 진행하면 최종 증명서 파일(암호화된 문자열)을 취득 할 수 있으며 이 때 **발행 과정 중에 최종 인증을 위해서는 CSR에 입력한 도메인을 반드시 실 소유하고 있어야 한다.**

### CSR 작성

[CSR](https://en.wikipedia.org/wiki/Certificate_signing_request)은 `openssl` 명령을 이용해서 [생성](https://support.globalsign.com/customer/portal/articles/1221018-generate-csr---openssl)한다.

{% highlight shell %}
$ openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privatekey.key
Generating a 2048 bit RSA private key
.........+++
....................................................................+++
writing new private key to 'privatekey.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:JP
State or Province Name (full name) []:Tokyo
Locality Name (eg, city) []:**********
Organization Name (eg, company) []:OOOTOKO
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:*.oootoko.net
Email Address []:daenam.kim@*****.***
{% endhighlight %}

`CSR.csr`에 있는 내용은 Certificate 발행 시 필요하며 `privatekey.key` 는 향후 웹 서버 설정이나 AWS에 등록할 때 필요하다.

### Certificate과 Private Key를 PEM 형태로 변경

AWS Certificate Manager에 Import 시에는 PEM 형태로 인코딩된 정보를 넣어야 한다. [다음과 같이](https://stackoverflow.com/questions/991758/how-to-get-pem-file-from-key-and-crt-files) 실행한다.

{% highlight shell %}
$ openssl rsa -in privatekey.key -text > privatekey.pem
$ openssl x509 -inform PEM -in server.crt > server.pem
{% endhighlight %}

내가 직접 실행 했을 때에는 `server.pem`의 경우 출력 데이터가 변하지 `server.crt`와 다르지 않았다.

### Chain 설정을 위한 Intermediate Certificate 취득

[Intermediate Certificate](https://en.wikipedia.org/wiki/Public_key_certificate#Types_of_certificate)는 보통 증명서를 구입한 곳에서 공개적으로 제공하고 있으므로 잘 찾아서 받아 놓자. 어떻게 생겼는지 궁금하면 [확인](https://www.alphassl.com/support/install-root-certificate.html)하자.

## Imoport Certificate on AWS

최종 준비물은 다음과 같다.

- [AWS Console](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&forceMobileApp=0) 계정.
- Private Key PEM Encoded.
- Certificate.
- Intermediate Certificate.

AWS Console에 로그인 한 후에 다음의 순서대로 진행한다.

![Import Image Step 0](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-0.png)

![Import Image Step 1](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-1.png)

![Import Image Step 2](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-2.png)

![Import Image Step 3](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-3.png)

![Import Image Step 4](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-4.png)

![Import Image Step 5](https://cdn.oootoko.net/blog/assets/img/import-a-custom-certificate-on-aws-certificate-manager/aws-certificate-5.png)

등록 완료! 이제 부터는 AWS에 구축된 서비스에 적용하면 되겠다.
