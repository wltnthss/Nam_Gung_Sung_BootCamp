# Day42 요약

## Servlet 문제풀이

## SERVLET

```java
class Hello{
    public static void main(String[] args){
        System.out.println("Hello")
    }
}

class Hello extends HttpServlet{
    public void service(HttpServletRequest request, HttpServletResponse response){
        System.out.println("Hello")
    }
}
```

* static 메서드 차이점으로 아래의 서블릿은 static 메서드가 아니므로 인스턴스 메서드를 사용 가능한 장점이 있음.
* 서블릿은 톰캣이 서블릿 생성과 관리를 대신해줌.
* HTML은 문자열이고, Sertvlet에서 문자열을 만들어줘서 웹 브라우저에게 전송.

**JSP, HTML 한글깨짐 현상 참고**

* response.setCharacterEncoding("utf-8");
* response.setContentType("text/html; charset=UTF-8");
* request.setCharacterEncoding("utf-8");
* Tomcat -> server.xml -> URIEncoding="UTF-8" 추가

