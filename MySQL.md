# MySQL

- 서버엔진 : 클라이언트의 요청을 받아 SQL을 처리하는 DB 자체의 기능적인 역할

- 스토리지 엔진 : 서버 엔진이 필요한 데이터를 물리 장치에서 가져오는 역할을 수행

![images_ggomjae_post_bdf47a05-b5e3-4577-9cea-b36a086da38b_image (1)](https://user-images.githubusercontent.com/103401813/179400754-50b5a2a0-34b2-4d6f-9070-a36c2e837531.png)

------

## 서버 엔진

DB가 SQL을 이해할 수 있도록 쿼리를 재구성하는 쿼리 파싱 또는 스토리지 엔진에 데이터를 요청하는 업무 담당

- 파싱 : 어떤 페이지(문서, html 등)에서 내가 원하는 데이터를 특정 패턴이나 순서로 추출해 가공하는 것

**스토리지 엔진에서 받아온 데이터를 사용자 요청에 맞게 처리하고 접근 제어, 쿼리 캐시, 옵티마이저 등의 역할을 수행**

→ 사용자와 mysql 사이에서 발생하는 데이터 처리 프로세스를 전부 담당

- ex) Join, Group By, Order By, Funtion/Procedure, Trigger

------

## 스토리지 엔진

물리적인 저장장치에서 데이터를 읽어오는 역할

- 플러그인 처럼 작동하여 여러 종류의 스토리지 엔진을 설치하여 바로 사용 가능
  - ex) InnoDB, MylSAM 등
    - InnoDB를 대중적으로 사용
- 확장성과 유연함이 뛰어나다.

### InnoDB는 Mysql에서 유일하게 트랜잭션을 지원한다.

- 트랜잭션 : 쪼갤 수 없는 업무 처리의 최소 단위
- 인덱스와 데이터를 모두 메모리에 올려 MyISAM과 성능 차이가 있다.
- 클러스터 인덱스 사용 가능
  - 테이블당 한 개만 생성 가능
  - 행 데이터를 인덱스로 지정한 열에 맞춰 자동 정렬
  - 내용 자체가 순서대로 정렬되어 있다.
  - 루트 페이지와 리프 페이지(데이터 그 자체)로 구성되어 있다.

------

## MySQL의 데이터 처리

병렬 처리를 하지 않는다. 모든 SQL을 단일 코어에서 처리한다.

- 단위 처리량이 좋은 CPU로 Scal-Up을 하는 것이 훨씬 좋다.
  - Scal-Up : 하나의 서버의 기능들을 업그레이드 하는 것

**MySQL의 Join은 항상 Nested Loop Join알고리즘으로 처리**

- Nested Loop Join : 2개 이상의 테이블에서 하나의 집합을 기준으로 순차적으로 상대방 레코드를 결합하여 원하는 결과르르 조합하는 조인 방식
  - 처리할 데이터가 적어지면 수행 속도가 빠르지만 테이블 하나라도 연산해야 할 데이터가 많아지면 쿼리 효율이 떨어진다.
