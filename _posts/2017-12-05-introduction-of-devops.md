---
layout: post
comments: true
title: "Introduction of DevOps"
date: 2017-12-05 06:36:33
image: '/assets/img/'
description: '개발 황무지를 DevOps로 개간하기.'
main-class: 'devops'
color:
tags:
- devops
categories:
- "Challenging DevOps."
twitter_text: '개발 황무지를 DevOps로 개간하기.'
introduction: '개발 황무지를 DevOps로 개간하기.'
---

2017년도 초에 진행한 DevOps 도입기를 적어볼까 한다.

## 그 옛날 (BEFORE)
2014년 12월 중순 [Ascent Networks](http://www.ascentnet.co.jp/ko)에 입사 하였다. 그 당시 사용되고 있는 개발 환경은 메일과 [IDE](https://ko.wikipedia.org/wiki/%ED%86%B5%ED%95%A9_%EA%B0%9C%EB%B0%9C_%ED%99%98%EA%B2%BD)를 제외하면 다음과 같았다.
- 소스 관리: [SVN](https://subversion.apache.org/)
- 프로젝트 관리: [Redmine](https://www.redmine.org/)
- 빌드 및 배포: [Hudson](http://hudson-ci.org/)
- 모니터링: [Cacti](https://www.cacti.net/), [Nagios](https://www.nagios.org/)
- 그룹 챗: [Skype](https://www.skype.com/en/new/)

### SVN
분산 개발 환경 [Git](https://git-scm.com/)이 이미 표준으로 자리잡아 가고 있는 와중에 우리는 내부 인프라에 자체 구축한 SVN을 사용하고 있었고 정체 모를 소스들과 초기에 작업하신 분이 솔루션 관련 모든 소스를 한 폴더에 넣고 관리하는 바람에 관리가 여간 불편한 것이 아니었다. 게다가 리뷰 시스템이 도입되어 있지 않았기 때문에 누가 무슨 작업을 했는지, 무엇을 올렸는지, 혹은 무엇을 삭제(?) 했는지 전혀 알 길이 없었다. 정확히는 나중에 알게 되었다.

### Redmine
한 달치 업무를 모두 레드마인의 스프린트 + 시간 단위 공수로 쪼개서 등록 해두고 월 말 쯤(약 한 달 주기)에 일괄로 배포 했었다. [애자일 스크럼](https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%81%AC%EB%9F%BC_(%EC%95%A0%EC%9E%90%EC%9D%BC_%EA%B0%9C%EB%B0%9C_%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4))을 하려는 의도 였을 것으로 보이나 현실은 대단히 어려웠고 비효율적이라고 생각 되었다. 왜냐하면 엄청나게 많은 고객 문의와 장애 대응과 동시에 기능 개발을 해야 했었기 때문에 기능에 대한 일치된 정보를 교환하고 개선하는 것이 어려운 상황이 이었으며 상황에 따라서 배포를 유동적으로 하고자 하는 강한 욕구가 들었다.

그 외에 다음과 같은 문제점이 있었다.
- 일부 보드나 레드마인 내의 Wiki를 사용했는데 정리가 되지 않아 실제 작성했던 사람 외에는 찾지 않는 장소가 되어 버렸음.
- 누가 무엇을 올리더라도 작성자가 알려주지 않으면 그게 무엇인지 아무도 알 길이 없었음.
- 구글 드라이브로 문서를 작성 하면서 자료의 보관 위치가 분산되어 나중에는 나 조차도 아예 가지 않게 되었음.
- 팀 규모에 비해서 지나치게 기능이 많으며 직관적인지 못함.

### Hudson
앱 빌드 및 배포로 사용되었으나 설정이 불완전하였으며 서버에 파일을 올려주는 작업 외에 나머지 작업은 수동이었다. 허드슨은 보안 패치도 2016년 2월을 기점으로 더이상 진행되지 않고 있으며 생태계가 더이상 발전되지 않고 있었다. 사실상 방치된(?) 패키지였다. 허드슨이 이렇게 된 이유는 [기사](http://www.itworld.co.kr/print/64516)를 참고하자.

### Skype
솔루션과 관련된 모든 의견 교환은 스카이프 그룹 챗을 통해서 오고 갔다. 개발자들을 위한 그룹 챗을 따로 만들어서 개발자들 끼리만도 얘기는 할 수 있었으나 다음과 같은 문제점(Skype for Business가 아니라서 그랬는지 모르겠다.)이 있었다. 
- 2017년초 지금까지 대화한 솔루션 그룹 챗 내용이 아주 깨끗하게 사라졌음. (정말 아무것도 남기지 않고 완벽하게 사라졌다. >.<)
- 파일 전송이 욕 나올 정도로 느리고 불안정함.
- 외부 서비스들과의 연동 기능이 없음. (메일, Redmine, 나중에는 [Google Keep](https://keep.google.com/), [Wunderlist](https://www.wunderlist.com/ko/download/)로 바꾸면서 가면 갈수록 확인하는 것만 해도 상당한 부담이 되었다.)
- 실제 전화번호로 전화가 되는 것 외에는 좋은 점이 없어 보임. (카톡을 쓰는 것이 낮다고 생각이 들 정도였음.)

## 결심 그리고 현재 (AFTER)
![wasteland](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/wasteland.jpg)
><cite>[사진 출처](https://cdn.pixabay.com/photo/2014/09/25/21/08/litter-460984_960_720.jpg)</cite>

더이상 미루지 말고 대대적인 **황무지 개간**을 시작할 때가 되었다고 판단되었다. 2017년 초 모든 것을 갈아 엎자는 취지 하에 **DevOps** 방법론을 우리 회사에 맞게 도입하기로 하였다.

- 소스 관리: [GitHub](https://github.com/)
- 프로젝트 관리: [Trello](https://trello.com/)
- 빌드 및 배포: [Jenkins](https://jenkins.io/)
- 서버 테스트: [Serverspec](http://serverspec.org)
- 모니터링: Cacti, Nagios, [Elasticsearch](https://www.elastic.co/jp/products/elasticsearch)
- 그룹 챗: [Slack](https://slack.com/)

### GitHub
![GitHub Logo](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/github-logo.png)
큰 회사들처럼 사내에 구축하지는 않고 [SasS](https://ko.wikipedia.org/wiki/SaaS) 형태의 [Team](https://github.com/pricing/team) 플랜을 사용 중이다. GitHub 사용의 장점은 다음과 같다.
- 매우 다양한 외부 서비스들과 연동 가능. (Slack, Jenkins, Trello 등.)
- 현재 대부분의 오픈 소스 프로젝트가 가동되고 있는 동일 인터페이스를 그대로 사용하므로 GitHub에서 조금이라도 개발 경험이 있는 사람의 경우 **학습 비용이 0임**.
- 인터페이스가 다른 서비스들([Bitbucket](https://www.atlassian.com/software/bitbucket), [GitLab](https://about.gitlab.com/) 등.)에 비해서 심플하면서도 직관적임. (지금은 다른 서비스들도 사용하기 많이 편리해졌을 것으로 생각된다.)
- 코드 리뷰. (별도 리뷰 서비스를 구축할 필요가 없음.)

GitHub의 서비스 안정성에 대해서 불만을 표시하는 분들을 간혹 보았으나 개인적으로는 전혀 불편함 없이 사용 중이다. 게다가 관리 비용을 시간 단위로 환산 한다면 사용하는 것이 더더욱 합리적이라고 생각된다.

우선 SVN에 떡처럼 붙어 있던 모든 파트별 저장소를 분리해서 GitHub으로 전부 Import 후 Slack 및 Trello와도 연결하였다.

개발 시 GitHub의 PR(Pull Request)를 이용한 [GitHub Flow](https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/)를 도입하기로 했다. 이유는 다음과 같다.
- **master**와 **feature branch** 구성으로만 진행함. (**master**는 항상 프로덕션 환경에 배포 가능한 상태를 유지함.)
- 구조가 간단하고 브랜치 명으로 작업 내용을 알 수 있으므로 직관적임.
- 작업 중인 코드는 수시로 서버에 push 하면서 동시에 **[WIP]**를 제목에 추가해서 여러번 코드 리뷰의 요청이 가능함.
- 결과적으로 소인 그룹에서 작업 시 작업 속도가 향상됨.

![GitHub Flow](http://cdn-ak.f.st-hatena.com/images/fotolife/s/shoma2da/20151104/20151104223339.png)

### Trello
![Trello Logo](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/trello-logo.png)
현재는 무료 버전으로 사용 중이며 필요하면 향후 유료 플랜으로 전환을 검토 예정이다. 엄청나게 유명한 [Jira](https://www.atlassian.com/software/jira) 도입을 검토 하였으나 이 또한 팀 규모에 비해 지나치게 기능이 복잡(=학습 비용 증가)한 것이 문제로 대두 되었다. Trello 도입을 검토하는 시점에 Jira 개발사인 [Atlassian](https://www.atlassian.com/)이 한화 약 [5천억원에 Trello를 인수](http://techneedle.com/archives/29533)하였다. 기사를 보는 순간 서비스에 대한 매우 큰 신뢰가 느껴졌다. (나도 참 단순하다.) 그 밖에 이유는 다음과 같다.
- 매우 다양한 외부 서비스들과 연동 가능. (Slack, GitHub 등.)
- 사용성이 매우 직관적임.
- 리스트와 카드를 기반으로 상당히 유동적인 업무 프로세스 설계가 가능함.

개발팀을 시작으로 Trello를 전사적으로 도입해서 사용중이며 현재까지 원활하게 사용되고 있다.

![Trello Usage](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/trello-usage.png)
><cite>[ListeningMind](http://www.listeningmind.com/ko/) 솔루션 개발 보드의 실제 모습. (Error 리스트의 카드 수는 기밀 사항이므로 모자이크 처리함.;;)</cite>

딱 보아도 Redmine 쓸 때보다 비교가 안되게 직관적이다.

### Jenkins
![Jenkins Logo](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/jenkins-logo.png)
빌드 및 배포 서버는 SaaS 형태가 아닌 내부에 직접 구축을 했다. 관리 비용이 발생함에도 불구하고 내부에 구축하기로 한 이유는 다음과 같다.
- GitHub, Slack 등 새로 도입한 서비스들과 연동 가능.
- 각 서비스마다 빌드 및 배포 환경, 처리 절차가 다름.
- 매우 다양 하면서 상세한 커스텀 설정이 가능함.
- 플러그인 생태계가 잘 활성화 되어 있음.
- 현재도 계속해서 많은 패치 및 업그레이드가 이루어지고 있음.

단점이라면 역시 관리 비용인데 필요한 기능을 하나 하나 만들고 붙이고 확인하는 작업이 필요하다. (물론 나중에 같은 기능이 필요하면 복사 할 수 있다.)

기존의 Hudson에서 조금 만들어져 있던 것을 모두 버리고 새롭게 처음부터 모든 빌드 및 배포 프로세스를 설계 및 작성하였다.

![Jenkins Usage](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/jenkins-usage.png)
><cite>ListeningMind 배포 과정.</cite>

### Serverspec
![Serverspec Logo](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/serverspec-logo.jpg)
타겟 서버에서 설치된 패키지, 프로세스, 포트, 파일, 디렉토리 및 크론탭 등 매우 다양하고 정교한 서버 테스트를 지원하는 도구이다. 이런 도구의 도움 없이 서버를 운영해본 사람이라면 이런 확인 작업이 얼마나 번거롭고 실수가 잦았었는지를 기억할 것이다. (아니면 나만 그랬을 수도 있다. ;;) 설정 가능한 상세한 내용은 [여기](http://serverspec.org/resource_types.html)를 참고하자.

아래는 Serverspec 실행 시 실제로 오류가 발생했을 때의 상황이다. 프로세스 수가 9개 이어야 하는데 5개로 확인 되면서 오류가 발생한 것이다.
{% highlight shell %}
Process "celery worker"
  count
    should eq 5

Failures:

  1) Process "celery worker" count should eq 9
     On host `deploy.1.production.worker.listeningmind.com'
     Failure/Error: its(:count) { should eq 9 }
       
       expected: 9
            got: 5
       
       (compared using ==)
       /bin/sh -c ps\ aux\ \|\ grep\ -w\ --\ celery\\\ worker\ \|\ grep\ -v\ grep\ \|\ wc\ -l
       5

     # ./spec/lm-worker-base/base_spec.rb:8:in `block (2 levels) in <top (required)>'

Finished in 2.75 seconds (files took 0.26748 seconds to load)
11 examples, 1 failure

Failed examples:

rspec ./spec/lm-worker-base/base_spec.rb:8 # Process "celery worker" count should eq 9

/var/lib/jenkins/.rbenv/versions/2.4.1/bin/ruby -I/var/lib/jenkins/.rbenv/versions/2.4.1/lib/ruby/gems/2.4.0/gems/rspec-support-3.6.0/lib:/var/lib/jenkins/.rbenv/versions/2.4.1/lib/ruby/gems/2.4.0/gems/rspec-core-3.6.0/lib /var/lib/jenkins/.rbenv/versions/2.4.1/lib/ruby/gems/2.4.0/gems/rspec-core-3.6.0/exe/rspec --pattern spec/\{lm-worker-base,lm-worker-production-1\}/\*_spec.rb failed
Build step 'Execute shell' marked build as failure
Finished: FAILURE
{% endhighlight %}
><cite>Serverpec 실행 결과.</cite>

Jenkins 프로젝트로 만들어 놓고 빌드 파이프라인에 적용시켜 두면 상당히 편리하다.

### Slack
![Slack Logo](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/slack-logo.png)
현재 [Standard](https://ascentnet.slack.com/plans) 플랜으로 사용하고 있으며 이 앱은 너무 유명해서 굳이 설명이 필요 없을 것 같지만 선정한 이유를 간단히 정리하면 다음과 같다.
- 매우 다양한 서비스들과 연동이 가능함. (GitHub, Trello, Jenkins 등.)
- 전화번호 전화 빼고 스카이프에서 가능한 모든 기능을 사용할 수 있음. (영상 통화, 화면 공유 등.)
- 위에서 소개한 모든 서비스들과 연동이 가능해서 Slack 하나 만으로 모든 작업 흐름을 알 수 있음.
- 각종 봇 서비스들과 연동해서 다양한 편의성을 도모할 수 있음.

![Slack Usage](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/slack-usage.png)
><cite>팀 별, 업무 별로 세분화된 Slack 채널들.</cite>

GitHub, Trello, Jenkins, 캘린더, 개인 메일, 감시 메일까지 연동할 수 있는 것은 모두 Slack이랑 연동을 해 놓아서 모든 업무 과정을 한 곳에서 확인할 수 있다. 예전처럼 모든 곳을 돌아다닐 필요가 없어졌으며 결과적으로 스케줄을 깜빡 했다던가 카드의 코멘트를 보지 못했다던가 하는 유치원생 레벨의 핑계는 더 이상 안통하게 되었다.

### Bot
![Hubot](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/hubot.png)
Jenkins까지 가지 않고도 현 상태 확인 및 배포 명령을 보내고자 Bot도 만들었다. 내부 서버에 구축하였으며 AsBot(Ascent Bot)으로 이름을 정하였다. [Hubot](https://hubot.github.com/)을 이용해서 작성 되었으며 언어는 [CoffeeScript](http://coffeescript.org/)로 되어 있다. Slack이 [Hubot 애드온](https://slack.com/apps/A0F7XDU93-hubot)을 지원하므로 연동 과정은 그다지 어렵지 않았으나 Jenkins와 연결하는 과정에서 [CSRF](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%9A%94%EC%B2%AD_%EC%9C%84%EC%A1%B0) 토큰 이슈가 나서 조금 애를 먹긴 했었다.

![Hubot Usage](https://cdn.oootoko.net/blog/assets/img/introduction-of-devops/hubot-usage.png)

## 개발 흐름 정리
- 이슈 발생, Trello 카드 작성, 브랜치 생성 및 작업 시작.
- 작업 완료, 커밋 및 푸시.
- Lint, Unit Test. (추가 중.)
- PR. (필요한 경우 PR과 동시에 브랜치 소스로 개발/스테이징에 배포 및 테스트.)
- 코드 리뷰 및 승인.
- Functional Test. (추가 중.)
- 마스터 브랜치에 머지.
- 개발 서버에 자동 배포 및 서버 테스트.
- 스테이징/프로덕션 환경에 배포 및 서버 테스트.

## 마무리
모든 업무의 시작은 Slack을 통해서 한 번에 확인 할 수 있게 되었으며 모든 업무 내용이 채널 내부에서 관련자들과 실시간으로 공유되고 의견을 주고받을 수 있게 되었다. 더 자주, 더 쉽고, 더 빠르게 작업할 수 있게 되었으며 더욱더 훌륭한 개발 환경을 만들기 위해서 계속해서 변화를 도모할 방침이다. [Ansible](https://www.ansible.com/)을 이용한 인프라 프로비저닝, Elasticsearch(현재는 구축만 되어 있음.)를 이용한 로그 분석 추가, 모바일 앱 개발을 위한 빌드서버, 현재는 내부 인프라의 여유가 있지만 향후 [AWS](https://aws.amazon.com/) 클라우드로의 이전 등 고민과 개선은 앞으로도 계속 될 것이다.
