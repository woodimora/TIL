[김영한 - 모든 개발자를 위한 HTTP 웹 기본지식] 학습 내용 정리
# 인터넷 통신
## IP(Internet protocol) 특징
- IP 패킷 정보 : 출발 IP, 도착 IP, 메세지
- 비연결성
    - 상대가 없거나 서비스 불능 상태여도 패킷을 전송
- 비신뢰성
    - 중간에 패킷이 사라질 수 있음
    - 패킷이 순서대로 전달되지 않음
- 프로그램을 구분하지 못함
    - 같은 IP를 사용하는데 여러 어플리케이션으로 통신을 한다면 구분하지 못함
___
## 인터넷 프로토콜 4계층
#### - 어플리케이션 계층 - HTTP, FTP
#### - 전송 계층 - TCP, UDP
#### - 인터넷 계층 - IP
#### - 네트워크 인터페이스 계층 - LAN 드라이버
___
## TCP의 특징
- 연결 지향 : 3 Way Handshake(물리적 연결이 아닌 가상연결)
- 데이터 전달 보증 : 전송 후에 응답을 받는다
- 순서 보장 : x번 째부터 다시 전달 가능 ( 서버에서 어플리케이션으로 구현가능 )
- 신뢰할 수 있는 프로토콜
- 현재 대부분 TCP를 사용 (90% 이상)
___
## UDP특징
- 연결 지향 x
- 데이터 전달 보증 x
- 순서 보장 x
- 데이터 전달 및 순서가 보장되지 않지만 단순하고 빠르다 ( 3way handshake 절차 생략 -> 데이터, 시간절약 )
- IP와 거의 동일하다. port, checksum 만 추가됨.
- 어플리케이션에서 추가적으로 작업을 하여 보완할 수 있다.
    - 떠오르는 대세
    - 최적화가 가능하다 (백지와 같은 느낌)
    - HTTP/3 에서는 UDP를 사용
___
## Port
0 ~ 65535 까지 지정이 가능   
0 ~ 1023 은 이미 많이 사용되어지고 있는 Port이므로 피하는 것이 좋다.
___
## DNS (Domain Name System)
IP 는 기억하기 어렵다.  
IP 는 변동 될 수 있다.  
도메인을 활용하여 IP를 대체함
___
## URI (Uniform Resource Identifier)
Uniform : 리소스를 식별하는 통일된 방식    
Resource : 자원    
Identifier : 구분에 필요한 정보
### URI : URL, URN 을 포함하는 큰 개념
### URL : 자원의 위치 정보.
### URN : 말 그대로의 자원의 이름. 
통상적으로 URI = URL 로 많이 쓴다.
___
## Scheme
scheme://[userinfo@]host[:port][/path][?query][#fragment]   
- userinfo@ : 사용자 정보를 포함한 내용. 거의 사용하지 않음
- host : 도메인이나 IP입력
- port : 일반적으로 생략. http : 80, https : 443
    - https 는 http에 강력한 보안이 추가됨 http secure
- path : 리소스 경로, 계층적 구조
- query : key=value 형태. ?로 시작. &로 추가 가능. query parameter 또는 query String으로 불림
- fragment : html 내부 북마크. 서버에 전송되지 않음.