# Day43 요약

## JSP 기본객체

**JSP 기본 객체**

https://freestrokes.tistory.com/20

## Cookie, Session

**Cookie**

* **클라이언트 식별 기술**
* **이름과 값이 쌍으로 저장된 정보**
* HTTP 프로토콜은 상태를 저장하지 않는 stateless(상태정보 유지안함)와 connectionless(비연결지향) 으로 서버가 클라이언트가 누구인지 확인하기 위해서 쿠키 or 세션을 사용함.
* 쿠키는 클라이언트의 상태 정보를 로컬에 저장함.
* 만료시점이 존재함.
* 정보를 서버에 저장하지 않고 로컬pc에 저장하므로 서버 부담이 줄어듬.

```java
Cookie cookie = new Cookie("id", "asdf");    // 쿠키 생성
response.addCookie(cookie);     // 응답에 쿠키 추가

Cookie[] cookies = request.getCookies();
```

**session**

**주요 응답 상태 코드**

* 200 : 요청 정상적으로 처리함
* 307 : 임시 페이지 리다이렉트
* 400 : 클라이언트 요청 잘못된 구문으로 구성됨
* 401 : 접근 허용하지 않음
* 404 : 요청한 URL 처리하기 위한 자원이 존재하지 않음
* 500 : 서버 내부 에러 발생
* 503 : 서버 일시적으로 서비스 제공 불가

**JSP 상대경로 절대경로**

https://wildwolf.tistory.com/entry/JspServlet-%EC%83%81%EB%8C%80%EA%B2%BD%EB%A1%9C-%EC%A0%88%EB%8C%80%EA%B2%BD%EB%A1%9C

**9주차 JSP rediret, forward 정리**

**9주차 JSP, servlet 정리 하기**