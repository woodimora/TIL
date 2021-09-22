[김영한 - 스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술] 학습 내용 정리

## 서블릿 등록
```java
@ServletComponentScan //서블릿 자동 등록
@SpringBootApplication
public class ServletApplication {
public static void main(String[] args) {
SpringApplication.run(ServletApplication.class, args);
}
```
`@ServletComponentScan` 애노테이션으로 서블릿을 직접 등록해서 사용할 수 있게 된다.   
`@WebServlet` 애노테이션으로 서블릿을 등록한다.
```java
@WebServlet(name = "helloServlet", urlPatterns = "/hello")
public class HelloServlet extends HttpServlet {
    protected void service(HttpServletRequest request, HttpServletResponse response){
    }
}
```
### WebServlet 애노테이션 속성
- name : 서블릿의 이름. 
- urlPatterns : 서블릿의 URL 목록을 설정하는 속성. 여러개를 등록할 수 있다.
- value : urlPatterns 와 동일한 역할을 한다.

HTTP 요청을 통해 매핑된 URL이 호출되면 서블릿 컨테이너는 `service` 메서드를 실행한다.   
```java
protected void service(HttpServletRequest request, HttpServletResponse response)
```

> ### HTTP 요청 메시지 로그로 확인하는법
> `application.properties`에서 아래 문구 추가 (개발 단계에서만 사용)
> ```java
> logging.level.org.coyote.http11=debug
> ```

### 서블릿 컨테이너 동작 방식
1. 사용자(클라이언트)가 URL을 통해 요청을 보내면 HTTP Request를 Servlet Conatiner로 전송
2. HTTP Request를 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 두 객체를 생성
3. 요청한 URL을 분석하여 서블릿 탐색.
4. 해당 서블릿에서 service 메소드를 실행하여 request 를 처리하고 response에 데이터를 담아서 응답을 보냄
5. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸

### HttpServletRequest 역할
HTTP요청 메시지를 개발자가 직접 파싱하지 않아도 편리하게 사용할 수 있도록 HTTP 요청 메시지를 파싱하여 `HttpServletRequest`객체에 담에서 제공
- 임시 저장소 기능 : 해당 HTTP요청의 시작부터 끝날 때까지 유지되는 임시 저장소 기능
- 세션 관리 기능