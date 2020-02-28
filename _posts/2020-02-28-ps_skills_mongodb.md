---
title: "몽고 DB 데이터 증가에 따른 관리 방법"
description: "증가하는 몽고 DB 데이터에 대한 관리하는 방법을 알아보자"
date: 2020-02-28 18:00:00
tags: [DB]
category: 기술
author_profile: false
---
## 데이터베이스의 등장배경과 필요성
### 데이터베이스 등장배경
- 네트워크가 활성화 되며 서로 멀리 떨어진 공간에서도 컴퓨터라는 매개체를 통하여 여러사람들이 정보를 공유하기 위한 수단으로 데이터베이스가 등장하게 되었다.

### 데이터베이스 필요성
컴퓨터가 등장하기 이전의 시대에는 정보, 즉 의사결정에 필요한 지식 및 기록 증거등을 문서를 통하여 관리했다. 컴퓨터가 등장함으로써 Excel 등의 편집프로그램과 저장공간을 활용하여 편리하게 정보를 정리하고 보관하고 관리 할 수 있게 되었다.

컴퓨터가 등장하기 이전 시대에는 정보를 활용하기 위한 용도로 어딘가에 적어서 기록해 두고 특정공간에 분류해두거나 관리하는 것처럼 데이터베이스도 마찬가지로 컴퓨터의 저장공간에 기록해 두고 시간이 지남에 따라 불필요한 정보는 삭제하고 정리하고 빠르게 찾고 활용할 수 있도록 하는 작업이 주기적으로 필요하다.

Mongo DB도 마찬가지로 시간이 지남에 따라 정보가 누적되어 추가적인 저장공간이 필요하거나 확보해야 하는 경우를 대비하여 Mongo DB의 데이터 삭제 및 관리하는 방법에 대해서 알아보자.

### 저장공간 확보를 목적으로 삭제 명령을 실행하여 데이터 삭제하기

RDBMS와 비교해보면 테이블 내의 로우데이터를 삭제하는 DELETE 명령과 REMOVE 명령은 동일한 역할을 수행하고 drop 명령은 테이블을 삭제하는 명령과 동일하고 동작한다.

IBM사의 DB2의 경우 설정에 따라 DELETE 명령을 수행하면 물리적인 디스크가 확보되지만 몽고 DB는에서 remove 명령을 사용하여 Document를 삭제하거나 Collection을 drop 명령을 수정하여도 실제 사용중인 디스크의 물리적인 가용 공간은 확보되지 않는다.

몽고 DB에서 데이터를 삭제하더라도 실제 사용 가능한 디스크 용량이 그대로인 이유는 몽고 DB에서 디스크를 미리 할당해서 사용하는 방식인 스토리지 엔진 방식을 사용하기 때문이다. 스토리지 엔진은 디스크에서 데이터를 읽어오고 저장하는 역할을 최적으로 수행 될 수 있도록 지원하는 역할로서 데이터베이스의 일부로 메모리와 디스크 모두에서 데이터가 저장되는 방식을 사용하는데 이는 더 나은 성능을 제공하고 다른 스토리지 엔진은 쓰기 작업에 대한 높은 처리량을 지원할 수 있기 때문이다.

몽고 DB에서 제공하는 스토리지 엔진은 다음과 같은 스토리지 엔진을 제공하는데 좀 더 자세한 내용이 궁금하신 분들은 아래의 내용을 검색하여 찾아보시면 도움이 될 것이다.

* MMAP v1
* WiredTiger
* In-Memory
* RocksDB
* TokuDB

![storage](https://user-images.githubusercontent.com/61443040/75522204-c063c600-5a4c-11ea-8a03-91a040f8af71.png)

### 몽고 DB의 실제 물리적인 디스크 가용공간을 확보하는 방법

1. db.repairDatabase(): 백업 세트를 복제하여 재구성하는 방식
- 장점: 실제 물리적인 디스크 가용공간이 확보되며, DB 손상 상태를 복구 할 수 있음
- 단점: 현재 사용중인 디스크 공간의 두배의 가용 공간이 필요함. 실행 시간이 길며 lock이 걸림(실행 시간동안 DB 사용불가)

2. 특정 DB의 각 collection마다 compact 명령 실행
- 장점: collection 대상으로 실행하기 때문에 repairDatabase보다는 훨씬 적은 디스크 용량을 사용
- 단점: 실행 후 실제 디스크 용량은 늘지 않고, 이미 할당된 공간의 파편화를 정리하여 사용 가능하게 만들어 줌
→ 따라서 디스크 용량이 충분하지 않은 경우엔 실행할 수 없다!! 2GB 정도의 데이터 용량을 사용함

## 가용공간 관리 방법
1. 서버에 접속하여 아래와 같이 명령을 입력하여 대상 DB로 이동한다.
```
[centos@dashboard-dev ~]$ mongo
MongoDB shell version: 2.6.12
connecting to: test
Server has startup warnings:
2019-12-26T19:32:41.019+0900 [initandlisten]
2019-12-26T19:32:41.019+0900 [initandlisten] ** WARNING: Readahead for /storage/mongodata is set to 4096KB
2019-12-26T19:32:41.019+0900 [initandlisten] **          We suggest setting it to 256KB (512 sectors) or less
2019-12-26T19:32:41.019+0900 [initandlisten] **          http://dochub.mongodb.org/core/readahead
>use [데이터베이스명]
```

2. 현재 DB의 인스턴스 스토리지에 대한 정보를 확인한다.
```
> db.stats()
{
        "db" : "[DB이름]",
        "collections" : 29,
        "objects" : 27162297,
        "avgObjSize" : 1006.4396159131902,
        "dataSize" : 27337211760,
        "storageSize" : 30315884400,
        "numExtents" : 176,
        "indexes" : 47,
        "indexSize" : 13262158784,
        "fileSize" : 83644907520,
        "nsSizeMB" : 16,
        "dataFileVersion" : {
                "major" : 4,
                "minor" : 6
        },
        "extentFreeList" : {
                "num" : 51,
                "totalSize" : 34989301680
        },
        "ok" : 1
}
```
- dbStats.collections: 해당 데이터베이스의 모음 수를 포함
- dbStats.objects: 모든 컬렉션의 데이터베이스에 있는 오브젝트 수 (즉, Document) 의 수를 포함
- dbStats.avgObjSize: 각 Document 평균 크기 바이트 기준으로 Document 수로 나눈 값
- dbStats.dataSize: 데이터베이스에 보유 된 압축되지 않은 데이터의 총 크기
- dbStats.storageSize: 이 데이터베이스에서 Document 저장을 위해 컬렉션에 할당 된 총 공간
- dbStats.numExtents:모든 컬렉션에 대한 데이터베이스의 익스텐트 수
- dbStats.indexes: 데이터베이스의 모든 콜렉션에 대한 총 인덱스 수를 포함
- dbStats.indexSize: 데이터베이스에서 작성된 모든 인덱스의 총 크기
- dbStats.scaleFactor: scale명령에 의해 사용되는 값. 정수가 아닌 스케일 팩터를 지정한 경우 MongoDB는 지정된 팩터의 정수 부분을 사용한다. 예를 들어 스케일 팩터를으로 지정하면 1023.999MongoDB가 1023스케일 팩터로 사용함
- dbStats.fsTotalSize: MongoDB가 데이터를 저장하는 파일 시스템의 모든 디스크 용량의 총 크기

3. 서비스 상황에 맞는 방법을 선택한다.

★ Collection 생성 시 최대 크기와 Document 개수를 옵션으로 설정
 - 최대 크기까지 도달 시 자동으로 오래된 데이터를 삭제 후 신규 데이터를 삽입함
 - Size 단위는 Byte 단위
 - 생성하는 시간 동안 잠금 상태를 유지함
 ```
 // Collection 별 최대 사이즈를 지정한다.
db.createCollection( "log", { capped: true, size: 100000 } )
db.createCollection("log", { capped : true, size : 5242880, max : 5000 } )

// Capped Collection 조회
db.cappedCollection.find().sort( { $natural: -1 } )
db.collection.isCapped()

//  생성한 Collection Capped
db.runCommand({"convertToCapped": "mycoll", size: 100000});
 ```

★mongod --smallfiles 옵션: 파일 할당 크기를 기본 64MB~2GB에서 16MB~512MB로 설정
 - 들어오는 데이터 크기가 작을 경우 DB 크기 증가 속도 감소
 - 파일 할당이 빈번해져서 속도가 느려질 수 있음
 - 성능상 속도 감소의 단점이 있으므로 관련 링크 첨부함
 - 관련 주소 링크 : https://docs.mongodb.com/manual/reference/program/mongod/

★ TTL Collection : TTL 수집은 특정 기간이 지나면 문서가 자동으로 삭제됨
 - 백그라운드로 삭제작업이 수행되며 작업이 수행되기 이전에는 데이터가 남아있을수 있음
 - 색인화된 필드는 반드시 날짜 유형이여야 함
 - usePowerOf2Sizes 설정 시 특정 기간 동안의 데이터를 보존하는 식의 컬렉션 같은 경우 storageSize 재사용률을 크게 높여줌

 ```
// TTL 인덱스 생성
// 지정된 시간 (초)보다 오래된 경우 컬렉션 에서 문서를 자동으로 삭제
db.log_events.createIndex( { "createdAt": 1 }, { expireAfterSeconds: 3600 } )

// 데이터 업데이트
db.log_events.insert( {
   "createdAt": new Date(),
   "logEvent": 2,
   "logMessage": "Success!"
} )

// 특정 시계시간 유형으로 지정
db.log_events.createIndex( { "expireAt": 1 }, { expireAfterSeconds: 0 } )

// 데이터생성
db.log_events.insert( {
   "expireAt": new Date('July 22, 2013 14:00:00'),
   "logEvent": 2,
   "logMessage": "Success!"
} )
 ```

★ repairDatabase
repairDatabase()는 명령어는 내부적으로 "mongoexport -> tmp생성 -> temp에 mongoimport -> 기존 disk 삭제 -> temp를 disk로 이전" 따라서 temp공간을 위한 여유공간이 필요하다.
300GB의 경우, 5시간이 소요 , 500GB의 경우 8시간 이상 소요되며 작업 시간이 길다.
(실제 운영환경이라면 기본 몇백GB는 기본으로 쌓여있는 상태에서 repairDatabase()를 수행하야 하는데, 이럴경우 수시간동안의 서비스 중지가 불가피하다. 무중단 서비스라면 이러한 부분을 반드시 고려해야 한다.)

```
db.repairDatabase()
```

### 결론
실제 Mongo DB에서 서버의 물리적인 디스크 공간을 확보하는 방법은 repairDatabase 명령을 수행하는 방법 뿐이다. 나머지 방법들은 할당된 영영을 재사용하는 방식임.

물리적인 디스크공간이 부족하여 실제 데이터 파일을 삭제하는 경우 아래와 같은 문제들이 발생한다.
- 컬렉션 객체가 삭제되지 않음.
- 인덱스 정리가 되지 않음.

결론은 DB 구축 시 데이터 증가량을 충분이 고려하여 알맞는 방법을 사용하는것을 권장한다.
