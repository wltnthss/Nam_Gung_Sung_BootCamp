# Day47

## JSP

**버퍼**

* JSP는 출력 내용을 버퍼에 저장한 후, 버퍼에 저장된 내용을 클라이언트에 전송함.
* 버퍼는 기본적으로 4kb ~ 8kb

**배포**

* 일반적으로 was에 프로젝트 war 파일을 배포
* springboot 에서는 프로젝트.jar(톰캣까지) 담아서 같이 배포

**데이터 저장**

1. GET 방식
2. POST 방식
3. 저장소 4개 PAGE -> REQUEST -> SESSION -> APPLICATION (크기 순)
    * Session 이 부담이 가장됨.(클라이언트마다 하나씩)
    * pageContext는 페이지마다 하나씩 존재
    * request는 forward한 페이지까지 존재
    * application 은 전체에 존재

**JSP 페이지 에러페이지**

1. JSP에 에러페이지 직접 지정
2. 상태코드별 지정 (Web.xml)
3. 에러종류별지정 (Web.xml)

**JSP include**

1. <jsp:inclue> 결과 포함
2. @include 소스 포함
3. <include> (web.xml) 자동 코드 추가 (소스 포함)