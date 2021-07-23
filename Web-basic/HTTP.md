[김영한 - 모든 개발자를 위한 HTTP 웹 기본지식] 학습 내용 정리

# HTTP (HyperText Transfer Protocol)
web 상에서 정보를 주고 받을 수 있는 프로토콜.   
주로 HTML(HyperText Markup Language) 문서를 주고 받을 때 사용한다. 요즘은 거의 모든 것을 HTML에 담아서 전송이 가능하다.   
서버간의 통신에도 HTTP를 많이 사용한다.
TCP 통신만을 이용하여 직접하는 경우는 잘 없다. (게임 개발)   
클라이언트인 웹브라우저에서 HTTP 를 통하여 정보를 request하면, 서버에서 필요한 정보를 response 하여 사용자에게 전달한다.   
### HTTP 역사
- HTTP/0.9 1991년 : GET 메서드만 지원, HTTP 헤더가 없음   
- HTTP/1.0 1996년 : 메서드, 헤더 추가   
- HTTP/1.1 1997년 : 현재 가장 많이 사용되고 있다.
    - RFC2068(1997) -> RFC2616(1999) -> RFC7230-7235(2014)
- HTTP/2.0 2015년 : 성능 개선
- HTTP/3.0 현재진행중 : TCP 대신 UDP 사용. 성능 개선   

HTTP/2.0, HTTP/3.0 의 사용이 점점 늘어나고 있다.

# HTTP 특징
## 클라이언트 - 서버 구조
---
## 무상태 프로토콜 (Stateless)
서버가 클라이언트의 상태를 유지 하지 않음.   
클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다. -> 응답 서버를 쉽게 바꿀수 있다.   
- 서버 확장성이 높다(스케일 아웃)
- 클라이언트에 추가 데이터를 전송해야한다는 단점.
- 로그인이 필요없는 페이지   
### 상태유지
- 로그인한 사용자는 로그인 했다는 상태를 유지해야한다.
- 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태를 유지한다.
- 상태 유지는 최소한만 사용한다.
---
## 비연결성
- HTTP 메시지를 이용하지 않으면 매번 TCP/IP 연결을 새로 맺어야 한다.(3way handshake 시간 추가)
- HTML 뿐아니라 자바스크립트, 이미지, css등 수많은 자원을 함께 다운로드 해야한다.
- 지금은 HTTP 지속 연결 Persistent Connections로 문제를 해결
- HTTP/2, HTTP/3 에서 더 많은 최적화
- 최대한 stateless로 하도록 한다. -> 대용량 트래픽 대응
### 특징
- HTTP는 기본이 연결을 유지하지 않는다.
- 실제 서버에서 동시에 처리하는 요청은 수십개 이하이다.
- 서버 자원을 효율적을 사용할 수 있다.
---
## HTTP 메시지
- start-line
    - 요청 메시지
        - GET /search?q=hello&hl=ko HTTP/1.1   
        host: www.google.com
        - GET, POST, PUT, DELETE 와 같은 메서드
        - /절대경로[?쿼리]
        - HTTP version
    - 응답 메시지
        - HTTP/1.1 200 OK   
        content-Type: text/html;charset=UTF-8   
        content-Length: 123   
           
           body
        - HTTP version
        - 응답   
        200 : 성공
        400 : 클라이언트 요청 오류
        500 : 서버 내부 오류

- HTTP 헤더
    - field-name: OWS field-value OWS
        - field-name : 대소문자 구분 X
        - OWS : 공백 가능
        - field-value : 대소문자 구분
    - HTTP 전송에 필요한 모든 부가정보 포함   
    ex) 메시지 바디의 내용, 메시지 바디 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보
    - 표준 헤더가 너무 많다.
    - 필요시 임의의 헤더 추가 가능
- HTTP 바디
    - 실제 전송할 데이터
    - HTML 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능
    - 단순함, 확장 가능
---
## 단순함, 확장 가능
