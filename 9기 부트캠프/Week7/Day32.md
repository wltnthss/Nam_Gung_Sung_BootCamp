# Day32 요약

## javascript

**변수 scope**

1. 전역 global
    * 전역변수는 window에 포함
    * window를 class로 생각하자 
2. 지역 local
    * 함수 내부에서 사용
3. 블럭 block(ES6)

**형변환**

1. 숫자 변환 
    * Number(), parseInt(), parseFloat(), *1
2. 문자열 변환
    * String()
3. boolean 변환
    * Boolean(), !!

**연산자**

* 문자열 + 숫자 -> 숫자
    * 덧셈 연산 제외 ex) 7 + "5" = "75"
* 소수점은 toFixed 사용
    * x = 1.0.toFixed(1)
* == 은 값만 비교, === 값과 타입 비교   
    * == 은 자동형변환 가능, sql 튜닝에서는 자동형변환에 의지 x
    * === 사용 하자
    * ex) let num = 123, let num2 = new Number(123) == 은 true, ===은 false

**배열**

* js는 배열의 크기를 동적으로 변경 가능하고, 하나의 배열에 여러 타입 저장 가능함.
* 배열 선언 arr = []; 
* 배열의 요소 추가,삭제

## HTML

**attribute, property**

* attribute : html 내의 태그
* property : 태그가 객체가 되어 iv역할을 하는 것
* ex) <h1 title = "header"> Hello HTML5 </h1>
* attribute는 title, property는 header, Hello HTML5 임.