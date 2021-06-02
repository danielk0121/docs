# 프로그래밍 방식
- 절차적, 객체지향, 함수형
- 구조적: 절차적 방식에서 함수로 구조화 하는 방식, top-down 방식이라고도 함

# oop 4가지 특징
- 캡슐화: 부모자식, 멤버변수 메소드접근, 접근제어자(public, protected, private)
- 상속
- 추상화: 인터페이스
- 다향성: 오버로딩, 오버라이딩

# solid
```
S (SRP : Single Responsibility Principle)
단일 책임 원칙: 한 클래스 한 책임

O (OCP : Open/Closed Principle)
개방 폐쇄 원칙: 확장에 오픈, 변경에 클로즈

L (LSP : Liskov’s Substitution Principle)
리스코브 치환 법칙 : 다향성
프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서
하위 타입의 인스턴스로 바꿀 수 있어야 한다.

I (ISP : Interface Segregation Principle)
인터페이스 분리 법칙: 추상화
특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.

D (DIP : Dependency Inversion Principle)
의존 역전 법칙: 추상화에 의존한다, DI
추상화에 의존한다. 구체화에 의존하면 안된다.
```

# http 1.1 주요 추가 사항
- Connection: Keep-Alive
- 청크 응답 지원
- OPTIONS, PUT, DELETE, TRACE 추가

# 디비, 데이터 무결성 제약조건, ACID
- A, 원자성: Tr은 분해가 불가능한 최소단위로, 연산이 all or nothing 되어야됨, commit, rollback
- C: 일관성: Tr 이후 언제나 모순없이 일관성 있는 상태 유지 (무결설 제약조건 처리)
- I: 고립성: Tr 실행 중, 다른 Tr이 연산 중간 결과를 접근 할 수 없음
- D: 영속성: 성공된 tr 결과는 영구적으로 저장됨
- 무결성 제약조건: pk, fk, check 등

# 정규화 목적
- 중복 제거
- "이상현상" 방지 (CUD 로 인한)
- 온라인 거래 시스템 같은 OLTP(OnLine Transaction Processing) DB는
  CRUD 빈번하므로 정규화가 적절
- 분석 리포트 같은 OLAP(OnLine Analytical Processing) DB는
  연산의 속도를 위해 반정규화가 적절

# 기타
- IoC: Inversion Of Control
- DI: Dependency Injection
- POJO: Plain Old java Ojbect
- Bean: POJO로, 스프링 컨테이너에 생성된 객체
- VO: Value Object
- DTO: Data Transfer Object
- REST: REpresental(대변하다, 대표하다) State Transfer
  - 자원을 표현하여 상태를 전달한다는 뜻
- HTTPS: HTTP + SSL(Secure Sockets Layer)
- LRU(Least Recently Used): 가장 오랫동안 사용하지 않음을 기준
- LFU(Least Frequently Used): 참조 횟수 기준
- ETL : 추출(Extract), 변환(Transform), 적재(Load)
- XSS: cross-site scripting
- CORS: Cross Origin Resource Sharing

# TCP UDP
- 혼잡제어: 네트워크 내 패킷 수가 넘치지 않도록 방지
- 흐름제어: 수신자가 윈도우 크기 값을 통해 수신량을 정할 수 있음
- 순서보장
- 4-way handshaking: syn, ack, FIN

# 응집도(Cohesion) 결합도(Coupling)
- 응집도: 동일기능이 하나의 모듈에 포함된 정도
- 결합도: 다른 모듈간의 의존성

# CISC, RISC
- CISC(Complex Instruction Set Computer)
  - 다수 명령어, 대다수의 프로세서가 CISC 모델로 구축(범용적)
  - 초기모델
- RISC(Reduced Instruction Set Computer)
  - 축소 명령어 세트 컴퓨터
  - 적은 명령어, 컴파일러 구현이 단순
  - CISC 개선으로 특수목적 CPU

# 트랜젝션 격리수준
- https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/
- READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE
- level 0, 1, 2, 3
- READ UNCOMMITTED: 어떤 트랜잭션의 변경내용이 COMMIT이나 ROLLBACK과 상관없이 다른 트랜잭션에서 보여진다.
- READ COMMITTED: 어떤 트랜잭션의 변경 내용이 COMMIT 되어야만 다른 트랜잭션에서 조회할 수 있다.
  - 이는 하나의 트랜잭션내에서 똑같은 SELECT를 수행했을 경우 항상 같은 결과를 반환해야 한다는 REPEATABLE READ 정합성에 어긋나는 것이다. 금전적인 처리와 연결되어 있다면 문제가 발생할 수 있다. 예를 들어 여러 트랜잭션에서 입금/출금 처리가 계속 진행되는 트랜잭션들이 있고
오늘의 입금 총 합을 보여주는 트랜잭션이 있다고하면, 총합을 계산하는 SELECT 쿼리는 실행될 때 마다 다른 결과값을 가져올 것이다.
  - update, insert 이후 select 에서 발생할 수 있다
  - PHANTOM READ: insert 에서 발생
  - update, undo 때문에 발생
  - MVCC (Multi Version Concurrency Control)
- REPEATABLE READ: 트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리수준이다. 자신의 트랜잭션 번호보다 낮은 트랜잭션 번호에서 변경된(+커밋된) 것만 보게 되는 것이다.
- SERIALIZABLE: InnoDB에서 기본적으로 SELECT 작업은 아무런 잠금을 걸지않고 동작하는데, 격리수준이 SERIALIZABLE일 경우 "읽기 작업에도 공유 잠금을 설정하게 되고", 이러면 동시에 다른 트랜잭션에서 이 레코드를 변경하지 못하게 된다.
  - SELECT 문장이 사용하는 모든 데이터에 shared lock
  - MVCC 사용안함
