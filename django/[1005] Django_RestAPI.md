[TOC]

# 1005 _ Django: Rest API

## REST API

1. API Server

   - CLI
   - GUI
   - API

2. RESTful API

   - REST란? 자원과 주소의 지정 방법
   - REST 구성
     - 자원 URI (통합자원식별자) 
       - URL, URN이 URI안에 포함
       - http://localhost:3000/posts/3 (Scheme/Protocol  / Host / Port / Path)
     - 행위 HTTP Method(컨텐츠를 전송하기 위한 프로토콜(규약))
       - Stateless - 상태정보가 저장되지 않음
       - Connectless - 서버에 요청을 하고 응답을 한 이후에 연결은 끊어짐
       - HTTP Method
         - GET - 저장 리소스의 표시를 요청, 오직 데이터를 받기만 함
         - POST - 클라이언티 데이터를 서버로 보냄
         - PUT/PATCH - 서버로 보낸 데이터를 저장/지정 리소스의 부분만을 수정
         - DELETE - 지정 리소스를 삭제
     - 표현 Representations
       - 우선, JSON!

   - REST 중심규칙
     - 1. URI는 정보의 자원을 표현해야한다
       2. 자원에 대한 (어떠한)행위는 HTTP Method를 통해서 한다



## JSON

- JavaScript 객체 표기법
- 언어 독립적 / 변환이 쉽다
- 단순 문자열
- 데이터 덩어리
- Data Serving (JSON으로!)



=> 프로그래밍을 통해 요청에 RESTful한 방식으로 JOSN을 응답하는 서버를 만들자!!!!!



## Django REST Framework

|          | Django   | DRF             |
| -------- | -------- | --------------- |
| Response | HTML     | JSON            |
| Model    | ModelFom | ModelSeriallzer |

