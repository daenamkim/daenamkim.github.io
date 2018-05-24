---
layout: post
comments: true
title: "설치형 WordPress에 한글과 일어 Noto Sans 적용하기"
date: 2017-02-16 02:28:20
image: '/assets/img/'
description: '설치형 WordPress에 구글이 배포 중인 한글과 일어 Noto Sans 폰트를 적용해보자.'
main-class: 'misc'
color:
tags:
- misc
- wordpress
categories:
twitter_text: '설치형 WordPress에 한글과 일어 Noto Sans 적용하기'
introduction: '설치형 WordPress에 구글이 배포 중인 한글과 일어 Noto Sans 폰트를 적용해보자.'
---

## Noto Sans
구글이 Material Design과 동시에 모든 제품의 UI, UX를 대규모로 개선 중 또는 개선 하였다.
그 중에서도 잘 알려진 요소 중에 하나가 [Noto Sans](https://www.google.com/get/noto/#sans-lgc) 폰트인데 구글은 이를 무료로 배포하고 있다.
무료이면서 아름답기 때문에 많은 앱 또는 웹에 적용 되어지고 있다.

Noto Sans 폰트는 아시아권 언어들도 지원이 되고 있으나 이 글을 포스팅 하는 현재는 earlyaccess로 따로 분류되어 있는 관계로 [서포트에서 제공하는 적용 방법](http://www.kriesi.at/documentation/enfold/register-additional-google-fonts-for-theme-options/)으로는 적용되지 않는다.
참고로 영어권 폰트의 경우 문제없이 동작하며 이 글 마지막에서 다루도록 하겠다.

## 사용 WordPress와 테마
[Enfold](http://www.kriesi.at/themedemo/?theme=enfold-overview) 테마를 기준으로 진행하기로 한다.
다른 테마에 적용할 경우 적용 방법이 다를 수 있으니 서포트 사이트 또는 포럼을 찾아 보아야 한다.
- WordPress 4.7.2
- Enfold 3.8.4
- Enfold Child 1.0

## 한글과 일어 Noto Sans 적용
언어별 테마에 적용하기 위해서는 테마도 언어 별도 준비가 필요하나 여기서는 과정을 생략한다.

**Enfold(또는 Enfold Child)(언어) > General Styling > Fonts > Quick CSS**

![Quick CSS](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/quick-css.png)

**한글 폰트의 경우 아래 코드를 캡처 이미지와 같이 입력한다.**

{% highlight shell %}
@import url(http://fonts.googleapis.com/earlyaccess/notosanskr.css);
html * {
    font-family: 'Noto Sans KR', 'Noto Sans', sans-serif;
    font-style: normal;
    font-weight: 300;
}
{% endhighlight %}

![Quick CSS Korean](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/quick-css-kr.png)

**일어 폰트의 경우 아래 코드를 캡처 이미지와 같이 입력한다.**

{% highlight shell %}
@import url(http://fonts.googleapis.com/earlyaccess/notosansjapanese.css);
html * {
    font-family: 'Noto Sans Japanese', 'Noto Sans', sans-serif;
    font-style: normal;
    font-weight: 300;
}
{% endhighlight %}

![Quick CSS Japanese](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/quick-css-jp.png)

저장 후에 새창으로 해당 페이지에 접속해서 폰트가 잘 적용되어 있는지 확인하자.
![Quick CSS Save](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/quick-css-save.png)

기본적인 확인 방법은 **눈**이다. ;; 관리자 화면에서 커스텀 CSS를 지우고 적용, 그리고 다시 입력 후 적용 하는 식으로 폰트가 바뀌는지 확인한다.
브라우저의 디버거를 이용해서도 웹 폰트가 정상적으로 동작하는지 확인해보자.

![Check Noto Sans 1](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/check-noto-sans-1.png)
![Check Noto Sans 2](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/check-noto-sans-2.png)

혹시 테마에서 커스텀 폰트가 정상적으로 반영되지 않을 경우 다음과 같이 `add_theme_support('avia_template_builder_custom_css')` 를 활성화 한다.

**Enfold의 경우**

작업자와 파일 소유자와 다를 경우 **sudo**를 같이 실행하여 편집을 진행한다.

{% highlight shell %}
$ cd [WordPress DIRECTORY]
$ sudo vi wp-content/themes/enfold/functions.php
{% endhighlight %}

가장 마지막 줄의 코멘트를 다음과 같이 해제 한다.

{% highlight shell %}
/*
 * add option to edit elements via css class
 */
add_theme_support('avia_template_builder_custom_css');
{% endhighlight %}

**Enfold Child의 경우**

{% highlight shell %}
$ cd [WORDPRESS Directory]
$ sudo vi wp-content/themes/enfold-child/functions.php
{% endhighlight %}

가장 마지막 줄에 다음과 같이 추가한다.

{% highlight shell %}
add_theme_support('avia_template_builder_custom_css');
{% endhighlight %}

수정 후에는 꼭 저장하고 나가자.

{% highlight shell %}
:wq
{% endhighlight %}

## 영어 Noto Sans 적용

직접 **functions.php**에 폰트 정보를 추가한다.

**Enfold의 경우**

{% highlight shell %}
$ sudo vi wp-content/themes/enfold/functions.php
{% endhighlight %}

71번 줄에 있는 `add_filter('avia_mega_menu_walker', '__return_false')` 를 찾아서 그 아래에 폰트 정보를 추가한다.

{% highlight shell %}
/*
 * deactivates the default mega menu and allows us to pass individual menu walkers when calling a menu
 */

add_filter('avia_mega_menu_walker', '__return_false');

/*
 * Noto Sans - Custom Fonts.
 */
add_filter( 'avf_google_heading_font', 'avia_add_heading_font');
function avia_add_heading_font($fonts)
{
    $fonts['Noto Sans'] = 'Noto Sans:400,700';
    return $fonts;
}

add_filter( 'avf_google_content_font', 'avia_add_content_font');
function avia_add_content_font($fonts)
{
    $fonts['Noto Sans'] = 'Noto Sans:400,700';
    return $fonts;
}
{% endhighlight %}

**Enfold Child의 경우**

{% highlight shell %}
$ sudo vi wp-content/themes/enfold-child/functions.php
{% endhighlight %}

다음과 같이 코드를 추가한다. 저장하고 종료하는 것을 잊지 말자.

{% highlight shell %}
<?php

/*
* Add your own functions here. You can also copy some of the theme functions into this file. 
* WordPress will use those functions instead of the original functions then.
*/

/*
 * Noto Sans - Custom Fonts.
 */
add_filter( 'avf_google_heading_font', 'avia_add_heading_font');
function avia_add_heading_font($fonts)
{
    $fonts['Noto Sans'] = 'Noto Sans:400,700';
    return $fonts;
}

add_filter( 'avf_google_content_font', 'avia_add_content_font');
function avia_add_content_font($fonts)
{
    $fonts['Noto Sans'] = 'Noto Sans:400,700';
    return $fonts;
}
{% endhighlight %}

화면 갱신 후 **Enfold > General Styling > Fonts** 순서로 이동하면 아래 그림과 같이 Noto Sans 폰트를 적용할 수 있다.

![Noto Sans Fonts Setup](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/noto-sans-fonts-setup.png)

마지막으로 브라우저 디버거에서 웹 페이지가 폰트를 잘 가져오는지 확인하자.
![Check Noto Sans 3](https://cdn.oootoko.net/blog/assets/img/wordpress에-한글과-일어-noto-sans-적용하기/check-noto-sans-3.png)

## 참고
- [Noto Sans Korean](https://fonts.google.com/earlyaccess#Noto+Sans+KR)
- [Noto Sans Japanese](https://fonts.google.com/earlyaccess#Noto+Sans+Japanese)
- [Register Additional Google Fonts for Theme Options](http://www.kriesi.at/documentation/enfold/register-additional-google-fonts-for-theme-options/)
- [Turn on Custom CSS Class field for all ALB Elements](http://www.kriesi.at/documentation/enfold/turn-on-custom-css-field-for-all-alb-elements/)
