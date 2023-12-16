# 9째 주

## Servlet 

**서블릿 개념**

* 클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술

**서블릿 동작과정**

* 클라이언트가 웹 서버에 요청하면 웹 서버는 톰캣과 같은 WAS에 역할을 위임.
* WAS는 각 요청에 해당하는 서블릿을 실행함.

1. 클라이언트 요청
2. HTTPServletRequest, HttpServletResponse 객체 생성
3. Web.xml이 어느 서블릿에 대해 요청한 것인지 탐색
4. 해당 서블릿에서 service() 메서드 호출
5. doGet(), doPost() 호출
6. 동적 페이지 생성 후 HttpServletResponse 객체에 응답 전송
7. 응답이 끝나면 HttpServletRequest, HttpServletResponse 객체 소멸

## JSP

**JSP 개념**

* 서블릿만 사용해서는 웹 페이지를 보여주는데 out 객체의 println 메서드를 사용하여 HTML을 작성하므로 이를 보완하기위에 JSP를 사용함.
* Java 코드가 들어가 있는 HTML 코드

**JSP 동작과정**

1. 사용자가 페이지를 요청하면 jsp는 서블릿으로 변환
2. 서블릿파일은 컴파일되어 자바파일을 통해 .class 파일이 만들어짐.
3. Execute 를 통해 HTML 파일을 생성하여 JSP 컨테이너에게 전달
4. JSP는 HTTP 프로토콜을 통해 HTML 페이지 클라이언트에게 전달

## JSP 상대경로 절대경로

* 상대경로 : 현 파일 위치 기준으로 목적지까지의 상대적인 경로
* 절대경로 : 처음부터 시작하여 목적지까지의 절대적인 경로 / 로 시작함.

```java
<%=request.getContextPath() %><br>
// http://localhost:8081/MyWebSite/index.jsp -> /MyWebSite
<%=request.getRequestURI()  %><br>
// http://localhost:8081/MyWebSite/index.jsp -> /MyWebSite/index.jsp
<%=request.getRequestURL() %>
// http://localhost:8081/MyWebSite/index.jsp -> http://localhost:8081/MyWebSite/index.jsp

// 절대경로 사용 예제
${request.contextPath()}/js/chart/Chart.js
```

* request.getContextPath() : 프로젝트 Path(포트번호 후의 경로를 가져옴)
* request.getRequestURI() : 프로젝트 + 파일경로
* request.getRequestURL() : 전체 경로

> 혼자 사용한다면 속도가 빠르고 간결한 상대경로를 사용하겠지만, 운영이나 협업하는 환경에서는 절대 경로를 사용하자.

## JSP 핵심 명령어

## Cookie, Session

**쿠키**

* 클라이언트 식별 기술

1. 브라우저 저장
2. 서버 부담 X
3. 보안 불리
4. 서버 다중화 유리

```java

```

**세션**

* 한 사용자의 여러 요청 묶은 것
* 세션객체 : 서버의 사용자 전용 저장공간

1. 서버에 저장
2. 서버 부담 O
3. 보안 유리
4. 서버 다중화 불리

```java

```