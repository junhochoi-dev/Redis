# REDIS


> REDIS(Remote Dictionary Server)

- 다수의 서버를 사용하는 분산 환경의 서버가 공통으로 사용할 수 있는 원격 해시 테이블 서버
- Open Source In-Memory Data Store written in ANSI-C

1. In-Memory
   - 모든 데이터를 RAM에 저장 (백업/스냅샷을 일부 사용)
2. Single Threaded
   - 단일 Thread에서 모든 Task 처리
     - Multi-Thread는 프로그램의 복잡성을 증가시킨다
3. Cluster Mode
   - 다중 노드에 데이터를 분산 저장하여 안정성 & 고가용성 제공
4. Persistence
   - RDB(Redis Database) + AOF(Append only File) 통해 영속성 옵션 제공
   - AOF : 데이터베이스 시스템에서 사용되는 하나의 영속성 유지 방법으로 명령이 실행될 때마다 그 명령을 순차적으로 파일에 기록하는 방식
   - 영속성 : 데이터가 생성된 프로그램이나 시스템을 종료하거나 중단해도 데이터가 계속해서 유지되는 특성
5. Pub/Sub (Publish/Subscribe)
   - Pub/Sub 패턴을 지원하여 손쉬운 어플리케이션 개발(e.g 채팅, 알림 등)

> REDIS의 장점

- 높은 성능
  - 모든 데이터를 메모리에 저장하기 때문에 매우 빠른 읽기/쓰기 속도 보장
- Data Type 지원
  - Redis에서 지원하는 Data type을 잘 활용하여 다양한 기능 구현
- 클라이언트 라이브러리
  - Python, Java, JavaScript 등 다양한 언어로 작성된 클라이언트 라이브러리 지원
- 다양한 사례 / 강한 커뮤니티
  - Redis를 활용하여 비슷한 문제를 해결한 사례가 많고, 커뮤니티 도움 받기 쉬움

> REDIS의 사례

- Caching
  - 임시 비밀번호(One-Time Password)
  - 로그인 세션(Session)
- Rate Limiter
  - 서버에서 특정 API에 대한 요청 회수를 제한하기 위한 기술
  - Fixed-Window / Sliding-Window Rate Limiter(비율 계산기)
- Message Broker
  - 메시지 큐(Message Queue)
  - 다양한 서비스 간의 커플링(Coupling)을 줄일 수 있다
  - Coupling : 소프트웨어 시스템에서 한 모듈, 클래스 또는 컴포넌트가 다른 모듈, 클래스 또는 컴포넌트와 얼마나 강하게 연결되어 있는지
    - 서비스 간의 커플링을 줄인다는 것은 각각의 서비스가 서로에게 영향을 미치지 않고 독립적으로 동작할 수 있도록 설계하는 것을 의미
- 실시간 분석 / 계산
  - 순위표(Rank / Leaderboard)
  - 반경 탐색(Geofencing)
  - 방문자 수 계산(Visitors Count)
- 실시간 채팅
  - Pub/Sub 패턴

> REDIS Persistence

- Persistence(영속성)
    - REDIS는 주로 캐시로 사용되지만 데이터 영속성을 위한 옵션 제공
    - 캐시로 사용되기 때문에 기본적으로 손실되어도 무방한 데이터를 기록
    - SSD와 같은 영구적인 저장 장치에 데이터 저장
- RDB(Redis Database)
  - Point-in-time SnapShot(특정시간 스냅샷 생성) → 재난 복구(Disaster Recovery) 또는 복제에 주로 사용
  - 스냅샷은 특정 시간 간격 또는 조건이 충족될 때 현재 메모리 상태를 디스크에 저장하는 방식
  - 일부 데이터 유실의 위험이 있고, 스냅샷 생성 중 클라이언트 요청 지연 발생
- AOF(Append Only File)
  - Redis에 적용되는 Write 작업을 모두 log로 저장
  - 데이터 유실의 위험이 적지만, 재난 복구시 Write 작업을 다시 적용하기 때문에 RDB 보다 느림 
  - AOF는 Redis에 수행된 모든 쓰기 명령을 파일에 기록하는 방식
  - 명령이 실행될 때마다 파일에 쓰여지며, 시스템이 재시작될 때 이 파일을 읽어서 데이터를 복구


> Caching

- 캐싱(Caching)
  - 데이터를 빠르게 읽고 처리하기 위해 임시로 저장하는 기술
  - 계산된 값을 임시로 저장해두고, 동일한 계산 / 요청 발생시 다시 계산하지 않고 저장된 값 바로 사용
- 캐시(Cache) = 임시 저장소
- 사용 사례
  - CPU 캐시
    - CPU와 RAM의 속도 차이로 발생하는 지연을 줄이기 위해 L1, L2, L3 캐시 사용 
  - 웹 브라우저 캐싱
    - 웹 브라우저가 웹 페이지 데이터를 로컬 저장소에 저장하여 해당 페이지 재방문시 사용 
  - DNS 캐싱
    - 이전에 조회한 도메인 이름과 해당하는 IP 주소를 저장하여 재요청시 사용
  - 데이터베이스 캐싱
    - 데이터베이스 조회나 계산 결과를 저장하여 재요청시 사용
  - CDN
    - 원본 서버의 컨텐츠를 PoP 서버에 저장하여 사용자와 가까운 서버에서 요청 처리
    - CDN(Content Delivery Network) : 여러 국가나 지역에 있는 다양한 서버들을 사용해서 웹페이지의 내용을 더 빨리 전달하는 기술
    - 만약 현재 미국에 있다면, CDN은 여러 국가에 있는 서버 중에서 가장 가까운 곳의 서버를 사용해서 웹페이지를 더 빨리 불러올 수 있게 도와준다
  - 어플리케이션 캐싱
    - 어플리케이션에서 데이터나 계산 결과를 캐싱하여 반복적 작업

> Cache Hit & Cache Miss

- Cache Hit
  - 캐시가 존재하여 리턴함
- Cache Miss
  - 캐시가 존재하지 않아 리턴되지 않음

> Cache-Aside pattern 

Cache에 데이터 확인
  - 있으면 OK (Cache Hit)
  - 없으면 Database에 확인 (Cache Miss)


  