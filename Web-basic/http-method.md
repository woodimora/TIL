[김영한 - 모든 개발자를 위한 HTTP 웹 기본지식] 학습 내용 정리

# HTTP 메서드
- URI는 리소스만 식별한다.
- 리소스와 행위를 분리하여 사용한다.   

## 주요 메서드
### GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리파라미터, 쿼리스트링)를 통해 전달
- 메시지 바디를 사용해서 전달 할 수 있지만, 지원하는 곳이 많지 않음.

### POST
- 요청 데이터 처리, 주로 등록에 사용한다.
- 메시지 바디를 통해 서버로 요청 데이터를 전달한다.
- 서버는 요청된 데이터를 처리한다.
- 주로 전달은 데이터로 신규 리소스 등록, 프로세스 처리에 사용   
프로세스 처리는 프로세스의 상태가 변경. 새로은 리소스가 생성 안될 수도 있음.
- 서버가 새로 등록된 리소스의 URI를 생성해준다.
- 컬렉션 (Collection)
    - 서버가 관리하는리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리

### PUT
- 리소스를 대체
- 리소스가 없으면 생성
- 덮어씌우기
- 클라이언트가 리소스를 식별해야한다 (*중요)
- 클라이언트가 리소스의 위치를 알고 URI를 지정한다.
- 스토어 (Store)
    - 클라이언트가 관리하는 리소스 저장소
    - 클라이언트가 리소스의 URI를 알고 관리한다.

### PATCH
- 리소스 부분 변경
- 신규라서 안되는 경우가 있다. -> POST 사용

### DELETE
- 리소스 제거

## 기타 메서드
- HEAD : GET 과 동일하지만 메시지 부분을 제외하고 상태 결과 헤더만 반화
- OPTION : 대상 리소스에 대한 통신 가능 옵션(메서드)를 설명(주로 COPS에서 사용)
    - COPS : Cross-Origin Resource Sharing   
    교차 출처 리소스 공유   
    scheme, host, port 로 동일 여부 판단.   
    브라우저에 포함되는 구현 정책이므로 서버간 통신시기는 상관없다.   
    요청 헤더의 Origin 필드와 응답 헤더의 Access-Control-Allow-Origin 과 비교해서 유효성 판단.   
    본요청을 보내기 전에 예비 요청을(Preflight)을 보낼 때, OPTION 메서드를 사용.
- CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정.
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행
---
## 메서드의 속성
- 안전
- 멱등
- 캐시가능

### 안전
- 호출해도 리소스가 변경되지 않는다. (GET)
- 해당 리소스에 대해서만 고려

### 멱등
- 한번이든 여러번이든 결과가 동일하다.
- GET, PUT, DELETE
- 자동 복구 메커니즘
- 외부요인으로 중간에 리소스가 변경되는 것은 고려하지 않는다.

### 캐시가능
- 응답 결과 리소스를 캐시해서 사용해도 되는가
- GET, HEAD, POST, PATCH 가 캐시가 가능하나 GET, HEAD 정도만 캐시로 사용한다.
- POST, PATCH 는 본문 내용까지 캐시키로 고려해야 하는데 구현이 쉽지 않다.
---
## 클라이언트에서 서버로 데이터 전송하는 방법
### 쿼리 파라미터를 통한 전송
- GET
- 주로 정렬, 필터
### 메시지 바디를 통한 데이터 전달
- POST, PUT, PATCH
---
## 데이터의 종류
### 정적 데이터
- GET 으로 조회
- 쿼리 파라미터 없이 경로로만 조회가능
### 동적 데이터
- HTML Form
- HTTP API
- 검색, 게시판 정렬 필터, 정렬 조건에 사용
- 조회는 GET 사용
- GET 은 쿼리 파라미터를 사용해서 데이터 전달

### HTML Form
- POST
    - Content-Type: x-www-form-urlencoded   
    Body에 query parameter 형식으로 전달
    - Content-Type: multipart/form-data   
    binarydata 전송에 사용   
    데이터, 파일을 함께 전송가능하다
- GET
    - 쿼리 파라미터로 전송
- HTML form submit 시 POST전송
- HTML form 은 GET, POST만 지원된다 -> AJAX 같은 기술로 해결가능
- 컨트롤 URI   
    - 동사로 된 리소스 경로 사용
    - HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API포함)

### HTTP API
- 서버 to 서버
- 앱 클라이언트
- 웹 클라이언트
- POST, PUT, PATCH 메시지 바디를 통해 데이터 전송
- GET : 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json을 주로 사용
---
## 저장소 종류
- document : 단일 개념
- collection : 서버가 관리하는 자원, 서버가 URI생성
- store : 클라이언트가 관리하는 저장소, 클라이언트가 URI를 알고 관리
- controller(컨트롤 URI) : 동사형태로 URI로 관리