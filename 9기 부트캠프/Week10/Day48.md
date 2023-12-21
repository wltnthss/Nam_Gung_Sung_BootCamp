# Day48

## JSP 정리

**원격프로그램**

1. 등록
2. URL 연결

* WebServlet("/hello) 이 등록과 URL 연결을 해줌.

* service(HttpServletRequest request, HttpServletResponse response)
    * // 1. 입력
    * // 2. 처리
    * // 3. 출력

* 형식에 맞추어 코드 작성

**쿠키, 세션**

* 쿠키 : 클라이언트 식별기술 (이름 = 값), 브라우저에 저장함.
* 세션 : 서버의 개별 저장소 (클라이언트 당 1개), K,V 로 이루어져있음.

**Scope 4가지**

1. PAGE
2. REQUEST
3. SESSION
4. APPLICATION

* 범위는 1~4 순서대로 커짐.
* 쓸 때는 setAttribute, 읽을 때는 getAttribute

**Redirect & Forward**

* Redirect : 요청 2번, 응답 2번
* Forward : 요청1전, 응답1번 (request에 값 담아서 전달 가능)

**include 3가지**

1. jsp:include : 결과 합치기
2. @include : 소스 합치기
3. include web.xml : 소스 자동합치기

**에러처리 3가지**

1. 에러페이지지정 : *.jsp
2. 예외종류에 따라 처리 : Web.xml
3. 상태코드에 따라 처리 : Web.xml

**페이지이동 5가지**

1. URL 입력
2. a 태그 클릭
3. form 태그 
4. redirect
5. forward

# 공부할 때 팁

1. 내가 코딩할 내용 주석 달기 => 주석 정리
2. 코드 삭제
3. 주석 정리한 내용을 보고 코드를 재작성 
4. 반복학습