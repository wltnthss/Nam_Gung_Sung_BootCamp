# Day6 요약 및 헷갈리는 개념

## 클래스변수, 인스턴스변수, 지역변수

* 인스턴스 변수 - iv (개별속성)
    * 객체 생성 후에 만듬.
* 클래스 변수 - cv (공통속성)
    * 객체와 상관없이 항상 사용가능함.
* 지역변수 - lv 
    * 메서드안에 선언된 변수

> 코딩하기전에 **설계의 중요성** 설계 먼저하고, 주석다는 습관 가지자

## 기본형 매개변수

```java
class Data1{
	int x;
}
public class PrimitiveParamEx {

	public static void main(String[] args) {
		Data1 d1 = new Data1();
		d1.x = 10;
		System.out.println("main() : x = " + d1.x);
		
		change(d1.x);
		System.out.println("After change(d1.x)");
		System.out.println("main() : x = " + d1.x);
	}
	
	public static void change(int x) {
		x = 1000;
		System.out.println("change() : x = " + x);
	}
}
```
```
main() : x = 10
change() : x = 1000
After change(d1.x)
main() : x = 10
```

* 기본형인 경우에는 d.x의 값이 변경된 것이 아니라 change 메서드의 매개변수 x의 값이 변경된 것임.
* 이처럼 기본형 매개변수인 경우에는 변수에 저장된 값만 읽을 수 있고 변경할 수 는 없음.

## 참조형 매개변수

```java
class Data2{
	int x;
}

public class ReferenceParamEx {
	public static void main(String[] args) {
		Data2 d2 = new Data2();
		d2.x = 10;
		System.out.println("main() : x = " + d2.x);
		
		change(d2);
		System.out.println("After change(d2.x)");
		System.out.println("main() : x = " + d2.x);
	}
	
	public static void change(Data2 d2) {
		d2.x = 1000;
		System.out.println("change() : x = " + d2.x);
	}
}
```
```
main() : x = 10
change() : x = 1000
After change(d2.x)
main() : x = 1000
```

* 기본형 매개변수와 달리 값이 저장된 주소를 change메서드에 넘겨줌으로써 변경하는 것이 가능함.

## 참조형 반환타입

```java
class Data3{
	int x;
}

public class ReferenceReturnEx {

	public static void main(String[] args) {
		
		Data3 d3 = new Data3();
		d3.x = 10;
		
		Data3 d4 = copy(d3);
		System.out.println("d3.x =" + d3.x);
		System.out.println("d4.x =" + d4.x);
	}
	
	static Data3 copy(Data3 d3) {
		Data3 tmp = new Data3();
		tmp.x = d3.x;
		
		return tmp;
	}
}
```
```
d3.x =10
d4.x =10
```

* copy 메서드는 새로운 객체를 생성한 다음, 매개변수로 넘겨받은 객체에 저장된 값을 복사해서 반환함.
* 반환 값이 Data객체의 주소이므로 반환 타입이 Data 인 것임.