[TOC]

# 1116_Vue : Vue + API 서버 활용

## Server & Client

### Server(Vue.js)

- 서버는 클라이언트에게 네트워크를 통해 정보나 서비스를 제공
- **정보 제공**



### Client(Vue.js)

- 서버가 맞는 서비스를 요청하고, 서비스 요청을 위해 필요한 인자를 서버가 원하는 방식에 맞게 제공하며, 사용자에게 적절한 방식으로 표현하는 기능을 가진 프로그램이나 시스템

1. 서버에 맞는 요청을 제공
   - Client(POSTMAN) -> Server(django REST framework)
   - ​                       <- (JSON) <-

2. 서버의 응답을 사용자에게 표현

   - Client -> Server

   -   <- (JSON) <-

- **정보 요청 & 표현**





## CORS (Cross-Origin Resource Sharing)

### CORS - What?

- CORS (Cross-Origin Resource Sharing) - 교차 출처 자원 공유
  - 다른 출처(Origin)에서 온 리소스를 공유하는 행위
- SOP (Same-Origin Policy) - 동일 출처 정책
  - 같은 출처(Origin)에서만 리소스를 공유

- CORS (Cross-Origin Resource Sharing) Policy - 교차 출처 자원 공유 정책
  - 다른 출처(Origin)에서 온 리소스를 공유하는 것에 대한 정책 -> SOP의 예외 사항



- 출처의 정의 : 두 URL의 프로토콜, 포트(명시한 경우), 호스트가 같아야 동일한 출처라고 한다



- CORS는 추가 HTTP 헤더를 사용하여, 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
- 보안상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP요청을 제한.
- 예를 들어, XMLHttpRequest와 Fetch API는 동일 출처 정책을 따름
- 즉, 이 API를 사용하는 앱 애플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불려오려면 그 출처에서 올바른 CORS헤더를 포함한 응답을 반환해야함

- 교차 출처 접근 허용하기
  - 서버에서 지정할 수 있는 방법



즉!

- **" 브라우저 (+웹 어플리케이션) 보호 "**
  - 요청에 대한 응답으로 받는 자원에 대한 최소한의 검증
  - 서버는 정상적으로 응답하지만 브라우저에서 받지 않고 차단



### CORS - How?

**Client** / Origin : https://lab.ssafy.com

**Server** / Access-Control-Allow-Origin : https://lab.ssafy.com or *

-> Access-Control-Allow-Origin 주의해야하기때문에 명시하는 것이 좋음





## Authentication & Authorization

### What is authentication?

- who are you?

### What is authorization?

- what can i do?



### Authentication & Authorization

- Authentication (인증)
  - 401
  - **자신이라고 주장하는 유저 확인**
  - Credentials(비밀번호, 얼굴인식) 검증
  - django => 게시판 서비스 로그인
  - 인증 이후에 획득하는 권한 (생성, 수정, 삭제)
- Authorization (권한/허가)
  - 403
  - **유저가 자원에 접근할 수 있는지 여부 확인**
  - 규칙/규정에 의해 접근할 수 있는지 확인
  - django => 일반 유저 vs 관리자 유저
  - 인증 이후에 부여되는 권한
    - 예시 - 로그인 후 글 작성 여부





## Session / Token Based Authentication

### Token(JWT)

- Client 에서 Server에 요청하면 
- 서버가 응답! JWT발급!
- 그럼 Client가 JWT를 local storage에 저장
- 다음번 요청에 JWT담아서 준다
- 그럼 서버가 토큰 검증 완료 -> 로그인

|                         | Session         | JWT                  |
| ----------------------- | --------------- | -------------------- |
| 인증 수단의 저장 위치   | Server          | Client               |
| 인증 수단의 정보 민감성 | Low(session id) | High(self-contained) |
| 유효 기간               | Y               | Y                    |

