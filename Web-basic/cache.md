[김영한 - 모든 개발자를 위한 HTTP 웹 기본지식] 학습 내용 정리

# 캐시
## 캐시 기본 동작
- 캐시가 없으면 데이터를 매번 다운로드 받아야한다.
- 캐시 사용시 비싼 네트워크 사용량 절감
- 빠른 사용자 경험
- 캐시 시간 초과
    - 캐시 유효기간이 초과하면 서버를 통해 다시 조회, 캐시 갱신.

## 캐시 검증 헤더와 조건부 요청
- 기존 캐시와 만료된 캐시와 데이터 변화가 없다. -> 재다운로드 없이 다시 사용할 수 있다.
### Last-Modified:If-Modified-Since
- 검증헤더 : Last-Modified, 최초 캐시 전달시
- 조건부 헤더 : If-Modified-Since, 캐시 재요청시
- 304 Not Modified : HTTP 바디가 없다. -> 네트워크 데이터가 많이 줄어든다.
- 응답 헤더로 캐시 메타 데이터 갱신
- 매우 실용적인 해결책
- 1초 미만의 단위로 캐시 조정은 불가능 하다. -> 날짜 기반 로직이기 때문
- 날짜 변경은 되었지만 데이터는 변경되지 않았을 경우에도 재다운로드를 하게됨.

## If-None-Match:ETag
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
- 날짜 변경은 되었지만 데이터는 변경되지 않았을 경우.
- 데이터 변경시 ETag 를 변경
    - 캐시 제어 로직을 서버에서 완전히 관리
    - 클라이언트는 단순히 이 값을 서버에 제공 (클라이언트는 캐시 매커니즘을 모름)   
    예) 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

## 캐시 제어 헤더
- Cache-Control
    - max-age : 캐시 유효기간 초단위 제어
    - no-cache : 데이터는 캐시 가능. 항상 origin서버에 검증하고 사용
    - no-store : 데이터에 민감한 정보가 있으므로 저장하면 안됨(메모리에서 사용하고 최대한 빨리 삭제)
- Progma : 캐시 제어 (하위호환)
- Expires : 캐시 유효기간 (하위호환)

### Progma
- HTTP 1.0 하위호환
- Progma:no-cache

### Expires
- 날짜 만료일을 날짜로 지정
- Cache-Control:max-age 가 더 유명하다.

### 정리
- 검증 헤더 validate
    - ETag
    - Last-Modified
- 조건부 요청 헤더
    - If-Match, If-None-Match : ETag사용
    - If-Modified-Since, If-UnModified-Since : Last-Modified 사용

## 프록시 캐시
- 원서버 (Origin) 직접 접근하며 캐시를 보관하는 서버
- 프록시 캐시 서버
    - 캐시를 보관하는 서버(Public 캐시)
    - 로컬, 클라이언트 캐시(Private 캐시)
- Cache-Control:public : 응답이 public 캐시에 저장되어도 됨
- Cache-Control:private : 응답이 사용자만을 위한것, private 캐시에 저장(기본값)
- Cache-Control:s-maxage : 프록시 캐시에만 적용되는 max-age
- Age:60 (HTTP 헤더) : 오리진 서버에서 응답 후 프록시 캐시내에 머문 시간

## 캐시 무효화
- Cache-Control : no-cache, no-store, must-revalidate
    - no-cache : 매번 원서버에 검증, 만약 접근할 수 없을 경우 옛날 데이터라도 보내라
    - no-sotre : 저장 x
    - must-revalidate : 캐시 만료후 조회시 원서버에 검증.