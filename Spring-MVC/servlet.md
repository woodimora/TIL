[김영한 - 스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술] 학습 내용 정리
# 서블릿
웹 애플리케이션 서버에서 HTTP 메시지를 파싱하여 서블릿을 호출한다. 서블릿은 이떄 비즈니스 로직을 실행한다.   
HttpServletRequest, HttpServletResponse 로 HTTP 스펙을 편리하게 사용할 수 있다.   
서블릿을 지원하는 WAS를 서블릿 컨테이너라고 한다. 서블릿의 초기화, 생성, 호출, 종료 등을 관리한다.   
## 서블릿 컨테이너의 특징
- 서블릿 객체는 싱글톤으로 관리 -> 하나를 만들어서 모든곳에 사용한다. *공유변수 주의
- JSP도 서블릿으로 변환되어서 나온다.
- 동시 요청을 위한 멀티 스레드 처리를 지원한다.

## 서블릿 객체를 누가 호출하는가?
서블릿 객체의 애플리케이션 코드를 하나하나 순차적으로 실행하는 것은 쓰레드이다.   
쓰레드가 없다면 자바 코드를 실행 할 수 없다.   
쓰레드는 하나의 한 코드 라인만 수행할 수 있다. 동시 처리가 필요하다면 쓰레드를 추가하여야 한다.   
   
   
## 멀티 쓰레드      
쓰레드 하나로 여러 요청을 처리하게 되면 애플리케이션 로직에 따라 다르지만 모든 요청이 죽거나 대기를 해야한다.  
### 요청마다 쓰레드를 생성할 경우
### 장점
- 동시 요청을 처리할 수 있다.
- 리소스가 허용할 때까지 처리가 가능하다.
- 쓰레드간 영향을 주지 않는다.
### 단점
- 쓰레드의 생성 비용이 비싸다. -> 요청마다 쓰레드 생성시 응답속도의 저하를 일으킨다.
- 쓰레드 컨텍스트 스위칭 비용이 발생한다.
- 쓰레드 생성에 제한이 없다. -> 요청이 너무 많으면 CPU, 메모리의 임계점 초과로 서버가 죽을 수 있다.

## 쓰레드 풀
필요한 쓰레드를 미리 만들어 놓고 요청시 사용가능한 쓰레드를 쓰레드 풀에서 호출하여 사용하고 다시 반납한다.
- 놀고 있는 쓰레드가 없으면 대기하거나 거절할 수 있다. 대기 시 특정 숫자 만큼만 대기 할 수 있다.
- 톰켓은 최대 200개 까지 기본으로 제공한다. 변경이 가능하다.
- 쓰레드가 미리 생성되어 있어서 생성, 종료에 대한 비용이 절약된다. 응답 속도도 빨라진다.
- 생성된 쓰레드가 정해져 있으므로, 많은 요청이 들어와도 기존 요청은 안전하게 처리가 가능하다.

멀티 쓰레드에 대한 부분은 WAS가 처리한다.
개발자가 멀티 쓰레드 관련 코드를 신경 쓰지 않아도 된다. 개발자는 싱글 쓰레드 프로그래밍 하듯이 소스코드를 개발하면 된다. 싱글톤 객체(스프링 빈)는 주의해서 사용해야한다.
