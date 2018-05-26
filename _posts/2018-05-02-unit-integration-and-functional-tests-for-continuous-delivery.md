---
layout: post
comments: true
title: "Unit, Integration, and Functional Tests for Continuous Delivery"
date: 2018-05-02 12:21:54
image: '/assets/img/'
description: '생산성 향상을 위해 테스트는 기본!'
main-class: 'dev'
color:
tags:
- dev
- webdev
- test
categories:
twitter_text: '생산성 향상을 위해 테스트는 기본!'
introduction: '생산성 향상을 위해 테스트는 기본!'
---

> [Chairat Onyaem](https://medium.com/@pacroy?source=post_header_lockup)이 작성한 [Separate Unit, Integration, and Functional Tests for Continuous Delivery](https://medium.com/pacroy/separate-unit-integration-and-functional-tests-for-continuous-delivery-f4dc240d8f2f)를 번역하였다. 웹 애플리케이션을 개발하면서 필요한 테스트들에 대한 개념을 간결하고 알기 쉽게 정리한 블로그라고 생각된다.

나는 최근에 [Eric Elliott](https://medium.com/@_ericelliott)가 작성한 ["JavaScript Testing: Unit vs Functional vs Integration Tests"](https://www.sitepoint.com/javascript-testing-unit-functional-integration/) 글을 읽은 후에 3가지 테스트 형태의 차이를 이해하는데 많은 도움이 되었다. 3가지 형태는 Unit, Integration 그리고 Functional 이며 아래와 같은 피라미드를 본 적이 있을 것이다.

![Test Automation Basics](https://cdn-images-1.medium.com/max/800/1*dciXQRSvE_4fSupO9SSI7Q.png)
<cite>출처: [Test Automation Basics — Levels, Pyramids & Quadrants](http://www.duncannisbet.co.uk/test-automation-basics-levels-pyramids-quadrants)</cite>

내 생각으로 피라미드의 최상단에 있는 GUI Tests는 Functional Test이다. 때로는 **End-to-End Test** 또는 **System Test** 라고 불린다. 그리고 피라미드에 가운데 있는 API, Integration 그리고 Component Tests를 모두 Integration Tests로 정의한다. 보통은 대부분의 앱들이 Unit과 Functional Test를 필수로 한다. 복잡한 앱에서는 Integration Test가 필요할 수도 있다. 우리는 이런 것들을 테스트 모음 이라고 부르도록 하자.

실제로는 당신이 3가지 주요 구성층들을 확실히 구분하기는 어려울 것으로 보이며 각 구성층마다 겹치는 부분이 존재한다. 다른 작은 구성들을 호출하는 큰 구성은 하나의 컴포넌트나 API가 될 수 있다. UI를 통한 테스트는 Functional 또는 API 테스트가 될 수 있다.

그러나, 예를 들어 당신이 지속적 배포(Continuous Delivery)를 위해 이런 테스트들을 자동화 하고자 할 때 이들을 구분하는 것은 매우 중요하다. 특히 테스트 결과들로부터 다양한 행동들과 당신이 예상한 결과들을 확인할 수 있는 Unit Test가 매우 중요하다.

우선, 이들의 차이점들을 알아보자.

## Unit Test

- 앱의 개별 컴포넌트를 검증(Validate).
- 컴포넌트의 입력과 출력 파라미터들의 확인(Assertion) 테스트.
- 테스트는 개발자의 관점에서 수행됨.
- 실시간 개발자 피드백.
- 간단하고, 빠르고, [F.I.R.S.T. Principle](https://github.com/ghsukumar/SFDC_Best_Practices/wiki/F.I.R.S.T-Principles-of-Unit-Testing)의 특징들을 가짐.
- **통제 불가능한 의존성이**나 다른 컴포넌트에 대한 인터페이스(예: 데이터베이스 접근, 파일/로그, 읽기/쓰기, 원격/API 호출 등.)가 **없음**.
- 언제(내일, 다음 달, 내년, 다음 5년), 어디에서(개발/QA/프로덕션 서버) 실행하던지 항상 일관된 결과를 표시함.
- 아래 4가지 질문들에 대해서 좋은 버그 리포트를 생성.

> 1. 어떤 컴포넌트가 테스트 중인가?
> 1. 예상되는 행동은 무엇인가?
> 1. 실제 결과는 무엇이었나?
> 1. 예상되는 결과는 무엇인가?

## Integration Test

- 컴포넌트들 협업을 검증(Validate).
- 컴포넌트들의 입력과 출력 파라미터들(API), UI 또는 부작용들(예: 데이터베이스, 파일, 로그 등.)을 확인(Assertion) 테스트.
- 테스트는 개발자(예: API) 또는 최종 사용자(예: UI)의 관점에서 수행됨.
- 간단하게 말하면, 통제 불가능한 의존성과 인터페이스(예: 데이터베이스 접근, 파일/로그, 읽기/쓰기, 원격/API 호출 등.)를 가지는 Unit Test(규모가 얼마나 큰지에 관계없이)임.
- 예측할 수 없는 의존성들 때문에 실행 시에 일관되지 않은 결과를 표시함.

## Unit vs. Integration Test

이 두가지의 다른점을 조금 더 이해하기 위해서 다음의 예를 살펴보도록 하자.

아래 다이어그램에서 보여지는 것과 같은 호출관계를 가진 여러 기능들(모듈식 프로그램)을 생각해 보자. 기능 E는 연산을 수행하기 위해서 데이터베이스로 부터 테이블을 읽어야 하며 E를 호출하는 것은 A와 B의 의존성을 가진다.

![Components with dependencies](https://cdn-images-1.medium.com/max/800/1*x02eaLtr5Rfb3e5cH-7M3w.png)
<cite>의존성을 가진 컴포넌트들<cite>

이 경우, 당신은 C, D, F 그리고 G를 위한 Unit Test만을 작성할 수 있다. 만약 E, B 또는 A를 위한 테스트를 작성한다면, 그것은 Unit Test가 아니고 Integration Test이며 이는 Unit Test 작성을 위한 도구인 [xUnit framework](https://martinfowler.com/bliki/UnitTest.html)의 목적을 벗어나게 된다. 가장 위험한 것은 당신이 Unit과 Integration Test를 합친 후에 어떻게 그 버그 리포트를 신뢰할 것인가이다.

그래서 당신이 E, B 그리고 A를 Unit Test로 "테스트 가능" 하게 하려면, 다음과 같은 방법들이 있다. 첫 번째 방법은 당신의 플랫폼에서 E가 항상 같은 결과를 가지는 것에 대해서 보장할 수 있는 Mock/Fake 데이터베이스를 사용하는 것이다.

다른 방법은 다음 그림과 같이 [Dependency Injection](https://en.m.wikipedia.org/wiki/Dependency_injection)로 구현된 [Inversion of Control (IoC)](https://en.wikipedia.org/wiki/Inversion_of_control)를 적용하는 것이다.

![Dependency Injection](https://cdn-images-1.medium.com/max/800/1*H-eWJjGCYKLoJOZrWAOFxQ.png)
<cite>의존성 주입</cite>

당신은 데이터베이스로부터 오직 E가 필요한 데이터만을 가져오는 기능 H를 작성할 수 있다. 필요한 데이터를 가져오기 위해서 당신이 호출자가(Caller)가 H를 호출할 수 있게 하면 이 데이터(의존성)를 E(A와 B를 통해서)로 전달(주입)하게 된다.

> <cite>Integration Test는 항상 Unit Test와 분리해야 한다.</cite>

## Functional Test

- 전체 앱 또는 시스템이 예상대로 동작하는지를 보장함.
- End-to-End Test 또는 System Test(Functional Test들의 집합) 이라고도 알려져 있음.
- 주로 실제 사용자 인터페이스의 출력 확인(Assertion) 테스트.
- 테스트는 최종 사용자의 관점에서 수행됨.
- 보통 **행복한 경로들**에 대해 철저한 테스트들을 진행함. 사용자 로그인, 가입, 구매 작업 흐름 및 모든 중요한 사용자 작업 흐름들이 예상대로 동작하는지와 같은 중요한 앱의 처리 능력을 보장함.

---

또 다른 Functional Test라고 불리는 Smoke Test를 소개한다.

## Smoke Test

- 제품 안전(production-safe)을 위한 기능 테스트들의 집합.
- 배포 처리 중에 잘못된 중요한 기능들이 없는지 확인하기 위해 실행.
- 목적은 "당신은 사용자들이 당신보다 먼저 버그를 발견하는 것을 원하지 않는다" 임.
- 당신은 반드시 이런 종류의 테스트를 당신의 자동 테스트 모음의 다른 테스트들과 분리해야며 이로써 배포 후에 실행할 수 있게됨.

---

## Test Suite

당신이 만약 테스트 모음을 자동화 했다면 다음과 같이 각 개발 환경에 맞는 테스트를 실행하고 싶을 것이다.

- **개발 환경**: Unit Test
- **스테이징 환경/QA**: 전체 테스트 모음
- **프로덕션 환경**: Smoke Test
