# Django Model

### 1. Model

- 데이터에 대한 단 하나의 정보 소스
- 저장된 데이터 베이스의 구조(layout)를 의미
- 사용자가 저장하는 데이터들의 필수적인 필드들과 동작들을 포함
- django는 model 을 통해 데이터에 접속하고 관리
- 일반적으로 각각의 model은 하나의 데이터 베이스 데이블에 매핑

### 2. Database

- 데이터베이스(DB) : 체계화된 데이터의 모임
- 쿼리(Query) : 데이터를 조회하기 위한 명령어, 조건에 맞는 데이터를 추출하거나 조작하는 명령어

### 3. Database의 기본 구조

- 스키마(schema) : 데이터베이스의 구조와 제약조건(자료의 구조, 표현 방법, 관계)에 관련한 전반적인 명세를 기술한 것
- 테이블(table) : 열(컬럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합. SQL 데이터 베이스에서는 테이블을 관계라고도 한다. 
- 열(column), 컬럼: 각 열에선는 고유한 데이터 형식이 지정된다. (integer, text, null 등)
- 행(row), 레코드 : 테이블의 데이터는 행에 저장된다. 
- PK(기본키) : 각 행(레코드)의 고유값으로 Primary Key로 불린다. 반드시 설정해야하며, 데이터베이스 관리 및 관계 설정시 주요하게 활용된다. 

### 4. ORM

> "Object-Relational-Mapping"은 객체지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템간에 (Django-SQL)데이터를 변환하는 프로그래밍 기술이다. 이것은 프로그래밍 언어에서 사용할 수 있는 '가상객체 데이터 베이스'를 만들어 사용한다. 

- 장점 : SQL 을 잘 알지 못해도 DB 조작 가능, 절차적 접근이 아닌 객체지향적 접근으로 인한 높은 생산성
- 단점 : ORM 만으로 완전 서비스를 구현하기 어려운 경우가 있음

**현대 웹 프레임워크의 요점은 웹 개발의 속도를 높이는 것(생산성)**

**우리는 DB를 객체(object)로 조작하기 위해 ORM을 사용한다. **

### 5. Field Type

#### 1) CharField()

- 길이의 제한이 있는 문자열을 넣을때 사용
- max_length가 필수 인자 (ex.CharField(max_length=None))
- 필드의 최대 길이, 데이터 베이스와 django의 유효성 검사

#### 2) TextField()

- 글자의 수가 많을 때 사용

#### 3) DateTimeField()

- 최초 생성 일자 : `auto_now_add=True`
  - django ORM 이 최초 데이터 입력시에만 현재 날짜와 시간으로 갱신
  - 테이블에 어떤 데이터를 최초로 넣을 때 
- 최종 수정 일자 : 

### 6. Migrations

- django가 model에 생긴 변화(필드를 추가했다던가 모델을 삭제했다던가 등)을 반영하는 방법
- Migrations Commands
  - `makemigrations` : model을 변경한 것에 기반한 새로운 마이그레이션을 만들 때 사용
  - `migrate` : 마이그레이션을 DB에 반영하기 위해 사용
  - `sqlmigrate` : 마이그레이션에 대한 SQL 구문을 보기 위해 사용
  - `showmigrations`: 마이그레이션 파일들의 migrate 여부를 학인하기 위한 명령어

- model의 중요 3단계 

  1) models.py : 변경사항 발생 

  2) makemigrations : 마이그레이션 만들기

  3) magrate : DB에 적용

### 7. DB API

- django 가 기본적으로 ORM 을 제공함에 따른 것으로 DB를 편하게 조작할 수 있도록 도와줌
- Model을 만들면 django 는 객체들을 만들고 읽고 수정하고 지울수 있는 database-abstract API를 자동으로 만듦
- database-abstract API 혹은 datadabe-access API라고 함.
- **Manager**
  - django 모델에 데이터베이스 query 작업이 제공되는 인터페이스
  - 기본적으로 모든 장고 모델 클래스에 objects 라고 Manager를 추가
- **QuerySet**
  - 데이터 베이스로부터 전달받은 객체 목록
  - queryset 안의 객체는 0,1 개 혹은 여러 개일 수 있다.
  - 데이터 베이스로부터 조회, 필터, 정렬 등 수행할 수 있다.
- **QuerySet API**
  - 데이터 베이스 조작으 ㄹ위한 다양한 QuerySet API method들은 해당 공식 문서를 반드시 참고 