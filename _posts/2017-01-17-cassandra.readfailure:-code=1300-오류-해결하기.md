---
layout: post
comments: true
title: "cassandra.ReadFailure: code=1300 오류 해결하기"
date: 2017-01-17 8:06:23
image: '/assets/img/'
description: 'Cassandra의 특정 테이블에 갑자가 접근이 안될 경우 확인하기.'
main-class: 'db'
color:
tags:
- db
- cassandra
categories:
twitter_text: 'cassandra.ReadFailure: code=1300 오류 해결하기'
introduction: 'Cassandra의 특정 테이블에 갑자가 접근이 안될 경우 확인하기.'
---

## 오류 내용
Cassandra 3.0을 이용하여 개발중인 서비스에서 갑자기 특정 테이블에 접속이 안되는 문제가 발생하였다.
그래서 `cqlsh`로 접속해서 해당 테이블을 조회 하니 다음과 같은 오류가 발생했다.

```
cassandra.ReadFailure: code=1300 [Replica(s) failed to execute read] 
message="Operation failed - received 0 responses and 1 failures"
info={'required_responses': 1, 'received_responses': 0, 'failures': 1,
'consistency': 'LOCAL_ONE'}
```

## 원인
도대체 왜 못 읽는 것일까 한참을 헤매다가 원인을 찾았다.
이는 지속적으로 삭제 처리가 진행 중인 개수가 설정의 `tombstone_failure_threshold`의 개수를 초과해서 발생하는 문제이다.
`tombstone_failure_threshold`를 확인하면 기본적으로 이상 아래와 같다.

```
$ cat /etc/cassandra/cassandra.yaml | grep tombstone_failure_threshold
tombstone_failure_threshold: 100000
```


`tombstone_failure_threshold`는 Cassandra의 분산 구조에서 발생할 수 있는 Consistency(일관성) 이슈를 위해서 고안된 기능이다.
삭제 처리 중인 레코드는 각 테이블의 `gc_grace_seconds`에 설정된 시간(TTL; Time To Live) 만큼 기다린 후에 Compaction이 진행될 때 완료된다.

문제가 발생한 테이블의 `gc_grace_seconds`을 확인하면 기본적으로 아래와 같다.

```
cqlsh:profile> DESC task_log;
	...
    AND comment = ''
    AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
    AND compression = {'chunk_length_in_kb': '64', 'class': 'org.apache.cassandra.io.compress.LZ4Compressor'}
    AND crc_check_chance = 1.0
    AND dclocal_read_repair_chance = 0.1
    AND default_time_to_live = 0
    AND gc_grace_seconds = 864000
	...
```

`gc_grace_seconds` = 864000 이면 10일 동안 삭제 레코드를 보관하겠다는 뜻이다. ;;
왜 이렇게 오랫동안 저장하는지는 위에서 언급한것 처럼 분산 DB 이기 때문인데 운영 중에 특정 Replica 노드에 장애가 발생 후 복구 후에도 데이터의 Consistency를 유지하기 위함이다.

## 해결

인터넷에서는 수동으로 Compaction을 진행 하라거나 여러가지 내용들이 있었지만 
해결은 의외로 간단하게 끝났다. ;; 개발 쪽에서는 Replica 노드가 없으므로 gc_grace_seconds을 0으로 지정해서 바로 지워지게 했다.

```
cqlsh:profile> ALTER TABLE task_log WITH gc_grace_seconds = 0;
```

## 다음 할 일
- Compaction Strategy 공부 및 정리.

## 참고
- [Compation](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/dml/dml_write_path_c.html#concept_ds_wt3_32w_zj__dml-compaction)
- [About deletes](http://docs.datastax.com/en/archived/cassandra/2.0/cassandra/dml/dml_about_deletes_c.html)
- [Reading error in cassandra](http://stackoverflow.com/questions/37114455/reading-error-in-cassandra)
