---
layout: post
comments: true
title: "A Guide to Becoming a Full-Stack Developer"
date: 2018-04-24 23:20:08
image: '/assets/img/'
description: '풀스택 개발자 되기'
main-class: 'dev'
color: 
tags:
- dev
- webdev
- fullstack
- coding
categories:
twitter_text: '풀스택 개발자 되기'
introduction: '풀스택 개발자 되기'
---

> [Daniel Borowski](https://medium.com/@mrdaniel?source=post_header_lockup)이 작성한 [A Guide to Becoming a Full-Stack Developer in 2017](https://medium.com/coderbyte/a-guide-to-becoming-a-full-stack-developer-in-2017-5c3c08a1600c)를 번역하였으며 필요에 따라 일부 추가 또는 삭제를 하였다. 1년 전에 작성된 글이지만 지금 읽어도 전혀 손색이 없는 풀스택 개발자가 되기위한 요소들을 깔금하게 잘 정리한 블로그라고 생각된다.

[스택 오버플로우 2016 개발자 조사](http://stackoverflow.com/insights/survey/2016)에 따르면 풀스택 웹 개발은 오늘날 가장 인기있는 직업이다. 그도 그럴것이 수많은 온라인과 오프라인 프로그램(강좌)들에서 사람들을 풀스택 개발자가 될 수 있도록 도와주며 심지어는 새로운 개발자들이 높은 급여의 프로그래밍 직업을 가질 수 있도록 도와주기도한다.

[Lynda](https://www.lynda.com/learning-paths/Web/become-a-full-stack-web-developer), [Udacity](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004), [Coursera](https://www.coursera.org/specializations/full-stack), [Thinkful](https://www.thinkful.com/bootcamp/web-development/), [General Assembly](https://generalassemb.ly/education/web-development-immersive) 등 [여러 사이트](https://www.quora.com/What-are-the-best-online-web-development-courses)에서 인기있는 온라인 프로그램들을 확인할 수 있다. 온라인 프로그램들 외에도 웹 개발자가 되기위한 기술들을 가르치는 오프라인 [코딩 부트캠프들](https://www.coursereport.com/reports/2016-coding-bootcamp-market-size-research)도 있다.

이 글에서는 어떤 웹 사이트나 코딩 부트캠프가 최고의 웹 개발 프로그램들을 제공하는지에 대해서는 논하지 않을 것이나 코드를 작성해본 경험이 전혀 없을 경우 풀스택 개발자가 되어 직업까지 구하게 되는 거의 완벽한 [필수 기술들](https://github.com/kamranahmedse/developer-roadmap)을 설명하겠다. 다음 목록의 3가지를 토대로한다.

1. 2017년에 대부분의 프로그램들이 학생들에게 가르치는 조합.
2. 과거 회사에서 개발자 포지션을 인터뷰했던 것과 현재 회사에서 풀스택 개발자 포지션 지원자들을 인터뷰한 개인적인 경험.
3. [Coderbyte](https://coderbyte.com/)에서 코딩 부트캠프를 마치고 프로그래밍 직업을 가진 사람들의 [이야기와 의견](https://coderbyte.com/About/) (아래 참고).

![Stories and feedback](https://cdn-images-1.medium.com/max/1000/1*1GHV2xKwt2HhYnSoa_Qifg.png)

## The Definitive Guide

풀스택 개발자는 애플리케이션의 프론트엔드와 백엔드 포지션에서 일할 수 있는 사람이다. 프론트엔드는 일반적으로 사용자들이 보거나 상호 작용을 위한 앱의 부분을 나타내며 백엔드는 로직, 데이터베이스 처리, 사용자 인증, 서버 설정 등을 다루는 앱의 부분이다. **풀스택 개발자가 되는 것이 반드시 프론트엔드나 백엔드 업무 시 필요한 모든 것에 통달했다는 뜻은 아니지만 두 부분에서 업무가 가능하며 애플리케이션을 만들 때 무엇을 해야 하는지 잘 숙지하고 있다고 생각하면 된다.**

만약 풀스택 개발자가 되어 첫 직업을 구하길 원한다면 아래 배워야할 목록을 참고하자.

## 1. HTML/CSS

![HTML/CSS](https://cdn-images-1.medium.com/max/800/1*mVyO2CM9a_8mpEj0oVh2Nw.jpeg)

온라인 또는 오프라인에 상관없이 어떻게 웹 개발자가 되는지를 가르치는 많은 개별 프로그램들은 HTML과 CSS부터 시작한다. 왜냐하면 이러한 것들이 웹의 구성 요소이기 때문이다. 간단히 말해서, HTML은 컨텐츠를 웹 사이트에 추가할 수 있게 해주고 CSS는 컨텐츠에 스타일을 적용할 수 있게 해준다. 다음의 HTML/CSS과 관련된 주제들은 인터뷰 및 실제로 일을 할 때 자주 나온다.

- [Semantic HTML](https://en.wikipedia.org/wiki/Semantic_HTML).
- [CSS 박스 모델](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)을 설명할 수 있다.
- [CSS 전처리들](https://htmlmag.com/article/an-introduction-to-css-preprocessors-sass-less-stylus)의 이점들. (하나에 대해서 깊은 수준으로 이해할 필요는 없으나 무엇을 위한 것이며 개발에 어떻게 도움이 되는지 정도는 이해하고 있어야 한다.)
- 다른 단말들과 반응형 CSS를 작성하기 위한 [CSS 미디어 쿼리](https://www.w3schools.com/css/css3_mediaqueries.asp).
- [Bootstrap](http://getbootstrap.com/) (페이지 상의 컨텐츠 디자인과 레이아웃을 돕기위한 프레임워크이며 많은 온라인 프로그램들과 학교들이 Bootstrap을 중점적으로 가르치고 있으나 실제로는 상세한 Bootstrap의 특징들 및 방법들보다 근본적인 CSS의 깊은 이해가 더 중요하다.)

## 2. JavaScript

![JavaScript](https://cdn-images-1.medium.com/max/800/1*UgCnCLR0e3R3v7fnCS9ALA.jpeg)

자바스크립트 언어는 매년 더욱더 인기가 올라가고 있으며 새로운 라이브러리들, 프레임워크들 및 도구들이 지속적으로 공개되고 있다. [Stack Overflow 2016 개발자 설문](http://stackoverflow.com/insights/survey/2016)에 의하면 JavaScript는 풀스택, 프론트엔드 그리고 백엔드 모두에서 가장 있기있는 언어이다. 선천적으로 브라우저에서 실행되고 서버 사이드에서도 함께 동작할 수 있는 (아래 있는 Node.js) 유일한 언어이다. 아래는 풀스택 개발자로서 알고 있어야 할 주제들이다.

- [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)이 어떻게 동작하는지에 대한 이해 및 [JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)은 무엇이며 DOM을 어떻게 조작하는지에 대해 이해한다.
- [Functional Composition](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0), Prototypal Inheritance, Closures, Event Delegation, Scope, Higher-Order Functions와 같은 중요한 [언어 특징들](http://javascriptissexy.com/16-javascript-concepts-you-must-know-well/).
- [비동기 제어 흐름](https://kaye.us/javascript-async-control-flow/), [Promise](http://www.datchley.name/es6-promises/)와 [Callbacks](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/).
- 적절하게 코드를 구조화하고 코드의 부분들을 [모듈화](https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc)하는 방법을 학습힌다. [Webpack](https://webpack.js.org/), [Browserify](http://browserify.org/) 또는 [Gulp](http://gulpjs.com/)와 같은 빌드 도구들을 확실하게 도움이 될 것이다.
- 최소한 한 개 정도는 [인기 프레임워크](https://medium.com/javascript-scene/top-javascript-frameworks-topics-to-learn-in-2017-700a397b711)의 사용방법을 숙지한다. (많은 프로그램들은 [React](https://facebook.github.io/react/)나 [AngularJS](https://angularjs.org/)와 같은 라이브러리나 프레임워크를 중점적으로 가르칠 것이나 실제로는 JavaScript 언어의 깊은 이해도를 가지는 것이 훨씬 중요하며 프레임워크의 세부적인 특징들에는 크게 중점을 두지 않는다. 일단 JavaScript에 대해서 잘 이해하고 있다면 최상급 프레임워크를 골라도 크게 어렵지 않을 것이다.)
- [일부 사람들](https://news.ycombinator.com/item?id=12969826)이 이런 것을 적게 사용하지 않으면 천천히 죽어갈 것이라 하지만 [jQuery](https://learn.jquery.com/) 코드는 아직도 대부분의 애플리케이션들에 존재하며 이를 확실한 이해한다면 도움이 될 것이다.
- [테스팅 프레임워크들](http://stateofjs.com/2016/testing/)과 그러한 것들이 왜 중요한지에 대한 지식. (선택 사항)
- 새로운 [ES6의 특징들](https://github.com/lukehoban/es6features)을 공부한다. (선택 사항)

## 3. Back-End Language

HTML/CSS에 대해서 잘 이해했다면 데이터베이스 처리, 사용자 인증 및 애플리케이션 로직과 같은 백엔드 언어를 해보고 싶을 것이다.

모든 온라인 프로그램들과 부트 캠프들은 보통 특정 백엔드 언어에 초점을 맞추지만 실제로는 무엇을 해야 하는지와 선택한 언어의 미묘한 차이를 이해하고 있다면 어떤 언어를 배울지는 중요하지 않다.

만약 누군가에게 어떤 백엔드 언어가 가장 좋냐는 질문을 한다면 엄청나게 많은 [다양한 답변](https://www.quora.com/Which-backend-programming-language-should-I-learn-in-2016)을 들을 것이므로 몇몇 인기 조합들을 아래 목록에 정리하였다. 중요: 어떤 것을 배우기로 하든 간에 끈기있게 최대한 깊게 공부하자. 왜냐하면 아래 목록에 있는 모든 언어들에 대해서 수요가 있기 때문이다.

![Back-End Language](https://cdn-images-1.medium.com/max/800/1*7Va2xnJbgXenQ95RAkhuAQ.jpeg)

- Node.js: 아주 훌륭한 선택인데 왜냐하면 JavaScript 환경을 그대로 사용할 수 있으며 이는 새로운 언어를 배울 필요가 없다는 뜻이다. 이런 이유로 많은 온라인 프로그램들과 부트 캠프들이 Node.js를 가르친다. 웹 애플리케이션 개발 시 배울 필요가 있을 것으로 보이는 가장 유명한 프레임워크는 [Express](https://expressjs.com/)이다.
- Ruby: Ruby로 개발 시 유명한 프레임워크들은 Rails와 Sinatra가 있다. [많은 프로그램들](https://www.quora.com/Why-do-many-coding-bootcamps-still-teach-Ruby-on-Rails-instead-of-JavaScript-for-web-app-development-like-Hack-Reactor-and-Fullstack-Academy-Is-it-because-the-current-demand-is-ROR-and-not-the-future)이 처음 백엔드 언어로 Ruby를 가르친다.
- Python: Python으로 개발 시 유명한 프레임워크들은 Django와 Flask가 있다.
- Java: 최근 프로그램들에서 풀스택 웹 개발 시에 Java는 많이 가르치지 않고 있지만 일부 회사들은 Java를 백엔드로 사용하며 여전히 높은 수요를 가진 언어 (위 그림 참고) 이다.
- PHP: PHP는 최근 프로그램들에서는 거의 가르치지 않지만 Java처럼 지금도 웹에서는 수요가 많고 [중요하다](https://www.quora.com/Why-should-I-learn-to-program-in-PHP-why-is-it-so-important).

## 4. Databases & Web Storage

![Databases & Web Storage](https://cdn-images-1.medium.com/max/800/1*IfG8E5UMuPwBp2OczpiUmw.jpeg)

웹 애플리케이션을 만들 때, 어느 시점부터 데이터를 어딘가에 저장하고 나중에 다시 사용하기를 원할 것이다. 그래서 아래 데이터베이스와 스토리지 관련된 주제는 반드시 잘 숙지하고 있어야 한다.

- [관계형 데이터베이스](https://www.pluralsight.com/blog/software-development/relational-non-relational-databases)의 이점을 이해하기. (예: [SQL](https://en.wikipedia.org/wiki/SQL)).
- [NoSQL](https://www.couchbase.com/nosql-resources/why-nosql) 데이터베이스들에 대한 학습. (예: [MongoDB](https://en.wikipedia.org/wiki/MongoDB)).
- [특정 상황](https://www.sitepoint.com/sql-vs-nosql-differences/)에서 어떤 데이터베이스가 좋을지 이해하기.
- [Redis](https://redis.io/)나 [memcached](https://memcached.org/)와 같은 In-memory 저장 방식의 [이점](http://www.computerweekly.com/feature/In-memory-databases-What-they-do-and-the-storage-they-need)들을 이애하기.
- 세션, 쿠키 및  캐시 데이터를 브라우저에 저장하가 위한 [Web storage](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API).
- 데이터 베이스 [확장](http://www.infoworld.com/article/2609739/database/scaling-and-querying-large-nosql-databases.html), [ACID](https://en.wikipedia.org/wiki/ACID) 및 [ORM](http://stackoverflow.com/questions/1279613/what-is-an-orm-and-where-can-i-learn-more-about-it) (모두 선택 사항).

## 5. HTTP & REST

![HTTP & REST](https://cdn-images-1.medium.com/max/800/1*3jazyUwurr2zfp5uEIi2Dg.png)

HTTP는 인터넷상의 [Stateless](https://en.wikipedia.org/wiki/Stateless_protocol) (서버 사이드에 동작 상태를 저장하지 않는 방식. 반대는 Stateful.) 애플리케이션 프로토콜이며 클라이언트들이 서버들과 통신할 수 있게 해준다. (예: JavaScript 코드는 서버에서 동작 중인 백엔드 코드에 HTTP를 통해서 [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) 요청을 생성한다.) 숙지해야 할 중요한 주제들은 다음과 같다.

- [REST](https://www.pluralsight.com/blog/tutorials/representational-state-transfer-tips)는 [무엇](https://en.wikipedia.org/wiki/Representational_state_transfer)이고 HTTP 프로토콜과 웹 애플리케이션들을 고려할 때 왜 [중요한가](http://stackoverflow.com/questions/671118/what-exactly-is-restful-programming).
- RESTful API ([POST/GET](http://stackoverflow.com/questions/3477333/what-is-the-difference-between-post-and-get) 요청들.) [설계](http://www.restapitutorial.com/)를 위한 [우수한 사례들](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api).
- [Chrome DevTools](https://developer.chrome.com/devtools) 사용방법을 배우는 것은 정말 도움이 된다.
- [SSL 증명서](https://www.digicert.com/ssl.htm)는 무엇인가?
- [HTTP/2 & SPDY](https://hpbn.co/http2/) (선택 사항).
- [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API), [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API) 및 [Service Workers](https://aarontgrogg.com/blog/2015/07/20/the-difference-between-service-workers-web-workers-and-websockets/) (모두 선택 사항).

## 6. Web Application Architecture

![Web Application Architecture](https://cdn-images-1.medium.com/max/800/1*wWDnYaaeAIsYVmNACstddg.png)

HTML/CSS, JavaScript, 백엔드 프로그래밍, 데이터베이스 그리고 HTTP/REST를 잘 이해하고 있다면 다루기 어려운 부분으로 가보자. 이 때, 어느정도 복잡한 웹 애플리케이션을 만들고자 한다면 어떻게 코드를 구조화 하고, 파일들을 분리하고, 어디에서 큰 미디어 파일들을 제공하고, 어떻게 데이터베이스 안에 데이터를 구조화 하는지, 어디에서 특정 태스크들을 수행할 지 (클라이언트 사이드 vs 서버 사이드) 등에 대해서 알아야 한다.

온라인에서 훌륭한 사례들을 읽을 수 있도 있으나 가장 좋은 방법은 [여러 동작하는 부분들](https://www.pinterest.com/pin/266697609164793095/)을 포함한 큰 애플리케이션을 직접 작업 하면서 애플리케이션 구조를 학습하는 것이며 훨씬 더 좋은 방법은 팀에서 어느정도 크고 복잡한 애플리케이션을 함께 개발하는 것이다.

이는 7년 이상의 경력인 사람이 2년 경력인 사람보다 CSS 또는 JavaScript를 반드시 더 잘 안다고는 할 수 없는 이유이지만 그들은 모든 시간을 다양한 애플리케이션들과 웹 사이트들을 구축하는데 사용했을 것이며 개발 시 가장 효율적이고 "큰 그림"을 볼 수 있도록 어떻게 애플리케이션들을 설계 (다른 [중요한 것들](https://www.quora.com/When-does-a-software-developer-become-a-senior-software-developer)을 공부하는 가운데) 해야 하는지를 [배웠다](http://stackoverflow.com/questions/816258/good-architecture-interview-questions). 아래는 어떻게 효율적으로 웹 애플리케이션을 설계하는지 도움을 주는 내용들이다.

- 인기 있는 [플랫폼 서비스](https://en.wikipedia.org/wiki/Platform_as_a_service)들 (예: [Heroku](https://www.heroku.com/)와 [AWS](https://aws.amazon.com/what-is-aws/)) 을 학습한다. Heroku는 아주 적은 설정과 서버 유지보수 만으로 코드를 업로드하고 애플리케이션을 가동할 수 있고 AWS는 스토리지, 비디오 처리, 부하 처리 등을 지원하는 수많은 제품들과 서비스들을 제공한다.
- 애플리케이션과 최신 브라우저를 위한 [성능](https://hpbn.co/?utm_source=igvita&utm_medium=referral&utm_campaign=igvita-homepage) [최적화](https://www.igvita.com/posa/high-performance-networking-in-google-chrome/).
- 웹 애플리케이션 설계 시에 포함해야 할 [선택 사항들](https://www.quora.com/What-does-a-web-application-architecture-include).
- Microsoft [웹 애플리케이션 설계](https://msdn.microsoft.com/en-us/library/ee658099.aspx).
- [MVC](http://softwareengineering.stackexchange.com/questions/127624/what-is-mvc-really).
- Most importantly though you should try to work on projects with people, look at codebases of popular projects on GitHub, and learn as much as you can from senior developers.
- 사람들과 함께 프로젝트를 진행해야 하는 것도 중요하지만, GitHub의 인기 프로젝트를 코드 베이스로 본다든지, 상급 개발자에게 최대한 [많이](https://design.quora.com/Notification-System-Design-99+) [배워라](https://www.youtube.com/watch?v=UbbXYRb-hCU).

## 7. Git

![Git](https://cdn-images-1.medium.com/max/800/1*NomW1pXBFlKFFwZuTXVSTA.png)

Git은 팀에서 작업하는 개발자들이 모든 변경 사항들을 코드 베이스로 추적할 수 있게 해주는 버전 관리 시스템이다. 최신코드를 가져오거나 코드의 일부를 갱신하고, 고치고, 다른 사람의 코드를 망가트리지 않고 변경하기 위해서는 Git의 일부 중요한 기능들에 대해서 숙지해야 한다. 반드시 Git의 개념을 이애하고 사용할 수 있어야 한다.

- 자주 사용하게 될 Git 명령어들 [참고 목록](https://git-scm.com/docs).
- Git과 GitHub를 사용한 초보자들을 위한 [튜노리얼](http://product.hubspot.com/blog/git-and-github-tutorial-for-beginners).

## 8. Basic Algorithms & Data Structures

![Basic Algorithms & Data Structures](https://cdn-images-1.medium.com/max/800/1*YewAB-IJnGpBr3LtvZPiRg.png)

이 주제는 다소 개발 세계에서 양극화되어 있는데, 이는 트리 순회, 정렬, 알고리즘 분석, 행렬 처리 등 컴퓨터 사이언스 주제들에 대해서 생각하지 않는 개발자들이 있기 때문이다.

그러나 구글과 같은 회사들은 이런 형태의 질문들을 인터뷰에서 [물어보기로](https://www.glassdoor.com/Interview/Google-Software-Engineer-Interview-Questions-EI_IE9079.0,6_KO7,24.htm#InterviewReview_4168541) 악명이 높다. [어떤 사람](https://www.quora.com/What-interview-questions-does-Google-ask-their-Front-End-engineer-candidates)이 구글의 프론트엔드 엔지니어링 인터뷰에 대해서 한 말이다.

> <cite>[Ryan McGrath](https://www.quora.com/profile/Ryan-McGrath)가 언급한 것 처럼, 프론트엔드 엔지니어들은 모든 엔지니어들처럼 확실한 컴퓨터 사이언스 배경 지식을  가지기를 기대한다고 했다.</cite>

실제로 지원자들에게 컴퓨터 사이언스 학위 또는 동등한 수준을 요구하는 회사들이 있는 반면, 많은 회사들은 어떻게 애플리케이션을 개발하고 모든 영역에 대해서 이해하고 있다는 것을 증명할 수 있다면 기술 자격이 없더라도 고용할 것이다. 그러나 유능한 개발자가되어 비효율적인 코드를 작성하거나 잘못된 도구를 사용하지 않는 것은 기본 알고리즘과 데이터 구조를 이해하고 상호보완적 관계를 분석할 수 있다. 그래서 확실히 공부해야할 내용들을 정리하였다.

- [알고리즘과 데이터 구조 기술들](https://medium.com/coderbyte/how-to-get-good-at-algorithms-data-structures-d33d5163353f)을 향상시킨다.
- [해시 테이블](http://stackoverflow.com/questions/730620/how-does-a-hash-table-work)을 공부하고 [깊은](https://www.quora.com/How-do-I-create-my-own-Hash-Table-implementation-in-Python) 수준으로 이해한다. 이 데이터 구조는 JavaScript의 Object(Python에서는 Dictionary, Ruby에서는 Hash)를 사용한다.
- 데이터 구조에서 트리와 그래프가 어떻게 [도움](https://www.quora.com/Under-what-circumstances-would-a-web-developer-need-to-use-data-structures-such-as-Linked-Lists-BST-and-Graphs)이 되지는 이해한다.
- 기본적인 [Big-O 분석](https://justin.abrah.ms/computer-science/big-o-notation-explained.html)을 이해하고 필요하지도 않은 3중 루프를 만드는 [바보같은](https://medium.com/@felipernb/algorithms-data-structures-and-web-development-7772e088f1d3) 짓을 하지말자!
- 언제 [오브젝트와 어레이](http://stackoverflow.com/questions/688097/objects-vs-arrays-in-javascript-for-key-value-pairs)의 사용하는지를 알고 상호보완적 관계를 이해한다.
- 대용량 데이터를 처리할 때 [캐시](https://martin.kleppmann.com/2012/10/01/rethinking-caching-in-web-apps.html)가 매우 중요한 이유를 학습한다. 또한 인메모리와 디스크 스토리지의 [장점과 단점](http://stackoverflow.com/questions/25802521/difference-between-in-memory-databases-and-disk-memory-database)을 학습한다.
- 큐와 스택의 [차이점](http://stackoverflow.com/questions/2074970/stack-and-queue-why)을 학습한다.

> 번역을 하면서 내용을 전부 꼼꼼히 들여다 보니 왠지 허성 세월을 보낸 것 같기도 하고 스스로에게 많이 반성하는 시간이 되었다. 그래도 지금이라도 정신이 들어서 다행이다.
