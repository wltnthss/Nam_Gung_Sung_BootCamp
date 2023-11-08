# Day18 요약 및 헷갈리는 개념

## String 클래스

* int i = Integer.parseInt("100");  // 문자 -> 숫자

## StringBuffer, StringBuilder

* StringBuffer 는 동기화 O, StringBuilder 는 동기화 X
* StringBuffer 멀티쓰레드에 유리
* append()는 반환타입이 자신의 주소
* 비교연산자, equals 를 사용해도 false
    * String 으로 바꾼 후에 equalse 를 통해 비교해야함.
    * String s = sb.toString() , s 참조변수로 비교

## Math 클래스

* 메서드가 모두 static 이며 생성자가 private으로 선언되어있음.
* 클래스내에 인스턴스 변수가 하나도 없어서 인스턴스를 생성할 필요가 없음.

**소수점 n번째 자리 반올림한 값 얻기**

1. 원래 값에 100 곱하기
    * 90.7552 * 100 -> 9075.52
2. 위의 결과에 Math.round() 사용
    * Math.round(9075.52) -> 9076
3. 위의 결과에 100.0 으로 나누기
    * 9076 / 100.0 -> 90.76

## 래퍼 wrapper 클래스

* 기본형(int) -> 객체(Integer) 기본형 값들을 객체로 변환하여 작업을 수행하기위함.
* Number 클래스는 모든 숫자의 조상.

```java
static int parseInt(String s, int radix)

// int i = Integer.parseInt("FF", 16);  // FF(16) -> 255
```

**오토박싱 & 언박싱**

* int <-> Integer : 자동변환가능
* 기본형 값을 래퍼 클래스의 객체로 자동 변환 : 오토박싱
* 반대는 언박싱

```java
list.add(10) -> (오토박싱) -> list.add(new Integer(10));
```

## Objects 클래스

```java
// 유효성 검사
void setName(String name){
    if(name == null){
        new NullPointerException("name must not be null.");
        this.name = name;
    }
}

// Objects 클래스 이용 유효성 검사
void setName(String name){
    this.name = Objects.requireNonNull(name, "name must not be null."); // 
}
```

* Objects를 활용하면 null 체크를 간단히 활용 가능함. (equals 등등..)

## Random 클래스

```java
double randNum = Math.random();
double randNum = new Random().nextDouble()  // 위와 동일

Random rand = new Random(1);    // seed값 부여
```

* 같은 seed(종자값)을 활용하여 같은 값 같은 순서로 얻을 수 있음

## 정규식

```java
Pattern p = Pattern.compile("c[a-z]*);
Matcher m = p.matcher(data[i]);
if(m.matches()){

}
```

* 정규식 패턴은 사용할 때 찾아서 보자.

# 10장 날짜와 시간

* Date(JDK 1.0) -> Calendar(JDK 1.1) -> java.time 패키지(JDK 1.8)

## Calendar

```java
Calendar cal = new Calendar();            // 추상 클래스이므로 인스턴스 생성x
Calendar cal = Calendar.getInstance();    // 클래스를 구현한 클래스의 인스턴스 반환
```

* 싱글톤을 통해 Calendar cal 은 변경하지 않아도 된다는 장점.
* Calendar 생성시 현재 시간으로 설정
* **날짜 계산 -> 일 단위로 계산**, **시간 계산 -> 초 단위로 계산**
* Calendar 시간 set 해줄 떄 clear() 후에 설정해주기.
* 달력은 그 달의 첫째 일, 마지막 일을 구해서 for문 돌리면 끝임.

## 형식화 클래스

* DecimalFormat 을 활용하여 1,234,567 -> 1234567 형식을 줌으로써 바꿔서 사용함.
* 날짜를 출력할 때는 SimpleDateFormat 사용
    * 달 : M, 분 : m 주의
    * 주로 날짜를 yyyy-MM-dd 형식으로 사용하기위함.
* ChoiceFormat : 점수들의 등급을 매길 때 주로 사용함.
* MessageFormat : 데이터를 정해진 양식에 맞게 출력할 때 사용함.

## java.time 패키지

* String 클래스처럼 불변의 특징을 가지고 있음.
* 날짜 - 날짜 = Period , 시간 - 시간 = Duration (클래스)
* now() - 현재 날짜와 시간 저장 객체 생성
    * LocalDate date = LocalDate.now(); // 2015-11-23
* of() - 해당 필드의 값 순서대로 지정
    * LocalDate date = LocalDate.of(2015, 11, 23)   // 2015년 11월 23일
* Instant - 에포크 타임(1970-01-01 00:00:00 UTC) 부터 경과된 시간 나노초 단위 표현.
    * 컴퓨터를 위한 날짜 시간
* TemporalAdjusters - 날짜 계산 기능을 미리 구현해 놓은 것.
* 문자열 날짜와 시간 파싱
    * LocalDate newDate = LocalDate.parse("2001-01-01");

> Serializable 뜻을 정확히 모름 나중에 따로 정리해보자.
>
> 이런 것이 있다고 알아만두기.
>
> 11장 여러번보기