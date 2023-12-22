c# Day49

## JSP

**JSP**

**EL**

* 지역변수를 통해 접근할 수 없음, 페이지 저장소를 통해서 값을 주고 받음
* 정수는 Long 이고 실수는 Double

```java
${param} = request.getParameter;
${cookie} = request.getCookies();

//ex  
// ${cookie.id.value}
```

**JSTL**

* scope의 기본 Default 는 페이지

```java
<c:set var="변수명" value"값">  // scope="page"
<c: if test="${expr}">...</c:if>
<c:choose>
    <c:when>
        // if 문과 동일
    </c:when>
    <c:otherwise>
        // default 값
    </c:otherwise>
</c:choose>
<c:foreEach var="i" items="${list}" begin="2" end"4">
```