[김영한 - 모든 개발자를 위한 HTTP 웹 기본지식] 학습 내용 정리

# HTTP 헤더
## 일반 헤더
- 과거에는 엔티티라고 쓰였고 현재는 표현(Representation)이라 한다.
- 표현 = 표현 메타 데이터 + 표현 데이터
- 메시지 본문을 통해 표현 데이터 전달. 메시지 본문 = 페이로드
- 표현은 요청이나 응답에서 전달할 실제 데이터. 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공 (데이터 유형, 데이터 길이 , 압축 정보)

## 1. 표현
- Content-Type : 표현 데이터 형식. text/html;charset=utf-8, application/json.
- Content-Encoding : 표현 데이터 압축 방식. gzip, deflate, identify(미압축).
- Content-Language : 표현 데이터의 자연 언어. ko, en, en-US.
- Content-Length : 표현 데이터 길이. 바이트 단위. Transfer-Encoding을 사용하면 사용하면 안된다.
- 표현 헤더는 전송. 응답 둘다 사용.

## 2. 콘텐츠 협상
- 클라이언트가 선호하는 표현 요청
- Accept : 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
- Accept-Language : 클라이언트가 선호하는 자연 언어
- 형상 헤더는 요청시에만 사용.
- Quality values(q) 값사용
- 0-1, 클수록 높은 우선순위. 생략시 1   
ex) Accept: text/*, text/plain, text/plain;format=flowed

## 3. 전송 방식
- Transfer-Encoding
- Range, Content-Range
- 단순 전송 : Content-Length
- 압축 전송 : Content-Encoding
- 분할 전송 : Transfer-Encoding; chunked
- 범위 전송 : Range.Content-Range

## 4. 일반 정보
- Form
    - 유저 에이전트의 이이베일 정보. 사용x
    - 검색 엔진 같은 곳에서 주로 사용
- Referer
    - 이전 웹페이지 경로
    - 현제 요청된 페이지의 이전 웹페이지 주소
    - A->B로 이동하는 경우 B 요청 할 때, Referer: A 를 포함해서 요청
    - Referer 를 통해 유입 경로 분석 가능
- User-Agent
    - 클라이언트의 애플리케이션 정보(웹브라우저 정보 등)
    - 통계 정보
    - 어떤 종류의 브라우저에서 장애가 발생하는지 파악가능
    - 요청에 사용
- Server
    - 요청을 처리하는 ORIGIN서버의 소프트웨어 정보   
    Serve: nginx, Server: Apache/2.2.22(Debian)
    - 응답에 사용
- Date
    - 메시지가 발생한 날짜와 시간
    - 응답에 사용

## 5. 특별한 정보
- Host
    - 요청한 호스트 정보(도메인)
    - 요청시 사용
    - 필수 -> 하나의 서버가 여러 도메인을 처리해야 할때, 하나의 IP주소에 여러 도메인이 적용되어 있을 때 식별할 있다.
- Location
    - 웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면 Location 위치로 자동이동(리다이렉트)
    - 201 (Created) : Location 값은 요청에 의해 생성된 리소스 URI
    - 3xx (Redirect) : Location 값은 요청을 자동으로 리다이렉션하기 위한 대상 리소스를 가리킴
- Allow
    - 허용 가능한 HTTP 메서드
    - 405 (Method Not Allow) 에 응답에 포함
    - Allow: GET, HEAD, PUT
- Retry-After
    - 유저 에이전트가 다음 요청을 하기 까지 기다려야하는 시간
    - 503 (Service Unavailable) : 서비스가 언제까지 불능인지 알려줄 수 있음.
    - 날짜, 초단위 표기
- 인증
    - Authorization : 클라이언트 인증정보를 서버에 전달
    - WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의   
    401 (Unauthorized) 응답과 함꼐 사용.
## 6. 쿠키
- Set-Cookie : 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고 HTTP 요청시 서버로 전달
- 쿠키가 없다면 모든 요청에 사용자 정보 또는 큰 데이터를 포함해야 하므로 네트워크 사용량이 크다.
- 사용처
    - 사용자 로그인 세션관리
    - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
    - 네트워크 트래픽 추가 유발
    - 최소한의 정보만 사용(세션 id, 인증 토큰)
    - 서버에 전송하지 않고 웹브라우 내부에 데이터를 저장하고 싶으면 웹스토리지(local Storage, Session Storage)참고
- 주의
    - 보안에 민감한 데이터는 저장하면 안된다.(주민번호, 신용카드 정보)
### 6.1 Expired, max-age
- 만료되면 일정 시간 이후 삭제된다.
- 세션쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지
### 6.2 도메인
- 명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
- 생략 : 현재 문서기준 도메인만 적용
### 6.3 보안
- Secure
    - 쿠키는 http, https를 구분하지 않고 전송
    - Secure를 적용하면 https인 경우에만 전송
- HttpOnly
    - XSS 공격 방지
    - 자바스크립트에서 접근 불가(document, cookie)
    - HTTP 전송에만 사용
- SameSite
    - XSRF 공격 방지
    - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키 전송
    - 아직 적용된지 오래 안됬기 때문에 브라우저에서 적용 범위 확인 후 사용