---
layout: post
title: "cassandra.ReadFailure: code=1300 오류 해결하기"
date: 2017-01-17 8:06:23
image: '/assets/img/'
description: Cassandra에 갑자가 접속이 안될 경우 확인하기.
main-class: "Cassandra"
color:
tags:
- db
- cassandra
categories:
twitter_text: "cassandra.ReadFailure: code=1300 오류 해결"
introduction: "Cassandra에 갑자가 접속이 안될 경우 확인하기."
---

개발 중인 프로파일 서버에서 갑자기 카산드라 접속이 안되기 시작한다.
그래서 cqlsh 로 직접 접속해서 해당 KEYSPACE의 TABLE을 조회 하니 다음과 같은 오류가 발생했다.


이는 저장되어 있는 tombstones의 크키가 지정한 갯수를 초과 했기 때문에 발생한 문제이다.

문제가 발생하는 해당 테이블의 설정 중에 ALTER TABLE [테이블명] WITH GC_GRACE_SECONDS = 0; 으로 변경하면 된다.
단 이는 

http://stackoverflow.com/questions/37114455/reading-error-in-cassandra



About tombstone
http://thelastpickle.com/blog/2016/07/27/about-deletes-and-tombstones.html