# 부트캠프전 자바의 정석 예습

## 1~5장은 반복문, 조건문, 배열이라 짧게 보고 알고리즘 문제 풀이, 6장 객체지향부터는 2번씩 보고 README 정리. 2번씩 보고 완벽히 이해했으면 Spring 공부 및 토이 프로젝트 진행

<details>
<summary style="font-size:20px">객체 지향 개념</summary>
<div markdown="1">

### 객체 지향 언어

* 코드의 재사용성이 높음 
* 유지보수에 용이

* OOP특징 4가지
  * 캡슐화 
  * 상속
  * 추상화
  * **다형성**

> 특징 4가지의 세부적인 사항은 따로 note에 정리해두자.

* 클래스 정의 : 객체를 정의해 놓은 것.
* 클래스 용도 : 객체를 생성하는데 사용, 클래스는 단지 객체를 생성하기위함.
* 객체 : 실제로 존재하는 것, 인스턴스 변수들의 묶음
* 객체 용도 : 객체가 가지고 있는 기능과 속성에 따라 다름.
  * ex) 클래스 : 제품 설계도, 객체 : 제품

### 객체

* 객체 = 속성(변수) + 기능(메서드)
  * ex) TV를 예로 들었을 경우, 채널 : int channel, 채널 높이기 : channelUp() {...} 

* 클래스로부터 객체를 만드는 과정 : 인스턴스화
* 그 클래스로부터 만들어진 객체 : 해당 클래스의 인스턴스

* TV설계도를 예로 들어보자.
  
```
클래스명 변수명;            // 객체 참조를 위한 참조변수
변수명 = new 클래스명();    // 클래스의 객체를 생성했음. 객체의 주소를 참조변수에 저장

Tv tv;
tv = new Tv();
``` 

### 객체배열 

* 객체배열은 참조변수 배열이라고도함

```
Tv[] tvArr1 = new Tv[3];              // tvArr1 참조변수의 객체 주소 생성

for(int i=0; i<tvArr1.length; i++) {  
			tvArr1[i] = new Tv();
}
```

* tvArr1[0], tvArr1[1], tvArr1[2] 참조변수 세 개를 배열로 만듬.

### 선언위치에 따른 변수의 종류

* 변수는 총 세가지
  * 인스턴스 변수 - 클래스 영역에 선언, 인스턴스를 생성할 때 만들어짐.
  * 클래스 변수 - static 변수라고도하며, 공통된 저장공간을 공유함. **클래스명.클래스 변수** 사용. 클래스가 메모리에 올라갈 때 만들어짐.
  * 지역 변수 - 메서드 영역에 선언되어 메서드 내에서 {} 블럭내에서 사용하며, 메서드 종료시 사라짐. 변수 선언문이 수행되었을 때 만들어짐.

### 클래스 변수와 인스턴스 변수

```java
public class Card {
	String kind;        // 인스턴스 변수 무늬 kind
	int num;            // 인스턴스 변수 숫자 num
	
	static int weight;  // 클래스 변수 너비 weight
	static int height;  // 클래스 변수 높이 height
}
```

* 카드를 예로 들어보자.
  * Card 인스턴스는 자신만의 무늬와 숫자를 가지고 있음.
  * 각 카드의 너비와 높이는 공통적으로 같은 값을 가져야하므로 클래스 변수로 설정.
  * 카드의 너비와 높이를 변경하는 경우 한 카드의 클래스 변수 weight, height 만 변경하면됨.

> 공통 속성은 클래스 변수(static), 개별 속성은 인스턴스 변수(클래스 객체 생성)

### 메서드 

* 간단하게 코드의 중복을 제거하기위해 문장들을 묶은 것.
* 값(입력)을 받아서 처리하고, 결과를 반환(출력) 하는 역할.

```java
반환타입 메서드이름(타입 변수명, 타입 변수명, ...){
  // 실행코드...
}

int add(int a, int b){
  int result = a + b;
  return result;
}
```

* 매개변수 a, b는 0~n개의 해당하고 출력은 0~1개에 해당함. void인 경우에는 출력값이 없을 수 있음.
* 선언부는 int arr .. 에 해당하고 구현부는 실행코드에 해당함.

> 메서드는 클래스 영역에만 사용가능.

#### 정리

![Alt text](image.png)

* Class는 Static 영역에 생성, new 연산을 통해 생성한 객체는 Heap영역에 생성됨.
* 객체를 통해 생성한 Heap영역에 있는 메모리는 GC에 의해 수시로 관리를 받으면서 사용하지 않으면 제거됨.
* 하지만 Static은 공통으로 사용한다는 점에서 유리한 이점을 가지고 있지만, GC관리 영역 밖에 있으므로 프로그램 종료시까지 메모리가 유지됨.
  * -> 이는 시스템의 퍼포먼스에 악영향을 미침. 그러므로 Static은 꼭 필요한 경우 사용해야함.

</div>
</details>

<details>
<summary style="font-size:20px">호출스택, 매개변수</summary>
<div markdown="1">

### 호출스택

* 호출스택 : 메서드 수행에 필요한 메모리가 제공되는 공강
* stack의 동작원리, LIFO LastInFirstOut 택배가 쌓이듯이 차례로 호출이 쌓이면 맨 위에서 차례로 제거됨.

* main() 이 println() 호출 과정
  1. main이 호출 (main 메서드 실행상태)
  2. main 메서드가 println을 호출하면 main 메서드 위에 println이 올라감. (main 대기상태 , println 실행상태)
  3. println이 종료되면 스택에서 제거되고 main 메서드로 돌아옴.(main 실행상태)
  4. 실행할 메서드가 없으므로 main도 제거됨. 

> 스택에 대해서는 note에 따로 정리해두자.

### 기본형 매개변수, 참조형 매개변수

* 매개변수의 타입이 기본형일 때는 기본형 값이 복사되지만, 참조형일 경우는 인스턴스의 주소가 복사됨.
* 기본형 매개변수 - 변수의 값을 읽기만 할 수 있음.
* 참조형 매개변수 - 변수의 값을 읽고 변경할 수 있음.

#### 기본형 매개변수 예제

```java
class Data{
	int x;
}

public class PrimitiveType {
	public static void main(String[] args) {
		Data d = new Data();
		d.x = 10;
		System.out.println("main() : x = " + d.x);
		
		change(d.x);
		System.out.println("After change(d.x)");
		System.out.println("main() : x = " + d.x);
	}

	static void change(int x) {   // 기본형 매개변수
		x = 1000;
		System.out.println("change() : x = " + x);
	}
}
```

```
main() : x = 10
change() : x = 1000
After change(d.x)
main() : x = 10
```

* change 메서드 호출되며 d.x 가 change메서드의 매개변수 x에 복사됨.
* change 메서드에서 x의 값을 1000으로 변경.
* change 메서드가 종료되면서 매개변수 x는 스택에서 제거.

> d.x의 값이 변경된 것이 아니라 change 메서드의 매개변수 x의 값이 변경된 것임.

#### 참조형 매개변수 예제

```java
class Data2{
	int x;
}

public class ReferenceType {
	public static void main(String[] args) {
		Data2 d = new Data2();
		d.x = 10;
		System.out.println("main() : x = " + d.x);
		
		change(d);
		System.out.println("After change(d)");
		System.out.println("main() : x = " + d.x);
	}

	static void change(Data2 d2) {
		d2.x = 1000;
		System.out.println("change() : x = " + d2.x);
	}
}
```

```
main() : x = 10
change() : x = 1000
After change(d)
main() : x = 1000
```

* change 메서드 호출되며 참조변수 d의 주소가 매개변수 d2에 복사됨.
* change 메서드에서 매개변수 d2로 x의 값을 1000으로 변경
* change 메서드가 종료되면서 매개변수 d는 스택에서 제거됨.

> 참조형 매개변수는 x값이 아닌 변수 d의 주소가 매개변수 d2에 복사됨.

### static 메서드, 인스턴스 메서드   

* static 이란 뭘까 ??
  1. 클래스 설계 시에 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙임.
  2. static이 붙은 변수(클래스변수) 는 클래스가 메모리에 올라갈 때 자동으로 생성되므로 인스턴스를 생성하지 않아도됨.
  3. 클래스 메서드는 인스턴스 변수를 사용할 수 없음. 반면에 인스턴스 메서드는 클래스 메서들르 사용할 수 있음.
  4. 매서드 내에서 인스턴스 변수를 사용하지 않는다면 static 붙이는 것을 고려함. (메서드 호출시간이 짧아지므로 성능 향상)

> 클래스의 멤버변수 중 모든 인스턴스에 공통된 값을 유지해야되는 것이 있음 -> static 고려해봄.
	
> 작성한 메서드 중에서 인스턴스 변수나 인스턴스 메서드를 사용하지 않음 -> static 고려해봄.

</div>
</details>

<details>
<summary style="font-size:20px">오버 로딩</summary>
<div markdown="1">

### 오버로딩

* 한 클래스 안에 같은 이름의 메서드를 여러 개 정의하는 것.
* 오버로딩 조건
  1. 매서드 이름이 같아야함
  2. 매개변수의 개수 or 타입이 달라야함
  3. 반환 타입은 관계없음.

```java
public class Overloading {

	public static void main(String[] args) {
		
		MyMath3 math3 = new MyMath3();
		System.out.println("math3.add(3, 3) 결과 : " + math3.add(3, 3));
		System.out.println("math3.add(3, 3L) 결과 : " + math3.add(3, 3L));
		System.out.println("math3.add(3L, 3) 결과 : " + math3.add(3L, 3));
		System.out.println("math3.add(3L, 3L) 결과 : " + math3.add(3L, 3L));
		
		int[] a = {100, 200, 300};
		System.out.println("math3.add(a) 결과 : " + math3.add(a));
	}
}

class MyMath3{
	int add(int a, int b) {
		System.out.print("int add(int a, int b) - ");
		return a+b;
	}
	long add(int a, long b) {
		System.out.print("long add(int a, long b) - ");
		return a+b;
	}
	long add(long a, int b) {
		System.out.print("long add(long a, int b) - ");
		return a+b;
	} 
	long add(long a, long b) {
		System.out.print("long add(long a, long b) - ");
		return a+b;
	}
	
	int add(int[] a) {
		System.out.print("int add(int[] a) - ");
		int rslt = 0;
		for(int i=0; i<a.length; i++) {
			rslt += a[i];
		}
		return rslt;
	}
}
```

```
int add(int a, int b) - math3.add(3, 3) 결과 : 6
long add(int a, long b) - math3.add(3, 3L) 결과 : 6
long add(long a, int b) - math3.add(3L, 3) 결과 : 6
long add(long a, long b) - math3.add(3L, 3L) 결과 : 6
int add(int[] a) - math3.add(a) 결과 : 600
```
 
> 동일한 기능을 하는 메서드를 하나의 이름으로 정의함으로써 오류를 줄여주고, 메서드의 이름만 보고 예측 가능함.

</div>
</details>

<details>
<summary style="font-size:20px">생성자</summary>
<div markdown="1">

### 생성자

* 인스턴스가 생성될 때 호출되는 인스턴스 초기화 메서드.
* 이름이 클래스 이름과 같아야함.
* 모든 클래스는 반드시 생성자를 가짐. (컴파일러가 생성자가 하나도 없을 떄 자동으로 만들어줌)
* 리턴 값이 없음.

```
클래스 이름(타입 변수명, 타입 변수명, ...){
    // 인스턴스 생성 시 수행될 코드
    // 주로 인스턴스 변수의 초기화 코드 적음.
}
```

```java
class Car{
	
	String color;
	String gearType;
	int door;
	
	Car(){
		System.out.println("기본 생성자 호출");
	}
	
	Car(String c, String g, int d){
		System.out.println("매개변수 생성자호출");
		color = c;
		gearType = g;
		door = d;
	}
}
public class Constructors {

	public static void main(String[] args) {
		
		Car car1 = new Car();
		
		car1.color = "white";
		car1.gearType = "auto";
		car1.door = 4;
		
		Car car2 = new Car("black", "auto", 2);
		
		System.out.println("car1 color = " + car1.color + ", car1 gear = " + car1.gearType + ", car1 door = " + car1.door);
		System.out.println("car2 color = " + car2.color + ", car2 gear = " + car2.gearType + ", car2 door = " + car2.door);
	}
}
```

```
기본 생성자 호출
매개변수 생성자호출
car1 color = white, car1 gear = auto, car1 door = 4
car2 color = black, car2 gear = auto, car2 door = 2
```

* car1 객체에는 기본 생성자를 생성, car2 객체에는 매개변수가 있는 생성자를 생성.
* 보통은 car2의 생성자를 객체로써 사용함.

#### 생성자 this

* 인스턴스 자신을 가리키는 참조변수 

```java
Car(String color, String gearType, int door){
		this.color = color;
		this.gearType = gearType;
		this.door = door;
	}
```

* this.color 는 Car에서 정의한 인스턴스변수, String color는 매개변수로 지역변수에 해당함.
* 생성자의 매개변수로 인스턴스변수들의 초기값을 제공받는 경우가 많기 때문에 이렇게 쓰임.

```java
	Car(String c, String g, int d){
		color = c;
		gearType = g;
		door = d;
	}
```

* 위의 예제처럼 매개변수의 이름을 다르게 하는 것 보다 this를 사용해서 구별하는 것이 의미가 명확함.
</div>
</details>

<details>
<summary style="font-size:20px">상속</summary>
<div markdown="1">

### 상속

* 기존의 클래스로 새로운 클래스를 작성하는 것.
* 두 클래스를 부모와 자식으로 관계를 맺어주는 것.
* 상속을 통해 보다 적은 양의 코드로 새로운 코드를 작성하고, 공통적으로 관리하여 유지보수에 용이함.

```java
class 자식클래스 extends 부모클래스 {
	...
}

class Parent{
	...
}

class Child extends Parent{
	...	
}
```

* 상속해주는 클래스(Parent)를 부모 클래스라고 하고, 상속 받는 클래스(Child)를 자식 클래스라고함.
* 자식 클래스 Child는 부모 클래스 Parent를 포함할 수 있다고도함.
* 부모 클래스가 변경되면 자식 클래스는 영향을 받지만, 자식 클래스가 변경되는 것은 부모 클래스에 영향을 주지 않음.
* 자식 클래스는 부모 클래스의 모든 멤버를 상속받지만 생성자와 초기화 블럭은 상속되지 않음.
* 자식 클래스의 멤버 개수는 부모 클래스보다 항상 같거나 많음.

```java
public class Ex7_1 {

	public static void main(String[] args) {
		
		SmartTv stv = new SmartTv();
		stv.channel = 10;
		stv.channelUp();
		System.out.println(stv.channel);
		
		stv.displayCaption("자바의정석 상속 이 부분은 안나올거임");
		stv.caption = true;
		stv.displayCaption("자바의정석 상속");
	}
}

class Tv{
	
	boolean power;
	int channel;
	
	void power() {
		power = !power;
	}
	
	void channelUp() {
		channel++;
	}
	
	void channelDown() {
		channel--;
	}
}

class SmartTv extends Tv{
	
	boolean caption;
	
	void displayCaption(String text) {
		if(caption) {
			System.out.println(text);
		}
	}
}
```

* 자식 클래스의 인스턴스를 생성하면 부모 클래스의 멤버도 같이 생성되기 때문에 부모 클래스의 인스턴스 생성없이 사용가능함.

#### 상속은 언제 사용?

* 클래스를 설계할 때 상속을 쓰는 경우는 어떠한 경우가 있을까?

```java
//1
class Circle{
	Point c = new Point();
	int r;
}

class Circle extends Point{
	int r;
}
```

* 위의 경우를 보았을 때 Circle클래스를 작성할 때 Point클래스를 포함시키거나 상속받는거는 별 차이 없어보임.
* 이러한 경우 ~은 ~이다 (is a), ~은 ~을 가지고 있다 (has a) 을 활용하자.

> 원은 점이다 - Circle is a Point

> 원은 점을 가지고 있다. - Circle has a Point

* 원은 점을 가지고 있다. has a 관계가 더 어울리므로 이러한 경우는 상속보다는 포함관계가 더 알맞음.

* 상속관계 is a 인 경우 Car와 SportsCar 를 예로 들어보자.
* SportsCar는 Car이다. 라는 문장이 어울리는 경우 Car를 부모클래스로 두어 상속관계를 맺는 것이 알맞음.

* 자바에서는 단일 상속만을 허용함.
* 다중상속을 허용하면 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있다는 장점이 있지만, 관계가 복잡해짐.
* 비중이 높은 클래스 하나만 상속관계로, 나머지는 포함관계로 작성함.

#### Object 클래스

```java
class Tv{

}

class Tv extends Object{

}

Tv tv = new Tv();

public static void main(String[] args) {
	tv.toString();
	tv.equals();
}

```

* 부모가 없는 클래스는 자동적으로 Object 클래스를 상속받음.
* 모든 클래스는 Object클래스에 정의된 11개의 메서드를 상속받음. (toString, equals 등등..)
* 상속계층도 최상위에는 Object 클래스가 위치함.

#### 참조변수 super

* super는 자식 클래스에서 부모 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수임.

```java
public class Super {
	
	public static void main(String[] args) {
		
		Child child = new Child();
		child.method();
	}
}

class Parent{
	int x = 10;
}

class Child extends Parent{
	int x = 20;
	
	public void method() {
		System.out.println("x = " + x);
		System.out.println("this.x = " + this.x);
		System.out.println("super.x = " + super.x);
	}
}
```

* 위의 예제와 같이 자식 Child 클래스는 부모 Parent 클래스로부터 x를 상속받는데, x값이 같아서 구분할 방법이 필요함.
* 이럴 때 부모 클래스의 멤버를 참조하는 경우 super 키워드를 사용함.

```java
public class Super {
	
	public static void main(String[] args) {
		
		Child child = new Child(1, 2, 3);
		System.out.println(child.toString());
		
		System.out.println();
		
		Parent parent = new Parent(5, 6);
		System.out.println(parent.toString());
	}
}

class Parent{
	int x, y;
	
	Parent(int x, int y){
		this.x = x;
		this.y = y;
		System.out.println("Super 생성자 호출");
	}
	
	public String toString() {
		return x + "," + y;
	}
}

class Child extends Parent{
	
	int z;
	
	Child(int x, int y, int z) {
		super(x, y);		// super(x,y) 는 매개변수가 있는 Parent 의 생성자를 호출함. Parent 기본 생성자가 있으면 this.x, this.y 사용 가능.
		this.z = z;
		System.out.println("Child 생성자 호출");
	}
	
	@Override
	public String toString() {
		return x + "," + y + "," + z; 
	}
}
```

```
Super 생성자 호출
Child 생성자 호출
1,2,3

Super 생성자 호출
5,6

```

* 자식 클래스인 Child에서 Parent로부터 상속받은 x,y를 초기화함.
* child 객체를 생성할 때 Child 생성자에서 super 호출을 통해 Parent의 생성자가 호출되며 Super생성자 호출, Child 생성자 호출이됨.
* child에서 오버라이딩한 toString을 통해 1,2,3 이 출력되고 생성자도 동일한 로직으로 호출이됨.

</div>
</details>

<details>
<summary style="font-size:20px">오버라이딩</summary>
<div markdown="1">

* 부모 클래스로부터 상속받은 메서드의 내용을 변경하는 것.
* 선언부는 바꾸지 못하고 구현부만 바꿀 수 있음.
* 오버라이딩 조건
  * 메서드의 선언부(메서드 이름, 매개변수, 반환타입)은 부모클래스와 자식클래스가 일치해야함.
  * 접근 제어자는 부모 클래스의 메서드보다 좁은 범위로 변경 할 수 없음.(부모가 protected 이면 자식은 protected or public 이어야함.)
  * 부모 클래스의 메서드보다 많은 수의 예외처리를 선언할 수 없음.

```java
public class Extends {

	public static void main(String[] args) {
		
		Point p1 = new Point();
		p1.x = 10;
		p1.y = 20;
		p1.getLocation();
		
		Point3D p2 = new Point3D();
		p2.x = 5;
		p2.y = 10;
		p2.z = 20;
		p2.getLocation();
		
		System.out.println(p1.getLocation());
		System.out.println(p2.getLocation());
		
	}
}

class Point{
	int x;
	int y;
	
	public String getLocation() {
		return "x : " + x + ", y : " + y;
	}
}

class Point3D extends Point{
	
	int z;
	
	@Override
	public String getLocation() {
		return "x : " + x + ", y : " + y + ", z : " + z;
	}
	
}
```

* Point3D는 Point로 부터 x,y 상속받고 getLocation() 메서드를 사용중임.
* 부모클래스에서 사용하는 getLocation() 메서드를 그대로 사용할 수도 있지만 자식 클래스에 변경하여 사용가능함.
* 왜 사용할까?
  * 부모클래스 Point 에서 getLocation 이 좌표를 가져다주는 기능을 사용했듯이 자식 클래스에서도 좌표를 문자열로 얻을 수 있다는 기대값이 있으므로 새로운 메서드를 제공하는 것 보다 오버라이딩을 통해 메서드의 기능을 유추하고 유지보수에 용이하다는 장점이 있음.

</div>
</details>

<details>
<summary style="font-size:20px">제어자, 접근제어자, 캡슐화</summary>
<div markdown="1">

### 제어자 

* 클래스와 클래스의 멤버(멤버 변수, 메서드)에 부가적인 의미 부여
  * 접근 제어자 - public, protected, (deault), private
  * 그 외 - static, final, abstract, native, transient, synchronized, volatile, stictfp

* 주로 클래스나 멤버변수와 메서드에 사용됨.
* 하나의 대상에 여러 제어자를 같이 사용가능하나 접근 제어자는 하나만 사용 가능함.
* 접근 제어자를 가장 왼쪽에 사용함.

#### static 

* 클래스의, 공통적인 이라는 의미를 가지고 있으며 인스턴스에 상관없이 같은 값을 가지고있음.
* 멤버변수, 메서드, 초기화 블럭에 사용됨.
* 클래스가 메모리에 로드될 때 생성됨.
* 인스턴스를 생성하지 않고도 사용 가능함.
* static 메서드 내에서는 인스턴스변수들을 직접 사용할 수 없다.
  * 인스턴스 변수는 객체가 생성되어야 사용가능한데 static은 객체 생성없이 사용 가능하여 호출시기가 다르기 때문임.

#### final

* 마지막의, 변경될 수 없는 의미를 가지고 있으며, 거의 모든 대상에 사용 가능함.
* 변수에 사용하면 변경할 수 없는 상수가 되며, 메서드에 사용하면 오버라이딩을 할 수 없고, 클래스에 사용되면 부모 클래스가 될 수 없음.

### 접근 제어자

![Alt text](image-1.png)

* 접근 제어자는 멤버, 메서드, 생성자 또는 클래스에 사용되며 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 함.

1. private - 같은 클래스 내에서만 접근이 가능함.
2. (deault) - 같은 패키지 내에서만 접근이 가능함.
3. protected - 같은 패키지 내에서, 그리고 다른 패키지의 자식클래스에서 접근이 가능함.
4. public - 접근 제한이 없음.

* public > protected > default > private 순으로 나열함. 
* 접근제한없음 > 같은 패키지 + 자식클래스 > 같은 패키지 > 같은 클래스

### 캡술화와 접근 제어자

* public protected, default, private 접근 제어자는 왜 사용할까?
  * **외부로부터 데이터를 보호하기 위함**
  * 외부에는 불필요한, 내부적으로 사용되는 부분을 감추기 위함

```java
public class Time{
	public int hour;
	public int minute;
	public int second;
}

public static void main (String[] args) {
	Time t = new Time();
	t.hour = 25;		// 멤버변수에 직접 접근이 가능함.
}
```

* 위의 예제로보면 멤버변수 hour는 0보다 같거나 크고 24보다 작은 범위의 같을 가져야함.
* 하지만 위의 코드에서 25로 잘못지정해도 막을 방법이 없기에 주로 private 제한하고 getter, setter로써 값은 가져옴.

```java
public class Time {

	private int hour;
	private int minute;
	private int second;
	
	public int getHour() {
		return hour;
	}
	public void setHour(int hour) {
		this.hour = hour;
	}
	public int getMinute() {
		return minute;
	}
	public void setMinute(int minute) {
		this.minute = minute;
	}
	public int getSecond() {
		return second;
	}
	public void setSecond(int second) {
		this.second = second;
	}
}
```

* get은 단순히 멤버변수의 값은 반환하며, set은 조건에 맞는 값일 때 멤버변수의 값을 변경함.
* **만일 상속을 통해 확장될 것이 예상되는 클래스인 경우는 private 대신 protected를 사용하는 것.**
* private 이 붙은 멤버는 자식 클래스에서도 접근이 불가능하기 때문임.

</div>
</details>

<details>
<summary style="font-size:20px">다형성</summary>
<div markdown="1">

### 다형성

* 여러 가지 형태를 가질 수 있는 능력.
* **부모 타입 참조 변수로 자식 타입 객체를 다루는 것.**

```java
class Tv{
	
	boolean power;
	int channel;
	
	void power() { power = !power; }
	
	void channelUp() { channel++; }
	
	void channelDown() { channel--; }
}

class SmartTv extends Tv{
	
	String text;
	boolean caption;
	
	void displayCaption(String text) {
		if(caption) {
			System.out.println(text);
		}
	}
}

	public static void main(String[] args) {
		
		// 다형성 미활용
		Tv t = new Tv();
		SmartTv stv = new SmartTv();
	}
```

* 다형성을 활용하기전에는 main에서 보듯이 인스턴스의 타입과 일치하는 타입의 참조변수만을 사용함.
* 부모는 부모의 인스턴스변수, 메서드를 사용, 자식은 부모, 자신의 인스턴스변수, 메서드에 접근하여 사용할 수 있었음.

* 다형성을 활용하면 아래와 같이 사용할 수 있음.
  
```java
public static void main(String[] args) {
		
		// 다형성 활용
		Tv tv = new SmartTv();
	}
```
* 부모 클래스의 타입 참조변수로 자식 클래스의 타입 인스턴스를 참조함.

#### 다형성 장점과 예제

```java
SmartTv stv = new SmartTv();
```

* 다형성을 사용하지 않았을 경우.
* SmartTv의 참조변수 객체 stv는 Tv의 기능 5개와 SmartTv 클래스 내에서의 기능 3개로 총 8개가 이용가능함.
  
```java
	//Tv
	boolean power;
	int channel;
	void power() { power = !power; }
	void channelUp() { channel++; }
	void channelDown() { channel--; }
	
	//SmartTv
	String text;
	boolean caption;
	void displayCaption(String text) {
		if(caption) {
			System.out.println(text);
		}
	}
```

```java
Tv tv = new SmartTv();
```

* 다형성을 사용했을 경우
* 부모클래스의 참조변수 객체 tv로 SmartTv 의 인스턴스를 만들었을때 인스턴스 기능은 8개지만 Tv의 기능 5개만 사용가능함.

#### 다형성 예제

```java
class Coffee {
    int price;

    public Coffee(int price) {
        this.price = price;
    }
}

class Americano extends Coffee {
    public Americano() {
        super(4000); // 상위 메서드 생성자 호출
    }
    // Object 클래스 toString() 메서드 오버라이딩
    public String toString() { 
        return "아메리카노";
    }
}

class CaffeLatte extends Coffee {
    public CaffeLatte() {
        super(5000);
    }
    // Object 클래스 toString() 메서드 오버라이딩
    public String toString() {
        return "카페라떼";
    }
}

class Customer {
    int money = 50000;

    // 커피 구매 메서드(다형성 활용)
    void buyCoffee(Coffee coffee) {
        if (money < coffee.price) {
            System.out.println("잔액이 부족합니다.");
            return;
        }
        money -= coffee.price;
        System.out.println(coffee + "를 구매하였습니다.");
    }

    /* 아메리카노, 카페라떼 구매 메서드를 따로 구현하지 않아도 됨
    void buyCoffee(Americano americano) {
        money -= americano.price;
    }

    void buyCoffee(CaffeLatte caffeLatte) {
        money -= caffeLatte.price;
    } */
}
```

* 개별적인 커피 구매 메서드를 따로 구현하지 않아도, 상위 클래스의 Coffee의 자료형만 매개변수로 받아 사용가능함.
* 밑의 예제를 하나 더 알아보자.
 
### 매개변수의 다형성

* 참조형 매개변수는 메서드 호출시, 자신과 같은 타입 또는 자식타입의 인스턴스를 넘겨줄 수 있음.

```java
public class Tv1 extends Product{
	
	public Tv1() {
		super(100);
	}
	
	public String toString() {
		return "tv";
	}
}

public class Buyer {

	int money = 1000;
	int bonusPoint = 0;
	
	void buy(Product p) {
		
		if(money < p.price) {
			System.out.println("잔액이 부족하여 물건 구매X");
			return;
		}
		money -= p.price;
		bonusPoint += p.bonusPoint;
		System.out.println(p + "을/를 구입하셨습니다.");
	}
}

public static void main(String[] args) {
	Buyer customer1 = new Buyer();

	customer1.buy(new Tv1());

	System.out.println("customer1 현재 남은 돈은 " + customer1.money + " 만원 입니다.");
	System.out.println("customer1 현재 보너스 점수는 " + customer1.bonusPoint + " 점 입니다.");
}

```

```
tv을/를 구입하셨습니다.
customer1 현재 남은 돈은 900 만원 입니다.
customer1 현재 보너스 점수는 10 점 입니다.
```

* 구매자 cutomer1을 객체로 만들어 cutomer1이 buy 메서드를 사용하고 있는 예제.
* customer1.buy(new Tv1()); 의 의미는 아래와 같음.
  * Product p = new Tv1();
  * customer1.buy(p);
* Tv객체를 만들고 p에 담아서 사용하는 것과 직접 Tv객체를 만들어 넣어주는 것과 같음. 헷갈리지 말자.
* 위의 예제 처럼 매개변수의 다형성은 buy 메서드 하나로만 사용하여 자식 클래스들이 사용가능한 유지보수의 용이성을 가지고 있음.
  
</div>
</details>

<details>
<summary style="font-size:20px">참조변수의 형변환, instanceof 연산자</summary>
<div markdown="1">

### 참조변수의 형변환

```java
public class CarMain {

	public static void main(String[] args) {
		
		FireEngine f = new FireEngine();
		Car c = f;						// 부모 Car타입 형변환 (생략가능)
		FireEngine f2 = (FireEngine)c;	// 자식인 FireEngine 타입으로 형변환 (생략불가), 컴파일 에러는 안나지만 실행시 에러가 남.
		Ambulance a = (Ambulance)f;		// 상속관계까 아닌 클래스 간은 형변환 불가.
	}
}
```

* FireEngine, Ambulance 는 Car를 상속받음.
* FireEngine 의 참조변수 f 에는 FireEngine 객체 생성한 주소를 담음.
* Car 의 참조변수 c는 f에 있는 주소를 참조함. (이 때 Car가 부모클래스이므로 형변환 생략이 가능함) 참조변수 c는 water 메서드는 사용 불가능함.
* FireEngine 의 참조변수 f2에는 f, c와 같은 메모리 주소를 참고하고있음. (이 때 자식클래스인 FireEngine타입으로 형변환은 생략이 불가능함.) 
* 상속관계가 아니면 당연히 클래스 간의 형변환은 불가함.

### instanceof 연산자

* 참조변수의 형변환 가능여부 확인에 사용하며 가능하면 true를 반환함.
* 참조변수 형변환을 할 떄는 형변환 여부를 먼저 파악한 후에 형변환을 하는 것이 바람직함.

```java
public class CarMain {

	public static void main(String[] args) {
		
		FireEngine f = new FireEngine();
		
		System.out.println(f instanceof Car);			// true
		System.out.println(f instanceof FireEngine);	// true
		System.out.println(f instanceof Object);		// true
		
	}
}
```

* 자기 자신도 참이 나오지만 부모클래스, 조상클래스에 대해서도 참 결과가 나오며 이는 형변환이 가능하다는 것임.
* 참조변수의 형변환은 왜 해야될까?
	* 참조변수를 변경함으로써 사용할 수 있는 멤버의 갯수를 조절하기 위함.
* instanceof 연산자는 언제 사용할까?
	* 참조변수를 형변환하기 전에 형변환 사용가능여부를 판단하기 위함.

</div>
</details>

<details>
<summary style="font-size:20px">추상 클래스</summary>
<div markdown="1">

### 추상클래스

* 클래스가 객체의 묶음으로 사용하는 설계도라면 추상 클래스는 미완성 설계도에 비유할 수 있음.
* 미완성 설계도로 완성된 제품을 만들 수 없듯이 추상 클래스로 인스턴스는 생성할 수 없음.

```java
abstract class Player{	// 추상 클래스 (미완성 클래스)

	boolean pause; 					// 추상 클래스도 변수를 가질 수 있음.
	int cuirrentPos;				// 추상 클래스도 변수를 가질 수 있음.

	Player(){						// 추상 클래스도 생성자가 있어야함.
		pause = false;
		currentPos = 0;
	}

	abstract void play(int pos);	// 추상 메서드(몸통이 없는 미완성 메서드)
	abstract void stop();			// 추상 메서드
}

Player p = new Player();  			// X, 에러남. 추상 클래스의 인스턴스는 생성 불가능.
```

* abstract가 붙은 class에는 abstract가 붙은 메서드가 있다고 생각할 수 있음.
* 추상메서드가 있으니 상속을 통해서 구현해주어야 하는 것을 알 수 있음.

```java
class AudioPlayer extends Player{
	void play(int pos){ ... }		// 추상 메서드 구현
	void stop() { ... }				// 추상 메서드 구현
}

AudioPlayer ap = new AudioPlayer();	// 상속을 통한 추상 클래스 객체 생성은 가능함.
```

* 상속을 통해 추상 메서드를 완성해야 인스턴스 생성 가능함.
* 추상클래스 왜 사용할까?
  * 꼭 필요하지만 자식클래스마다 다르게 구현될 것으로 예상하는 경우 사용함.
  * 새로운 클래스를 작성하는데 있어 아무 것도 없는 상태에서 시작하는 것보다는 틀을 갖춰서 시작하기 위함.
  * ex) 같은 크기 TV라도 기능에 따라서 모델이 여러 개 있지만, 설계도 90%정도는 동일시함.
  * 서로 다른 세 개 설계도를 그리는 것보다는 공통부분만 그린 미완성 설계도를 만들어 놓고, 이것을 이용해 완성하는 것이 효율적.

```java
abstract class AbstractPlayer extends Player{	// play, stop 두 가지 메서드 중 하나만 구현한 경우
	void play(int pos){ ... }
}
```

* 추상 클래스를 상속할 때 메서드를 두 개다 구현해야만 생각할 수 있음.
* 하지만 abstract 를 붙이면 미완성 클래스이므로 둘 중 하나만 구현하여 사용할 수도 있음.

#### 추상클래스 작성

* 추상클래스는 공통적으로 사용될 수 있는 클래스를 작성하기도 하고, 기존 클래스에서 공통적인 부분을 뽑아 추상클래스로 만들어 상속하기도 함.
* 추상클래스 예제를 통해 알아보자.

```java
package ch7;

public class AbstractTest {

	public static void main(String[] args) {
		
		Unit[] unit = { new Marin(), new Tank(), new Dropship()};
		
		for (int i = 0; i < unit.length; i++) {
			unit[i].move(100, 200);
		}
		
		Marin marin = new Marin();
		marin.stimPack();
		
		Tank tank = new Tank();
		tank.changeMode();
		
		Dropship dropship = new Dropship();
		dropship.load();
		dropship.unload();

	}
}

abstract class Unit {
	int x, y;
	abstract void move(int x, int y);
	void stop() {};
}

class Marin extends Unit{
	void move(int x, int y) {
		System.out.println("Marine x = " + x + ", y = " + y);
	}
	void stimPack() {
		System.out.println("Marin 스팀팩 사용");
	}
}

class Tank extends Unit{
	void move(int x, int y) {
		System.out.println("Tank x = " + x + ", y = " + y);
	}
	void changeMode() {
		System.out.println("Tank 모드 변경");
	}
}

class Dropship extends Unit{
	void move(int x, int y) {
		System.out.println("Dropship x = " + x + ", y = " + y);
	}
	void load() {
		System.out.println("Dropship 유닛 태우기");
	}
	void unload() {
		System.out.println("Dropship 유닛 내리기");
	}
}
```

```
Marine x = 100, y = 200
Tank x = 100, y = 200
Dropship x = 100, y = 200
Marin 스팀팩 사용
Tank 모드 변경
Dropship 유닛 태우기
Dropship 유닛 내리기
```

* 공통부모인 Unit 클래스 타입의 객체 배열을 통해 서로 다른 종류의 인스턴스를 하나의 묶음으로 다룸.
* 부모 클래스 Unit의 참조변수 unit을 통해 자손 타입의 인스턴스를 참조하므로 위와 같이 사용할 수 있음.
* 만약 최상위 Object 클래스에서 사용하고자하면 move메서드가 정의되지 않았기에 사용불가함.

#### 추상화된 코드의 장점

* 추상화된 코드는 구체화된 코드보다 유연함. (변경에 유리함)

```java
GregorianCalendar cal = new GregorianCalendar();	// 구체적
Calendar cal = Calendar.getInstance();				// 추상적

public static Calendar getInstance(Local aLocal){
	return createCalendar(TimeZone.getDefault(), aLocal);
}

private static Calendar createCalendar(Timezone zone, Local aLocale){
	//...
	if(caltype != null){
		switch(caltype){
			case "buddhist":
				cal = new BuddhistCalendar(zone, aLocal);
				break;
			case "japanese":
				cal = new JapaneseImperialCalendar(zone, aLocal);
				break;
			case "gregory":
				cal = new GregorianCalendar(zone, aLocal);
				break;
		}
	}
}
```

* 구체적으로 명시한 GregorianCalendar의 객체 cal은 하드코딩임. 다 고쳐야되는 문제점이 있음.
* 하지만 추상적으로 유연한 코드를 작성하면 코드를 건드리지않고 추가만하면되는 장점이 있음.

</div>
</details>

<details>
<summary style="font-size:20px">인터페이스</summary>
<div markdown="1">

### 인터페이스

* 추상 클래스는 추상 메서드를 가지고 있으나 인터페이스는 추상 메서드만 가질 수 있음. (상수도 가능)
* 인터페이스는 일종의 추상클래스라고도 하며 추상 클래스보다 추상화 정도가 높음.(추상 메서드의 집합이라고도 함)
* 추상 클래스와 달리 추상메서드와 상수만을 멤버로 가질 수 있음.
* 추상 클래스가 미완성 설계도라면 인터페이스는 밑그림만 있는 기본 설계도라고 할 수 있음.
* 모든 변수는 public (생략 가능), 상수만 올 수 있으며 구현부는 없고 선언부만 존재함.
* 인터페이스는 **추상 메서드의 집합이며 껍데기라고 알아두자.**

```java
interface Playground{
	publiuc static final int SPADE = 4;
	final int DIAMOND = 3;						// public static final int DIAMOND = 3;
	static int HEART = 2;						// public static final int HEART = 2;
	int CLOVER = 1;								// public static final int CLOVER = 1;

	public abstract String getCardNumber();
	String getCardKind();						// public abstract String getCardKind();
}
```

* 인터페이스는 모든 제어자가 public이며 편의성을 위해 생략 가능함.
* 상수는 static final 이 붙음.
* 인터페이스의 조상은 인터페이스만 가능함.(Object가 최고 조상이 아님)
* 다중 상속이 가능함. 추상 메서드는 선언부만 존재하므로 충돌해도 문제 없음

#### 인터페이스 구현

```java
class 클래스이름 implements 인터페이스이름{
	// 인터페이스에 정의된 추상메서드를 모두 구현해야함.
}

interface Fightable{
	void move(int x, int y);
	void attack(Unit u);
}

class Fighter implements Fightable{
	public void move(int x, int y) { ... };
	public void attack(Unit u) { ... };
}

// 추상 클래스와 마찬가지로 일부만 구현하는 경우, 클래스 앞에 abstract 를 붙여야함.
abstract class Fighter implements Fightable{
	public void move(int x, int y) { ... };
}
```

* 추상 클래스는 상속을 통해서 사용하지만, 인터페이스는 implements 를 통해서 구현함.
* 추상 클래스와 동일하게 일부의 메서드만 구현하고자 한다면 앞에 abstract 를 붙여서 사용함.

> 인터페이스 vs 추상클래스
>
> 인터페이스는 추상클래스보다 좀 더 추상화된 개념이며 인스턴스 변수, 생성자를 가질 수 없는 추상 메서드의 집합이며, 다중상속이 가능함.

#### 인터페이스를 이용한 다형성

* 부모 참조변수로 자식 객체를 가리키는 것이 다형성 ex) Tv t = new SmartTv();
* 인터페이스도 인터페이스 타입의 참조변수로 클래스의 인스턴스를 참조할 수 있으며 형변환도 가능함.

```java
class Fighter extends Unit implements Fightable{
	public void move(int x, int y) { .... };
	public void attack(Fightable f) { ... };
}

interface Fightable{
	void move(int x, int y);
	void attack(Fightable f);
}

Unit u = new Fighter();			// 부모 클래스 자손객체 참조
Fightable f = new Fighter();	// 인터페이스 자손객체 참조

f.move(100, 200);
f.attack(new Fighter());
```

* 참조변수 f를 사용할 떄에는 인터페이스에 선언해놓은 추상메서드만 사용가능함.
* **매개변수 타입이 인터페이스라는 것은 Fightable 인터페이스를 구현한 클래스의 인스턴스만 참조가능.**
* 인터페이스를 메서드의 리턴타입으로 지정할 수 있음.

```java 
Fightable method(){
	Fighter f = new Fighter();
	return f; 	
	// return new Fighter(); 와 같은 의미
}
```

* Fightable 인터페이스를 구현한 클래스의 인스턴스를 반환.
* 즉, 메서드의 반환타입이 인터페이스임.
  * 이것은 인터페이스 구현한 객체를 반환해야함.
  * 매서드를 호출하는 쪽에서는 반환타입과 일치하는 타입을 사용해야함.
  * 리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환하는 것을 의미함.

#### 인터페이스 장점

* 두 대상간의 연결, 대화, 소통을 돕는 중간 역할을 함. 
* 개발시간이 단축 가능함 - 메서드의 내용과 관계없이 선언부만 알면 프로그램 작성이 가능함.
* 독립적인 프로그래밍이 가능함 - 클래스의 선언과 구현을 분리함으로써 간접적인 관계로 변경하여 변경이 다른 클래스에 영향을 미치지 않음.

```java
class B{
	public void method(){
		System.out.println("methodB");
	}
}
```

* 위와 같이 껍데기 + 알맹이로 선언부와 구현부를 사용한 class B를 인터페이스를 이용했을 때

```java
interFace I{
	public void method();
}

class B implements I{
	public void method(){
		System.out.println("methodB");
	}
}
```

* 새로운 interface I를 만듬으로써 method() 를 선언부만 떼어네어 추상메서드로 구현함.
* 이렇게 했을 때 B 클래스가 I를 구현함으로써 선언부와 구현부를 분리하여 유연한 프로그래밍을 도와줌.
* 새로운 A 클래스가 들어와도 껍데기를 일치하게 사용함으로써 코드의 재사용성을 높여줌. (느슨한 결합)
   
#### 인터페이스 다형성 예제 

```java
class A{
	public void method(B b) {
		b.method();
	}
}

class B{
	public void method() {
		System.out.println("B클래스 메서드");
	}
}

class C{
	public void method() {
		System.out.println("C클래스 메서드");
	}
}

public class InterFaceTest {

	public static void main(String[] args) {
		
		A a = new A();
		a.method(new B());	// A가 B를 사용(의존 관계) C를 사용할 때 A와 B를 둘 다 수정해야함.
	}
}
```

* 클래스 A와 B가 있고 A는 B의 객체를 참조변수로 사용하며, method에는 B의 메서드를 호출하고있음.
* 이 때 클래스 C를 사용한다하면 클래스 A에 있는 B의 참조형 매개변수를 C로 고쳐야함. 
  
```java
package ch7;

class A{
	public void method(I i) {
		i.method();
	}
}
// B 클래스 선언과 구현을 분리함.
interface I{
	public void method();
}

class B implements I{
	public void method() {
		System.out.println("B클래스 메서드");
	}
}

class C implements I{
	public void method() {
		System.out.println("C클래스 메서드");
	}
}

public class InterFaceTest {

	public static void main(String[] args) {
		
		A a = new A();
		a.method(new C());
	}
}
```

* 코드를 위와 같이 바꾸어주면 class A는 interface i의 method를 호출하게됨.
* main에서 a의 객체에서 참조형 매개변수로 new C() 를 호출하므로 
* c의 인스턴스 주소가 호출되고 c에 있는 method 함수를 호출하게되어 C클래스 메서드가 출력됨.

#### 인터페이스의 디폴트 메서드와 static 메서드

* 인터페이스에 디폴트 메서드, static 메서드 기능 추가(JDK 1.8 부터)
* 인터페이스에 새로운 메서드를 추가하기 어려운 문제를 보완하고자 만들어짐.
  * 기능 새로 추가시 기존에 구현했던 클래스들 모두 구현해야한다는 단점을 dafult method를 통해 구현하자.

```java
interface MyInterface{
	void method();
	void newMethod();	// 추상 메서드
}

interface MyInterface2{
	void method();
	default void newMethod() { ... }
}
```

* newMethod() 기능을 새로 구현하고자하면 implements 했던 클래스들 모두 구현해야하기에
* 구현부, 선언부를 사용가능한 default void newMethod() { ... } 를 통해 구현하면 새로운 추상 메서드를 구현하지않고 사용가능함.
* 디폴트 메서드와 부모 클래스간의 충돌이 일어나면 부모 클래스의 메서드가 상속되고, 디폴트 메서드는 무시됨.
* **충돌났을 때는 오버라이딩 하자.**

</div>
</details>

<details>
<summary style="font-size:20px">내부 클래스, 익명 클래스</summary>
<div markdown="1">

### 내부 클래스

* 내부 클래스는 클래스 내에 선언된 클래스
* 클래스에 다른 클래스를 선언하는 이유는 두 클래스가 긴밀한 관계에 있기 때문임.
* 두 클래스의 멤버들 간에 쉽게 접근할 수 있고 불필요한 클래스를 감춤으로써 코드 복잡성을 줄일 수 있음.(캡슐화에 유리함)

```java
class A{	// 외부 클래스

	class B{	// 내부 클래스
		... // 객체 생성 없이도 A의 멤버에 접근 가능함.
	}
}
```

* B는 A의 내부 클래스 (inner class) 임.
* 내부 클래스 B는 외부 클래스 A를 제외하고 다른 클래스에서는 잘 사용되지 않는 것이어야함.

```java
package ch7;

class AA{	// AA는 BB의 외부 클래스
	int i = 5;
	BB b = new BB();
	class BB{	// BB는 AA의 내부 클래스
		void method() {
//			AA a = new AA();
//			System.out.println(a.i);
			System.out.println(i); 		// 객체 생성없이 외부 클래스 멤버 접근가능.
		}
	}
}
class CC{
	
//	BB b = new BB();	BB는 직접 접근 불가함. AA의 내부 클래스에 있으므로
}
public class InnterTest {

	public static void main(String[] args) {
//		BB b = new BB();
//		b.method();
		AA a = new AA();
		a.b.method();
	}

}
```

* BB 클래스를 AA의 내부 클래스로서 사용할 때 AA클래스의 객체 a를 만들어 a에 있는 b의 객체를 사용가능함.

#### 내부 클래스의 종류와 특징

```java
class Outer{
	int iv = 0;
	static int cv = 0;

	void myMethod(){
		int lv = 0;
	}
}

class Outer{
	class InstanceInner {}
	static class StaticInner {}

	void myMethod(){
		class LocalInner {}
	}
}
```

* 내부 클래스의 종류는 변수의 선언위치에 따른 종류와 같음.
* 변수를 선언하는 것과 같은 위치에 선언가능하며, 선언위치에 따라 인스턴스 변수, 클래스 변수로 나뉨.
* 내부 클래스는 네 종류가 있음.
  * 인스턴스 클래스 : 외부 클래스의 멤버 변수 선언위치에 선언함. 
  * 스태틱 클래스 : 외부 클래스의 static 멤버처럼 다루어짐.
  * 지역 클래스 : 외부 클래스의 메서드나 초기화 블럭 안에 선언됨.
  * 익명 클래스 : 일회용으로 사용하는 이름 없는 클래스

* 내부 클래스 역할은 변수의 특징과 유사함 (iv, cv, lv)

#### 내부 클래스의 제어자와 접근성

* 내부 클래스의 제어자는 변수에 사용 가능한 제어자와 동일함.

```java
class Outer{
	private class InstanceInner {}
	protected static class StaticInner {}

	void myMethod() {
		class LocalInner {}
	}
}
```

* 내부 클래스에서도 public, default, private, protected 전부 동일하게 사용가능함.
* 내부 클래스에서 static 멤버가 필요하면 내부 클래스를 static class 로 작성하면됨.
* 상수인경우에는 final static 으로 사용가능함.
* 내부 클래스에서는 외부 클래스의 private 멤버도 접근 가능함.
* 외부 클래스의 지역변수는 final이 붙은 상수만 접근 가능함.(JDK 1.8부터는 값이 안바뀌는 변수도 상수로 간주함)
  * 값이 바뀌지 않는 전제하에 final이 안붙어도 에러가 안남. (왠만하면 final 붙이자) 

### 익명 클래스

* 다른 내부 클래스들과 달리 이름이 없는 클래스
* 클래스의 선언과 객체의 생성을 동시에 하기 때문에 한번만 사용가능한 일회용 클래스임.

```java
new 부모클래스이름(){
	// 멤버 선언
}

new 구현인터페이스이름(){
	// 멤버 선언
}
```

* 익명 클래스는 이름이 없으므로 생성자를 가질 수 없으며, 상속받는 동시에 인터페이스를 구현할 수 없음.
* 오로지 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만 구현 가능함.

#### 익명 클래스 예제

```java

class EventHandler implements ActionListener{
	public void actionPerformed(ActionEvent e) {
		System.out.println("ActionEvent occurred");
	}
}

public class anonymousTest {

	public static void main(String[] args) {

		Button b = new Button("Start");
		b.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				System.out.println("ActionEvent occurred");
			}
		});
	}

}
```

* 위의 EventHandler 의 조상클래스인 ActionListener 를 익명클래스로써 구현한 것이 밑의 예제임.
* EventHadnler 라는 클래스를 일회용으로써 사용한다면 아래와 같이 익명클래스로써 구현하는 것이 코드의 간결화에 유리함.
* 익명 클래스는 람다에서도 다시 다루니 알고만 넘어가자.

</div>
</details>

<details>
<summary style="font-size:20px">예외 처리</summary>
<div markdown="1">

### 프로그램 오류 

* 프로그램 오류는 총 3가지로 나뉨.
  * 컴파일 에러 : 컴파일 시에 발생하는 에러 (자바 컴파일러가 구문체크, 번역, 최적화를 해줌)
  * 런타임 에러 : 실행 시에 발생하는 에러, 런타임 에러의 종류가 두 가지
    * 에러 : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류 (OutofMemoryError, StackOverflowError)..
    * 예외 : 프로그램 코드에 의해서 수습될 수 있는 미약한 오류 (Exception.. RuntimeException..)
  * 논리적 에러 : 실행은 되지만, 의도와 다르게 동작하는 것

#### 예외처리의 정의와 목적

* 정의 : 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드 작성.
* 목적 : 프로그램의 비정상적 종료를 막고, 정상적인 실행상태 유지.

### 예외 클래스의 계층 구조

![Alt text](image-2.png)

* 위 그림은 실행 시 발생할 수 있는 오류를 클래스로 정의한 그림임.
* 모든 클래스의 조상은 Object 이고, Exception, Error 클래스 또한 자식 클래스들임.

![Alt text](image-3.png)

* 모든 예외의 최고 조상은 Exception 클래스라는 상속계층도.
* RuntimeException 도 Exception 의 자식에 속함.
* Exception 클래스들과 자식들은 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외.
* RuntimeException 클래스들과 자식들은 프로그래머의 실수로 발생하는 예외.

### 예외 처리 try-catch 문

* 프로그램 런타임시 에러는 어쩔 수 없는 문제이고, 예외는 프로그래머가 처리가 가능한 부분임.
* 예외처리란 프로그램 실행 시 발생할 수 있는 예기치 못한 **예외의 발생에 대비한 코드를 작성**하는 것.

```java
public class ExceptionTest {

	public static void main(String[] args) {
		
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(0/0);
			System.out.println(4);
		} catch (ArithmeticException ae) {
			if(ae instanceof ArithmeticException) {
				System.out.println("true");
			}
			System.out.println("ArithmeticException!!");
		} catch(Exception e) {
			System.out.println("Exeption!!");
		}
		System.out.println(6);
	}
}
```
```
1
2
3
true
ArithmeticException!!
6
```

* 1, 2 출력 -> try문 3 까지 출력 후 0/0 으로 나누면 ArithmeticException 이 발생함.
* 4는 출력되지않고 catch 문에서 차례로 이동하며 맨 위에 ArithmeticException 이 발생했으므로 실행시키고
* Exception 의 catch 문은 실행시키지 않고 6을 출력하고 프로그램이 종료됨.
* Exception 은 최고 조상인 클래스이므로 제일 마지막 catch 블럭에 모든 예외처리를 진행해줌.

### printStackTrace() 와 getMessage()

* 예외가 발생했을 때 생성되는 예외 클래스의 인스턴스에는 발생한 예외에 대한 정보가 담겨 있음
* 이는 자주 사용되는 getMessage() 와 printStackTrace() 를 통해서 정보들을 얻을 수 있음.

* printStackTrace() - 예외발생시 호출 스택에 있던 **메서드의 정보와 예외 메시지**를 화면에 출력함
* getMessage() - 발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있음

### 멀티 catch 블럭

* catch 블럭을 | 기호를 사용하여 하나의 catch 블럭으로 합치는 것.
* JDK 1.7부터 가능함.

```java
try{
	catch (Exception A | Exception B e){
		e.printStackTrace();
	}
}
```

* 예외 클래스가 부모 자식 관계에 있으면 컴파일 에러 발생함.
* 부모 클래스의 예외만 써주는 것과 동일하기 때문에 불필요한 자식 클래스 예외는 제거하라는 뜻.

### 예외 발생시키기

```java
public class Ex8_6 {
	public static void main(String[] args) {
		
		try {
//			Exception e = new Exception("고의로 에러 발생시킴");
//			throw e;
			
			throw new Exception("고의로 에러 발생2");
		} catch (Exception e) {
			System.out.println("에러 메시지 : " + e.getMessage());
			e.printStackTrace();
		}
		System.out.println("프로그램 정상 종료");
	}
}
```

* 고의로 예외를 발생시킬 수 있는 방법도 존재함.
  * Exception e = new Exception("예외 메시지 입력 방법1");
  * throw e; 
  * 
  * throw new Exception("예외 메시지 입력 방법2")

### 메서드에 예외 선언하기

```java
void method() throws Exception1, Exception2 ... { ... };

void method() throws Exception { ... }	// 이 메서드는 모든 종류의 예외가 발생할 가능성이 있음.
```

* try-catch는 직접처리, 메서드 예외 선언은 예외를 떠넘기는 것.
* 예외를 처리하기 위해선 try-catch문을 사용하는 것이 일반적이지만 메서드에 선언하는 방법도 있음.
* 예외가 여러 개인 경우에는 쉼표로 구분하여 여러 개 적는 것도 가능함.
* 모든 예외의 최고 조상인 Exception 을 메서드에 선언하면 이 메서드는 모든 종류의 예외가 발생할 가능성이 있음.

```java
public class Ex8_6{
	public static void main(String[] args) throws Exception{
		method1();
	}
	
	static void method1() throws Exception{
		method2();
	}
	
	static void method2() throws Exception{
		throw new Exception();
	}
}
```
```
Exception in thread "main" java.lang.Exception
	at ch8.Ex8_6.method2(Ex8_6.java:14)
	at ch8.Ex8_6.method1(Ex8_6.java:10)
	at ch8.Ex8_6.main(Ex8_6.java:6)

```

* 메서드 호출 과정
  1. method2() 에서 throw new Exception() 문장으로 인해 예외가 강제적으로 발생했음.
  2. try-catch 문으로 예외처리를 하지 않았으므로, method2() 는 종료되며 자신을 호출한 method1() 에게 넘김.
  3. method1() 에서도 예외처리를 하지 않았으므로, 종료되면서 main에게 예외를 넘겨줌.
  4. main 메서드에서도 예외처리를 하지 않았으므로, main 메서드가 종료되며 프로그램이 비정상적으로 종료됨.

* 위의 예제 처럼 예외가 발생한 메서드에서 예외처리를 하지 않고 자신을 호출한 메서드에게 넘겨줄 수는 있지만,
* 이것으로 예외가 처리된 것은 아니고 단순히 전달만 하는 것임. 
* 결국 어느 한 곳에서는 반드시 try-catch 문으로 예외처리를 해주어야함.
* 예외가 선언되어 있으면 Exception 과 같은 checked(컴파일시 오류가 나는 에러) 예외는 try-catch 문으로 처리 하지 않아도 컴파일 에러가 발생하지 않음.

### 메서드 예외 선언하기 예제2

```java
package ch8;

import java.io.File;

public class Ex8_10 {

	public static void main(String[] args) {

		try {
			File f = createFile(args[0]);
			System.out.println( f.getName() + " 파일이 성공적 생성");
		} catch (Exception e) {
			System.out.println(e.getMessage() + " 다시 입력");
		}
	}
	
	static File createFile(String fileName) throws Exception {
		
		if(fileName == null || fileName.equals("")) {
			throw new Exception("파일이름이 유효하지 않음.");
		}
		File f = new File(fileName);
		f.createNewFile();
		return f;
	}

}
```
```
파일이름이 유효하지 않음. 다시 입력
```

* args[0] 에 null이나 "" 을 입력하고 파일 생성 시에 if문에서 예외가 발생 
* main문의 catch문으로 이동하여 결과와 같은 내용이 출력됨.

### finally 블럭

```java
try{
	// 예외가 발생할 가능성이 있는 문장
}catch(Exception e){
	// 예외 처리 문장
}finally{
	// 예외의 발생여부에 관계없이 항상 수행되는 문장
	// finally는 try catch문의 맨 마지막에 위치해야함.
}
```

* try 블럭 안에 return 문이 있어서 try 블럭을 벗어나갈 때도 finally 블럭이 실행됨.
* 임시파일을 삭제하는 메서드가 여러 개인 경우, 이 때 finally 문에서 하나 적어줌으로써 코드중복을 제거함.

### 사용자 정의 예외 만들기

* 기존에 정의된 예외 클래스 외에 필요에 따라 프로그래머가 새로운 예외 클래스를 정의하여 사용 가능함.
* 보통은 Exception 클래스 또는 RuntimeException 클래스로부터 상속받는 클래스를 만듬.
* Exception 은 사용자가 발생시키는 예외, RuntimeException 은 프로그래머의 실수로 발생시키는 예외
* 선택처리 unchekced가 가능한 RuntimeException 을 사용하고 Exception은 chekced 필수처리이므로 사용을 지양하자.

```java
class MyException extends Exception {
	MyException(String msg){	// 문자열을 매개변수로 받는 생성자
		super(msg);				// 조상인 Exception 클래스의 생성자 호출
	}
}
```

### 연결된 예외

* 한 예외가 다른 예외를 발생시키는 경우
* 예외 A가 예외 B를 발생시키면 A를 B의 원인 예외라고 함.

```java
void install() throws InstallException {
	try{
		startInstall();
		copyFiles();
	}catch (SpaceException e){
		InstallException ie = new InstallException("설치중 예외발생");
		ie.initCause(e);
		throw ie;
	}catch (MemoryException me){
		...
	}
}
```

* startInstall() 메서드에서 저장공간 부족으로 SpaceException 예외 발생.(예외 A라 가정)
* 새로운 예외 InstallException ie = new InstallException 생성 (예외 B라 가정)
* 예외B의 원인 예외를 예외A로 지정 하여 예외 B를 발생시킴
* 연결된 예외는 왜 써야될까?
  * 여러 예외를 하나로 묶어서 사용할 때
  * checked 예외를 unchecked 예외로 변경할 때

</div>
</details>

<details>
<summary style="font-size:20px">java.lang 패키지, util 클래스</summary>
<div markdown="1">

### java.lang 패키지

* java.lang 패키지는 가장 기본이 되는 클래스들을 포함하여 import문 없이도 사용할 수 있음.
* java.lang 패키지에서 자주 사용되는 클래스들을 알아보자.

#### Object 클래스

```java
public boolean equals(Object obj){
	return;
}
```

* Object 클래스는 모든 클래스의 최고 조상이므로 클래스에서 바로 사용가능함.
* Object 클래스의 equals 메서드는 매개변수로 객체의 참조변수를 받아서 비교하여 결과를 boolean으로 알려 주는 역할.
* 자주 사용하는 Object 클래스 메서드를 알아보자.

#### Object 클래스 - equals()

```java
class Value{
	int value;
	
	public Value(int value) {
		this.value = value;
	}
}

public class Ex9_1 {

	public static void main(String[] args) {
		
		Value v1 = new Value(10);
		Value v2 = new Value(10);
		
		if(v1.equals(v2)) {
			System.out.println("v1와 v2는 같습니다.");
		}else {
			System.out.println("v1와 v2는 다릅니다.");
		}
	}
}
```

* equals 메서드는 주소값으로 비교를 하기 때문에 멤버변수값이 10으로 같을지라도 결과는 false임.
* Object 클래스로부터 상속받은 equals 메서드는 참조변수에 저장된 값이 같은지를 판단하는 기능밖에 할 수 없음.
* 그렇다면 객체의 주소값을 비교하는게 아니라 value 값을 비교하는게 방법은 어떻게 할까?

#### equals() 오버라이딩

```java
class Person{
	
	long id;
	
	public Person(long id) {
		this.id = id;
	}
	
	public boolean equals(Object obj) {
		
		if(obj instanceof Person) {
			return id == ((Person)obj).id;
		}else {
			return false;
		}
	}
}

public class Ex9_2 {

	public static void main(String[] args) {
		
		Person p1 = new Person(8011222L);
		Person p2 = new Person(8011222L);
		
		if(p1.equals(p2)) {
			System.out.println("p1과 p2는 같은 사람입니다.");
		}else {
			System.out.println("p1과 p2는 다른 사람입니다.");
		}
	}
}
```

* equals 메서드가 Person 인스턴스 주소값이 아닌 id를 참고하기 위해 equals 메서드를 오버라이딩함.
* 서로 다른 인스턴스라도 같은 id를 가지고 있으면 재정의한 equals 메서드로 true 결과를 얻게 할 수 있음.

#### Object 클래스 - hashCode()

```java
public class Object{
	public native int hashCode();	// native 란 os가 가지고 있는 메서드
}
```

* hashCode() 메서드는 해싱기법에 사용하는 해시함수를 구현한 것임.
* 객체의 해시코드를 반환하는 메서드
* 내용이 없으며 객체의 주소를 int로 변환해서 반환해줌.
* equals()를 오버라이딩하면 hashCode() 도 오버라이딩 해주는게 바람직함.
* 왜냐하면 equals() 결과가 true인 두 객체의 해시코드가 같아야하기 때문임.
  
```java
	public static void main(String[] args) {
		String str1 = new String("abc");
		String str2 = new String("abc");
		
		System.out.println(str1.hashCode());
		System.out.println(str2.hashCode());
		System.out.println(System.identityHashCode(str1));
		System.out.println(System.identityHashCode(str2));
	}
```
```
96354
96354
1521118594
1940030785
```

* String 클래스는 문자열의 내용이 같으면 동일한 해시코드를 반환하도록 오버라이딩되어있음.
* 반면에 System.indentityHashCode 는 객체의 주소값으로 해시코드를 생성하기 떄문에 다른 해시코드값을 반환함.

#### Object 클래스 - toString()

```java
public String toString(){
	return getClass().getName()+"@"+Ineger.toHexString(hashCode());
}
```

* 인스턴스에 대한 정보를 문자열로 제공할 목적으로 정의한 메서드.
* toString() 메서드를 오버라이딩 하지 않으면 클래스이름과 16진수의 해시코드의 결과값이 나옴.

```java
import java.util.Objects;

class Card{
	
	String kind;
	int num;
	
	public Card() {
		this("SPADE", 5);
	}

	public Card(String kind, int num) {
		this.kind = kind;
		this.num = num;
	}
	
	@Override
	public String toString() {
		return kind + "," + num;
	}
	
	public boolean equals(Object obj) {
		if(!(obj instanceof Card)) {
			return false;
		}
		Card c = (Card)obj;
		
		return this.kind.equals(c.kind) && this.num == c.num;
	}
	
	public int hashCode() {
		return Objects.hash(kind, num);
	}
	
}

public class Ex9_5 {

	public static void main(String[] args) {
		
		Card card1 = new Card();
		Card card2 = new Card("SPADE", 5);
		
		System.out.println(card1);
		System.out.println(card2);
		
		System.out.println(card1.equals(card2));
		System.out.println(card1.hashCode());
		System.out.println(card2.hashCode());
	}
}
```
```
SPADE,5
SPADE,5
true
-1842861215
-1842861215
```

* toString 메서드를 오버라이딩 할 때는 Object 의 접근 제어자보다 같거나 넓어야하기때문에
* 오버라이딩 할 때 public 으로 했다는 것을 눈 여겨 보자.
* equals 를 오버라이딩하면 hashCode도 Objects.hash 를 통해서 같은 값이 나와야함.

#### String 클래스

* String 클래스는 문자열을 저장하고 이를 다루는데 필요한 메서드를 함께 제공함.
* String 클래스 = 데이터(char[]) + 메서드(문자열 관련)

```java
public final class String implements java.io.Serializable, Comparable {
	private char[] value;
	...
}
```

```java
String a = "a";
String b = "b";
a = a + b;
```

* 내용을 변경할 수 없는 불변 클래스
* 기존 a가 ab로 바뀌는게 아니라 새로운 문자열 ab가 만들어지므로 덧셈 연산자를 통한 문자열 결합은 성능이 떨어짐.
* 문자열의 결합이나 변경이 잦으면, 내용을 변경가능한 StringBuffer 을 사용하는게 성능이 더 좋음.
* 반복문을 통해서 문자열을 지속적으로 결합하는 경우에는 StringBuffer 를 사용하자.

### 문자열 비교

* 문자열을 만들 때는 두 가지 방법, 문자열 리터럴을 지정하는 방법과 String 클래스의 생성자를 사용해서 만드는 방법이 있음.

```java
public class ex9_6 {

	public static void main(String[] args) {
		
		String str1 = "abc";
		String str2 = "abc";
		
		System.out.println("str1 == str2 : " + (str1 == str2));
		System.out.println("str1.equals(str2) : " + str1.equals(str2));
		
		String str3 = new String("abc");
		String str4 = new String("abc");
		
		System.out.println("str3 == str4 : " + (str3 == str4));
		System.out.println("str3.equals(str4) : " + str3.equals(str4));
	}
}
```
```
str1 == str2 : true
str1.equals(str2) : true
str3 == str4 : false
str3.equals(str4) : true
```

* str1과 str2는 문자열 "abc" 를 가르킴. 하나의 문자열을 여러 참조변수가 공유함.
* str3과 str4는 각각의 문자열 "abc" 를 가르킴. 항상 새로운 문자열이 만들어짐.
* 문자열 내용비교를 할 때는 equals를 사용하고 주소를 비교 할 때는 == 를 사용하자.
* 왜 그런지 문자열 리터럴을 통해서 알아보자.

#### 문자열 리터럴

* 프로그램 실행시 자동으로 생성됨. String은 클래스이므로 객체를 생성해야하나 문자열 리터럴은 자동으로 상수 저장소에 만들어짐.(constant pool 에 저장)
* 같은 내용의 문자열 리터럴은 String 객체이고 하나만 만들어짐. 

```java
public static void main(String[] args) {
	String s1 = "AAA";
	String s2 = "AAA";
	String s3 = "AAA";
	String s4 = "BBB";
}
```
![Alt text](image-4.png)

* s1, s2, s3가 만들어진 String 불변의 객체를 공유함.
* 내용을 변경할 수는 없으므로 하나의 문자열을 여러 참조변수가 공유함.
  
#### 문자열 기본형간의 변환

* 숫자 -> 문자

```java
int i = 100;
System.out.println(i + "");
System.out.println(String.valueOf(i));	// 속도가 더 빠름, 성능 향상이 필요할 경우 사용하자.
```

* 문자 -> 숫자

```java
System.out.println(Integer.parseInt("100"));
System.out.println(Integer.valueOf("100"));
```

#### StringBuffer 

```java
public final class StringBuffer implements java.io.Serializable {
	private char[] value;
}
```

* String 클래스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 StringBuffer 클래스는 변경이 가능함.
* 내부적으로 문자열 편집을 위한 buffer를 가지고 있으며 인스턴스를 생성할 때 그 크기를 지정할 수 있음.
* 문자열가지고 조작가능한 경우는 StringBuffer를 사용하자.
* String 클래스는 불변, StringBuffer 클래스는 가변

```java
StringBuffer sb = new StringBuffer("abc");
sb.append("123").append("zz");

abc123zz 결과 출력
```

* StringBuffer는 equals(). 가 오버라이딩되어있지 않음. (주소비교)

```java
String Buffer sb = new StringBuffer("abc");
String Buffer sb2 = new StringBuffer("abc");

System.out.println(sb=sb2);				// false
System.out.println(sb.equals(sb2));		// false

String s = sb.toString();	// sb를 String으로 변환 해줘야함
String s2 = sb2.toString();

System.out.println(s.equals(s2));	// true
```

#### StringBuilder

* StringBuilder는 StringBuffer와 유사하나 StringBuffer는 동기화 되어있고, StringBuilder는 동기화되어있지않음.
* StringBuffer는 멀티쓰레드에 안전하고, 동기화는 StringBuffer 의 성능을 떨어뜨림.
* 싱글쓰레드에서는 StringBuilder를 사용하면 성능 향상.
  
> StringBuffer는 동기 StringBuilder는 비동기, 멀티쓰레드인 경우 StringBuffer, 싱글쓰레드인경우 StringBuilder 사용하자.

</div>
</details>

<details>
<summary style="font-size:20px">String 클래스의 생성자와 메서드</summary>
<div markdown="1">

* 주로 사용되는 String 생성자와 메서드를 직접 사용해보자. 실무, 코테에서도 번번히 쓰이니 이런 것이 있다는 것만 알아두기.

```java
		//String(String s) - 주어진 문자열(s)을 갖는 String 인스턴스 생성
		String s1 = new String("Hello");
		System.out.println(new String(s1));		// Hello
		
		//String(char[] value) - 주어진 문자열(value)을 갖는 String 인스턴스 생성
		char[] c = {'H', 'e', 'l', 'l', 'o'};
		System.out.println(new String(c));		// Hello
		
		//String(StringBuffer buf) - StringBuffer 인스턴스가 갖고 있는 문자열과 같은 내용의 String 인스턴스 생성
		StringBuffer sb = new StringBuffer("Hello");
		System.out.println(new String(sb));		// Hello
		
		//char charAt(int index) - 지정된 위치에 있는 문자를 알려줌
		System.out.println("Hello".charAt(1));	// e
		System.out.println("012345".charAt(1));	// 1
		
		//int compareTo(String str) - 문자열(str) 과 사전순서 비교, 같으면 0 이전이면 음수 이후면 양수 반환
		System.out.println("aaa".compareTo("aaa"));		// 0
		System.out.println("aaa".compareTo("bbb"));		// -1
		System.out.println("bbb".compareTo("aaa"));		// 1
		
		//String concat(String str) - 문자열(str) 을 뒤에 덧붙임
		System.out.println("Hello".concat("Java"));	// HelloJava
		
		//boolean contains(CharSequence s) - 지정된 문자열이 포함되어있는지 검사
		System.out.println("abcdefg".contains("bc"));		// true
		
		//boolean endsWith(String suffix) - 지정된 문자열 suffix로 끝나는지 검사
		System.out.println("Hello.txt".endsWith("txt")); 	// true
		
		//boolean equalsIgonreCase(String str) - 대소문자 구분없이 비교
		System.out.println("Hello".equalsIgnoreCase("HELLO"));		// true
		System.out.println("Hello".equalsIgnoreCase("HELLo"));		// true
		
		//int indexOf(int ch) - 문자ch가 문자열에 존재하는지 확인 후 위치를 알려줌 못찾으면 -1 반환
		System.out.println("Hello".indexOf('o'));	// 4
		System.out.println("Hello".indexOf('k'));	// -1
		
		//String replace(char old, char new) - 문자열 중의 문자 old를 새로운 문자 new 로 치환
		System.out.println("Hello".replace('H', 'C'));	//Cello
		
		//String[] split(String regex) - 분리자 regex로 나누어 문자열 배열에 담아 반환
		String[] arr = "dog,cat,bear".split(",");
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);		//dog,cat,bear
		}
		
		//String substring(int begine, int end) - 시작부터 끝 위치 범위 포함 문자열 
		System.out.println("java.lang.Object".substring(2,5)); 	// va.

		그 밖에 등등... toLowercase(), toUpperCase(), trim()
```

</div>
</details>

<details>
<summary style="font-size:20px">날짜의 시간 & 형식화</summary>
<div markdown="1">

java 1.8부터는 java.time 패키지를 제공하지만 그 전의 버전들은 Calendar, Date를 써오고 있기에 가볍게 알아보고 가자.
  
### Calendar 클래스

```java
Calendar cal = Calendar.getInstance();	

public static void main(String[] args)   {
		
		Calendar cal = Calendar.getInstance();
		
		System.out.println(cal.get(Calendar.YEAR));
	
		// cal.get 으로 Calendar 클래스의 인스턴스 메서드 함수 호출 가능.
		// YEAR, MONTH, WEEK_OF_YEAR, HOUR, MINUTE 등등..
	}
```

* Calendar은 추상클래스이기 때문에 직접 객체를 생성하지 않고, 메서드를 통해 구현된 클래스의 인스턴스를 얻어야함.

#### Calendar 예제1

```java
public static void main(String[] args)   {
	
	Calendar cal = Calendar.getInstance();
	
	System.out.println("이 해 년도 : " + cal.get(Calendar.YEAR));
	System.out.println("월(0~11), 0:1월 : " + cal.get(Calendar.MONTH));
	System.out.println("이 해의 몇 째 주 : " + cal.get(Calendar.WEEK_OF_YEAR));
	System.out.println("이 달의 몇 째 주 : " + cal.get(Calendar.WEEK_OF_MONTH));
	System.out.println("이 달의 몇 일 : " + cal.get(Calendar.DATE));
	System.out.println("이 달의 몇 일 : " + cal.get(Calendar.DAY_OF_MONTH));
	System.out.println("이 해의 몇 일 : " + cal.get(Calendar.DAY_OF_YEAR));
	System.out.println("요일(1~7, 1:일요일) : " + cal.get(Calendar.DAY_OF_WEEK));
	System.out.println("이 달의 몇 째 요일 : " + cal.get(Calendar.DAY_OF_WEEK_IN_MONTH));
	System.out.println("오전_오후 (0: 오전, 1: 오후) : " + cal.get(Calendar.AM_PM));
	System.out.println("시간(0~11) : " + cal.get(Calendar.HOUR));
	System.out.println("시간(0~23) : " + cal.get(Calendar.HOUR_OF_DAY));
	System.out.println("분(0~59) : " + cal.get(Calendar.MINUTE));
	System.out.println("초(0~59) : " + cal.get(Calendar.SECOND));
	System.out.println("1000분의 1초(0~999) : " + cal.get(Calendar.MILLISECOND));
	System.out.println("이 달의 마지막 날 : " + cal.getActualMaximum(Calendar.DATE));
}
```
```
이 해 년도 : 2023
월(0~11), 0:1월 : 9
이 해의 몇 째 주 : 41
이 달의 몇 째 주 : 2
이 달의 몇 일 : 10
이 달의 몇 일 : 10
이 해의 몇 일 : 283
요일(1~7, 1:일요일) : 3
이 달의 몇 째 요일 : 2
오전_오후 (0: 오전, 1: 오후) : 1
시간(0~11) : 2
시간(0~23) : 14
분(0~59) : 36
초(0~59) : 3
1000분의 1초(0~999) : 950
이 달의 마지막 날 : 31
```

#### Calendar 예제2

```java
public static void main(String[] args) {
	
	// 요일은 1부터 일요일이므로 0번째 배열은 공백
	final String[] DAY_OF_WEEK = {"", "일", "월", "화", "수", "목", "금", "토"};
	
	Calendar date1 = Calendar.getInstance();
	Calendar date2 = Calendar.getInstance();
	
	date1.set(2019, 3, 29);
	System.out.println("date1은 " + toString(date1) + DAY_OF_WEEK[date1.get(Calendar.DAY_OF_WEEK)]+ "요일이고,");
	System.out.println("date2은 " + toString(date2) + DAY_OF_WEEK[date2.get(Calendar.DAY_OF_WEEK)]+ "요일입니다.");
	
	// 두 날짜간의 차이
	long difference = (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
	System.out.println("그 날(date1)부터 지금(date2)까지 " + difference +"초가 지났습니다.");
	System.out.println("일(day)로 계산하면 " + difference / (24*60*60) + "일 입니다.");
}

public static String toString(Calendar date) {
	return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH)+1) + "월 "
				+ date.get(Calendar.DATE) + "일 ";
}
```
```
date1은 2019년 4월 29일 월요일이고,
date2은 2023년 10월 10일 화요일입니다.
그 날(date1)부터 지금(date2)까지 140400000초가 지났습니다.
일(day)로 계산하면 1625일 입니다.
```

#### Calendar 예제3

```java
public static void main(String[] args) {
	final int[] TIME_UNIT = {3600, 60, 1};
	final String[] TIME_UNIT_NAME = {"시간 ", "분 ", "초 "};
	
	Calendar time1 = Calendar.getInstance();
	Calendar time2 = Calendar.getInstance();
	
	time1.set(Calendar.HOUR_OF_DAY, 10);
	time1.set(Calendar.MINUTE, 20);
	time1.set(Calendar.SECOND, 30);
	
	time2.set(Calendar.HOUR_OF_DAY, 20);
	time2.set(Calendar.MINUTE, 30);
	time2.set(Calendar.SECOND, 10);
	
	System.out.println("time1 : " + time1.get(Calendar.HOUR_OF_DAY) + "시 "
			+ time1.get(Calendar.MINUTE) + "분 " + time1.get(Calendar.SECOND) + "시");
	System.out.println("time2 : " + time2.get(Calendar.HOUR_OF_DAY) + "시 "
			+ time2.get(Calendar.MINUTE) + "분 " + time2.get(Calendar.SECOND) + "시");
	
	long difference = Math.abs(time2.getTimeInMillis() - time1.getTimeInMillis())/1000;
	
	String tmp = "";
	for (int i = 0; i < TIME_UNIT.length; i++) {
		tmp += difference/TIME_UNIT[i] + TIME_UNIT_NAME[i];
		difference %= TIME_UNIT[i];
	}
	System.out.println("time1과 time2의 차이는 " + difference + "초 입니다.");
	System.out.println("시분초를 변환하면" + tmp + " 입니다.");
}
```
```
time1 : 10시 20분 30시
time2 : 20시 30분 10시
time1과 time2의 차이는 0초 입니다.
시분초를 변환하면 10시간 9분 40초 입니다.
```

### DecimalFormat

```java
double number = 1234567,89;
DecimalFormat df = new DecimalFormat("#.#E0");
String result = df.format(number)	// 1.2E6
```

### SimpleDateFormat

실제 실무에서 자주 클래스.
주로 사용자가 원하는 엑셀 형식으로 변환해줄 때 사용했음.

```java
Date today = new Date();
SimepleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");

// 오늘 날짜를 yyyy-MM-dd 형태로 변환하여 반환함.
String result = df.format(today);
```
</div>
</details>

<details>
<summary style="font-size:20px">컬렉션 프레임웍</summary>
<div markdown="1">

### 컬렉션 프레임웍

**여러번 반복, 빠르게 전체적으로 다시 보고**
**실습을 통해 어떻게 언제 쓰는지 파악하면서 공부하기**

* 컬렉션 : 여러 객체(데이터)를 모아 놓은 것을 의미함.
* 프레임웍 : 표준화, 정형화된 체계적인 프로그래밍 방식.
* 컬렉션 프레임웍 : 데이터 군을 저장하는 클래스들을 표준화한 설계를 뜻함.

#### 컬렉션 프레임웍 핵심 인터페이스

1. List
   * 순서가 있는 데이터 집합, 데이터의 중복을 허용함. ex) ArrayList, LinkedList, Stack, Vector 등..
2. Set
   * 순서가 없는 데이터 집합, 데이터의 중복을 허용하지 않음 ex) HashSet, TreeSet 등..
3. Map
   * 키(key) 와 값 (value) 의 쌍으로 이루어진 데이터의 집합, 순서는 유지되지 않고, 키는 중복을 허용하지 않고, 값은 중복을 허용함. ex) HashMap, TreeMap 등..

* List, Set은 Collection 에 속하고 Map은 속하지 않음.

#### List, Set, Map 인터페이스

* List 인터페이스의 주요 인터페이스 : ArrayList, LinkedList
  * 주요 메서드 : add, get, indexOf, remove, set, sort ...
* Set 인터페이스 주요 인터페이스 : HashSet, TreeSet 
  * 주요 메서드 : Collections 인터페이스와 동일
* Map 인터페이스 주요 인터페이스 : HashMap, TreeMap 
  * 주요 메서드 : put, putAll, remove, containsKey, containsValue, get, entrySet, keySet, values

### ArrayList

* 가장 많이 사용되는 컬렉션 클래스, List 인터페이스를 구현하기 때문에 순서유지, 중복허용의 특징이 있음.

```java
public class ArrayList extends AbstractList implements List, RandomAcess, Cloneable, java.io.Serializable {
	...
	trasient Object[] elementData;
}
```

* ArrayList는 elementData 이름의 Object 배열을 멤버변수로 선언하고 있어서 모든 종류의 객체를 담을 수 있음.

#### ArrayList 메서드

* 추가,삭제 메서드 : add, addAll, remove, removeAll, clear
* 검색 메서드 : indexOf, contains, get, set, toArray(), isEmpty(), trimToSize(), size()

#### ArrayList 예제

```java
public class Ex11_1 {
	@SuppressWarnings("deprecation")
	public static void main(String[] args) {
		
		 // 기본 길이 10인 ArrayList 생성
		 ArrayList list1 = new ArrayList(10);
		 // list1에는 객체만 저장가능함, autoboxing 에 의해 기본형 -> 참조형으로 자동 변환됨.
		 list1.add(new Integer(5));
		 list1.add(new Integer(4));
		 list1.add(new Integer(2));
		 list1.add(new Integer(0));
		 list1.add(new Integer(1));
		 list1.add(new Integer(3));
		 
		 ArrayList list2 = new ArrayList(list1.subList(1, 4));
		 
		 printed(list1, list2);
		 
		 // Collections.sort 는 리스트의 정렬
		 // Collection 은 인터페이스, Collections는 유틸 클래스
		 Collections.sort(list1);
		 Collections.sort(list2);
		 
		 printed(list1, list2);
		 
		 // list1을 포함하면 true
		 System.out.println("list1.containsAll(list2) : " + list1.containsAll(list2));
		 
		 list2.add("B");
		 list2.add("C");
		 list2.add(3, "A");
		 printed(list1, list2);
		 
		 list2.set(3, "AA");
		 printed(list1, list2);
		 
		 // 지정된 객체의 위치 반환
		 list1.add(0, "1");
		 System.out.println("list1.indexOf(1) : " + list1.indexOf(2));
		 printed(list1, list2);
		 // 지정된 객체의 위치 삭제
		 list1.remove(0);
		 
		 // list1에서 list2 겹치는 부분만 제외하고 나머지 삭제
		 System.out.println("list1.retainAll(list2) : " + list1.retainAll(list2));
		 printed(list1, list2);
	}

	private static void printed(ArrayList list1, ArrayList list2) {
		System.out.println("list1 : " + list1);
		System.out.println("list2 : " + list2);
		System.out.println();
	}
}
```

#### ArrayList 예제2

```java
public class ArrayListEx1 {

	public static void main(String[] args) {
		
		// 5명의 사람의 이름을 입력 받아 ArrayList에 저장 후 이들 중 '김'씨 성을 가진 사람 출력 
		
		ArrayList<String> list = new ArrayList<String>();
		Scanner sc = new Scanner(System.in);
		
		for (int i = 0; i < 5; i++) {
			list.add(sc.next());
		}

		for (int i = 0; i < list.size(); i++) {
			String name = list.get(i);
			if(name.startsWith("김")) {
				System.out.println(name);
			}
		}
	}
}

```

#### ArrayList 추가와 삭제

* ArrayList의 요소를 삭제하는 경우, 삭제할 객체의 바로 아래에 있는 데이터를 한 칸씩 위로 복사해서 덮어쓰는 방식으로 처리함.
* 만일 삭제할 객체가 마지막 데이터라면, 복사할 필요 없이 단순히 null로 변경해주면 됨.
 
```java
public class Ex11_2 {

	public static void main(String[] args) {
		
		ArrayList<Integer> list = new ArrayList<Integer>();
		
		for (int i = 0; i < 5; i++) {
			list.add(i);
		}
		
//		for (int i = 0; i < 5; i++) {
//			list.remove(new Integer(i));
//		}
		
		for (int i = list.size()-1; i >= 0; i--) {
			list.remove(i);
		}
	}
}
```

* remove 는 i번째 인덱스에 있는 위치의 객체를 제거하기 때문에 마지막에 저장된 것부터 삭제해주자.
* 배열의 중간에 위치한 객체를 추가하거나 삭제하는 경우는 작업시간이 오래 걸리므로 성능이 많이 저하됨.

### LinkedList

* LinkedList는 불연속적으로 존재하는 데이터를 서로 연결한 형태로 구성되어있음.

![Alt text](image-5.png)

* LinkedList는 각기 노드마다 화살표로 연결되어 리스트 형태로 나열되어있음.
* 노드는 하나의 객체이고, 객체를 만들면 객체의 주소가 생기게 되는데, 노드마다 각기 객체의 주소를 참고함으로써 연결 형태를 구성함.

```java
class Node{
	Node next;		// 다음 요소의 주소를 저장
	int data;		// 데이터를 저장
}
```

* 데이터의 추가 삭제에 용이하다는 장점
* 데이터 n번째 데이터까지 차례대로 따라가면서 읽어야하므로 데이터를 읽는 시간은 느리다는 단점.
* 이를 보완하고자 한 것이 doubly linkted list (양방향 연결 리스트) 임. (여전히 탐색은 n의 시간복잡도)
* 자바의 linkedlist 는 양방향 연결 리스트로 구현되어있음.

![Alt text](image-6.png)

```java
class Node{
	Node next;		// 다음 요소의 주소를 저장
	Node prev;		// 이전 노드 주소를 저장
	int data;		// 데이터를 저장
}
```

![Alt text](image-7.png)

* 순차적으로 데이터를 추가/삭제 - ArrayList 가 빠름
* 비순차적으로 데이터를 추가/삭제 - LinkedList 가 빠름
* 접근시간 - ArrayList 가 빠름
* FIFO 선입선출이 빈번할 경우, 큐를 사용해야할 때 LinkedList를 사용한다라고 말하지만,
* 외국 사례에선 LinktedLIst 를 사용하는 사례보다 그냥 ArrayList를 사용하는 사례가 많다고함. (성능상으로 큰 차이 X)
  
### Stack, Queue

#### Stack

![Alt text](image-10.png)

* 상자에 물건을 쌓아 올리듯이 데이터를 쌓는 자료 구조
* LIFO(Last In First Out) 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 구조

#### Stack 메서드

1.	boolean empty() : Stack이 비어있는지 확인
2.	Object peek() : Stack의 맨 위에 저장된 객체 반환, pop()과 달리 객체는 꺼내지 않음. 비었을 때 EmptyStackException 발생
3.	Object pop() : Stack의 맨 위에 저장된 객체를 꺼냄, 비었을 때 EmptyStackException 발생
4.	Object push(Object item) : Stack에 객체를 저장
5.	int search(Object o) : Stack에서 주어진 객체를 찾아서 위치를 반환

#### Quque

![Alt text](image-9.png)

* 줄을 지어 순서대로 처리되는 자료구조
* FIFO(First In FIrst Out) 먼저 들어온 데이터가 가장 먼저 나가는 구조
* Queue는 인터페이스로 정의되어있어 객체로 쓰고자 할 때는 클래스를 직접 구현하던가, 구현한 클래스를 사용해야함.

#### Queue 메서드

1.	boolean add(Object o) : 지정된 객체 Queue에 추가, 저장공간 부족 시에 illegalStateException 발생
2.	Object remove() : Queue 에서 객체를 꺼내 반환, 비어있을 떄 NoSuchElementException 발생
3.	Object element() : 삭제없이 요소를 읽어옴, peek과 달리 Queue 비었을 때 NoSuchElementExceoption 발생
4.	boolean offer(Object o) : Queue 에 객체를 저장
5.	Object poll() : Queue 에서 객체를 꺼내서 반환
6.	Object peek() : 삭제없이 요소를 읽어옴

#### Stack, Queue 메서드 사용 예제

```java
public class StackEx1 {

	public static void main(String[] args) {
		
		Stack<Integer> st = new Stack<Integer>();
		Queue<Integer> q = new LinkedList<Integer>();
		
		st.push(1);
		st.push(2);
		st.push(3);

		q.offer(1);
		q.offer(2);
		q.offer(3);
		
		System.out.println("=stack=");
		while(!(st.empty())){
			System.out.println(st.pop());
		}
		System.out.println("=queue=");
		while(!(q.isEmpty())){
			System.out.println(q.poll());
		}
	}
}
```
```
=stack=
3
2
1
=queue=
1
2
3
```

#### Stack 활용예제

* 스택 활용 예 : 웹브라우저의 뒤로가기/앞으로가기
* 큐 활용 예 : 최근사용문서, 버퍼
  
```java
public class Ex11_3 {

	public static void main(String[] args) {
		
		String expression = "((3+5*8-2))";
		Stack<String> s = new Stack<String>();
		
		System.out.println("expression : " + expression);
		
		try {
			for (int i = 0; i < expression.length(); i++) {
				char ch = expression.charAt(i);
				if(ch == '(') {
					s.push(ch + "");
				}else if(ch == ')') {
					s.pop();
				}
			}
			if(s.isEmpty()) {
				System.out.println("괄호가 일치합니다.");
			}else {
				System.out.println("괄호가 일치하지 않습니다.");
			}
		} catch (EmptyStackException e) {
			System.out.println("괄호가 일치하지 않습니다.");
		}
		
	}
}
```
```
expression : ((3+5*8-2))
괄호가 일치합니다.
```

* '(' 를 만나면 stack에 push 메서드로 값을 넣고 ')' 를 만나면 stack에서 pop 메서드로 '(' 를 꺼냄.
* ')' 를 만나서 '(' 를 꺼내려고 할 때 스택이 비어있으면 괄호 일치, 비어있지 않으면 괄호가 일치하지 않는 것임.

#### Queue 활용예제

* 스택 활용 예 : 웹브라우저의 뒤로가기/앞으로가기, 수식괄호계산
* 큐 활용 예 : 최근사용문서, 버퍼
  
```java
public class Ex11_4 {

	static Queue<String> q = new LinkedList<String>();
	static final int MAX_SIZE = 5;
	
	public static void main(String[] args) {
		System.out.println("help 입력 시 도움말을 볼 수 있습니다.");
	
		while(true) {
			System.out.print(">>");
			
			try {
				Scanner sc = new Scanner(System.in);
				String input = sc.nextLine().trim();
						
				if("".equals(input)) {
					continue;
				}
				
				if(input.equalsIgnoreCase("q")) {
					System.exit(0);
				}else if(input.equalsIgnoreCase("help")) {
					System.out.println(" help - 도움말을 보여줍니다.");
					System.out.println(" q or Q - 프로그램을 종료합니다.");
					System.out.println(" history - 최근에 입력한 명령어를 " + MAX_SIZE + "개 보여줍니다.");
				}else if(input.equalsIgnoreCase("history")) {
					save(input);
					
					LinkedList<String> list = (LinkedList<String>)q;
					
					for (int i = 0; i < list.size(); i++) {
						System.out.println((i+1) + "." + list.get(i));
					}
				}else {
					save(input);
					System.out.println(input);
				}
			} catch (Exception e) {
				System.out.println("입력오류입니다.");
			}
		}
	}
	
	public static void save(String input) {
		if(!"".equals(input)) {
			q.offer(input);
		}
		
		if(q.size() > MAX_SIZE) {
			q.remove();
		}
	}
}
```
```
help 입력 시 도움말을 볼 수 있습니다.
>>Hello
Hello
>>Java
Java
>>Spring
Spring
>>Stack
Stack
>>Queue
Queue
>>help
 help - 도움말을 보여줍니다.
 q or Q - 프로그램을 종료합니다.
 history - 최근에 입력한 명령어를 5개 보여줍니다.
>>HIstory
1.Java
2.Spring
3.Stack
4.Queue
5.HIstory
>>Q
```

</div>
</details>

<details>
<summary style="font-size:20px">Iterator, Arrays, Comparable</summary>
<div markdown="1">

### Iterator, ListIterator, Enumeration 

* 컬렉션에 저장된 데이터를 접근하는데 사용되는 인터페이스
* Enumeration 은 Iterator 의 구버전
* ListIteratior 는 Iterator 의 접근성을 향상시킨 것(단방향 -> 양방향) (잘쓰이진 않음 Iterator 만 정확히 알고 넘어가자.)
* Iterator는 왜 쓸까?
  * 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화하여 읽어오기 위함. List, Set, Hash 는 각 메서드가 읽어오는 방법이 다르기때문에
  * 표준화된 Iterator 를 사용함으로써 요소들을 읽어오는 역할을 하기 위함.

```java
public class IteratorTest {

	public static void main(String[] args) {
		
		List<Integer> list = new ArrayList<Integer>();	// 다른 컬렉션 변경시 이부분만 고치면 사용 가능함.
		list.add(1);
		list.add(2);
		list.add(3);
		
		Iterator<Integer> it = list.iterator();
		
		while(it.hasNext()) {
			System.out.println(it.next());
		}
	}
} 
```

* Iterator는 Collection 인터페이스의 정의되어있어 List, Set 도 사용가능함.
* iterator() 라는 메서드를 호출하면 Iterator it 객체에 담김.
* 객체를 활용하여 읽어올 요소가 있는지 hasNext() 로 확인 후 next() 로 요소를 읽어서 사용함.
* iterator() 는 1회용이라 한 번 사용하고나면 객체를 다시 얻어와야함.

#### 사용 메서드 

* boolean hasNext() - 읽어 올 요소가 남아있는지 확인, 있으면 true, 없으면 false 반환
* Object next() - 다음 요소를 읽어옴, next() 를 호출하기전에 hasNext() 를 호출하여 읽어 올 요소가 있는지 확인

### Map과 Iterator

* List, Set 은 Iterator를 사용할 수 있지만 Map 인터페이스는 key, value를 쌍으로 저장하므로 iterator() 를 직접 호출할 수 없음.
* Map을 사용할 때는 keySet() 과 entrySet() 을 사용하자.

```java
public class MapIteratorTest {

	public static void main(String[] args) {

		Map<Integer, String> map = new HashMap<Integer, String>();
		map.put(1, "Son");
		map.put(2, "Park");

		// 방법1 - keySet 활용
		for(Integer key : map.keySet()) {
			System.out.println("key  : " + key + ", value : " + map.get(key));
		}
		System.out.println();
		// 방법2 - entrySet 활용
		for(Map.Entry<Integer, String> entry : map.entrySet()) {
			System.out.println("key  : " + entry.getKey() + ", value : " + entry.getValue());
		}
	}
}
```

* 자세한 Map 사용법은 뒤에서 자세하게 예제와 알아보자.

### Arrays

* 배열을 다루기 편리한 매서드(static) 제공함.

#### Arrays 메서드 - toString, 복사

```java
public class ArraysTest {

	public static void main(String[] args) {
		
		ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1, 2, 3));
		System.out.println(list);
	} 
}
```

* 배열의 타입만 다르게 오버로딩 되어있는 - toString() 기본형 배열과 참조형 배열 별로 하나씩 정의되어있음.

```java
public class ArraysTest {

	public static void main(String[] args) {
		
		// toString()
		ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1, 2, 3));
		System.out.println(list);
		System.out.println();
		
		// copyOf()
		int[] arr1 = {1, 2, 3, 4};
		int[] arr2 = Arrays.copyOf(arr1, arr1.length);
		for(int newCopyArray : arr2) {
			System.out.println(newCopyArray);
		}
	}
}
```

#### Arrays 메서드 - fill(), setAll() ,sort(), binarySearch()

```java
import java.util.Arrays;

public class ArraysTest {

	public static void main(String[] args) {
		
		//fill(), setAll()
		int[] arr = new int[5];
		Arrays.fill(arr, 9);
		
		for (int i : arr) {
			System.out.print(i + " ");
		}
		System.out.println();
		Arrays.setAll(arr, i -> (int)(Math.random()*5) + 1);
		for (int i : arr) {
			System.out.print(i + " ");
		}
		
		System.out.println();
		//sort(), binarySearch()
		Arrays.sort(arr);
		for (int i : arr) {
			System.out.print(i + " ");
		}
		System.out.println();
		int[] binarySearch = {4, 2, 6, 7, 3};
		Arrays.sort(binarySearch);
		System.out.println(Arrays.binarySearch(binarySearch, 4));
	}
}
```
```
9 9 9 9 9 
1 4 5 1 5 
1 1 4 5 5 
2

```

* fill() 은 배열의 모든 요소를 지정된 값으로 채움.
* setAll() 은 배열을 채우는데 사용할 함수형 인터페이스를 매개변수로 받음.
* sort() 는 배열을 정렬할 때
* binarySearch() 는 알고리즘에도 자주 나오는 메서드이므로 잘 기억해두자
  * 배열이 정렬되어있다는 상태를 전제하에 지정된 값이 지정된 위치를 찾아서 반환함.
  * 배열의 검색할 범위를 반복적으로 절반씩 줄여가며 검색하므로 검색속도가 이진 검색보다 빠름.
  * 단, binarySearch() 를 사용할 때는 배열이 정렬되어있다는 것을 잘 기억해두고 사용하자.

#### Arrays 메서드 - toString(), deepToString(), equals(), deepEquals()

```java
import java.util.Arrays;

public class ArraysTest {

	public static void main(String[] args) {
		
		// toString, deepToString
		int[] arr = {1, 2, 3, 4};
		int[] arr2 = {1, 2, 3, 4};
		int[][] twoArr = { {1, 2}, {3, 4} };
		int[][] twoArr2 = { {1, 2}, {3, 4} };
		
		System.out.println(Arrays.toString(arr));
		System.out.println(Arrays.deepToString(twoArr));
		
		// equals, deepEquals
		System.out.println(Arrays.equals(arr, arr2));
		System.out.println(Arrays.deepEquals(twoArr, twoArr2));
	}
}
```
```
[1, 2, 3, 4]
[[1, 2], [3, 4]]
true
true
```

* 많이 사용해왔던 toString(), equals() 이차원 배열에서는 deepToString(), deepEquals() 사용함을 알아두자.

#### Arrays 메서드 - asList(Object ... a)

```java
public class ArraysTest {

	public static void main(String[] args) {
		//asList(Object ...a)
		List<Integer> list = Arrays.asList(1,2,3,4,5);
		System.out.println(list);
		// list.add(6); asList()가 반환한 List의 크기는 변경할 수 없음.
		// 변경하고하자면 아래와 같이 사용 가능함.
		List<Integer> lists = new ArrayList<Integer>(Arrays.asList(1, 2, 3, 4, 5));
		lists.add(6);
		System.out.println(lists);
	}
}
```
```
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 6]
```

* asList()는 배열을 List에 담아서 반환함. 매개변수의 타입이 가변인수라서 배열 생성없이 저장할 요소들만 나열하는 것도 가능.
* asList()가 반환한 List의 크기를 변경할 수는 없음. 새로운 ArrayList를 생성하여 변경하는 것은 가능함.

### Comparator 와 Comparable

* 궁금한 인터페이스, 클래스의 오픈 소스를 보고싶을 때 들어가면 익숙한 Comparator, Comparable 볼 수 있었음. 얘네는 뭘까?
* Comparator와 Comparable은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메서드를 정의함.
* Comparable 을 구현한 클래스는 기본 정렬기준을 구현하는데 사용하고, Comparator 는 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용함.
* 실제 소스는 아래와 같음

```java
public interface Comparator {
	int compare(Object o1, Object o2);	// o1과 o2를 비교
	boolean equals(Object obj);
}

public interface Comparable {
	int compareTo(Object o);	// 객체 자신 (this) 와 o를 비교
}
```

* Arrays.sort 는 String의 Comparable 구현에 의한 정렬
* Arrays.sort(Object[] a, String.CASE_INSENSITIVE_ORDER) 은 지정한 Comparator에 의한 정렬
* 위의 두 차이점이 있다는 것을 알아두자.

</div>
</details>

<details>
<summary style="font-size:20px">HashSet, TreeSet, HashMap, Collections</summary>
<div markdown="1">

### HashSet

* Set인터페이스를 구현하여 순서와, 중복이 허용되지않음.
* 순서를 유지하고자하면 LinkedHashSet 을 사용해야함.

#### HashSet 예제1

```java
public class HashSetTest {

	public static void main(String[] args) {
		
		Object[] arr = {"1", "2", "5", "6", "2", "1"};
		
		Set<Object> hashSet = new HashSet<Object>();
		
		for (int i = 0; i < arr.length; i++) {
			hashSet.add(arr[i]);
		}
		System.out.println(hashSet);
		
		Iterator<Object> iterator = (Iterator<Object>) hashSet.iterator();
		
		while(iterator.hasNext()) {
			System.out.print(iterator.next() + " ");
		}
	}
}
```
```
[1, 2, 5, 6]
1 2 5 6 
```

* 결과는 순서가 유지된 것처럼 나왔으나 순서는 유지되지않음.

#### HashSet 예제2

```java
public class HashSetTest {

	public static void main(String[] args) {
		
		Set<Integer> set = new HashSet<Integer>();
		
		for (int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(num);
		}
		
		List<Integer> list = new LinkedList<Integer>(set);
		Collections.sort(list);
		System.out.println(list);
	}
}
```
```
[7, 12, 13, 16, 25, 36]
```

* set의 크기가 6보다 작은 동안 1~45 사이의 난수를 저장함.
* set의 모든 요소를 list에 저장하고 list를 정렬 후에 출력한 결과가 나옴.

#### HashSet 예제3

```java
public class HashSetTest {
	class Person{
		
		String name;
		int age;
		
		Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public String toString() {
			return "name : " + name + ", age  : " + age; 
		}
		
		@Override
		public boolean equals(Object obj) {
			if(!(obj instanceof Person)) return false;
			Person p = (Person)obj;
			return name.equals(p.name) && age == p.age;
		}
		
		@Override
		public int hashCode() {
			return Objects.hash(name, age);
		}
	}
	public class HashSetTest {

		public static void main(String[] args) {
		
			Set<Person> set = new HashSet<Person>();
			set.add(new Person("Son", 29));
			set.add(new Person("Son", 29));
			System.out.println(set);
		}
	}
}
```
```
[name : Son, age  : 29]
```

* equals 를 오버라이딩 하지 않으면 같은 객체를 생성하더라도 중복 값이 나오므로 오버라이딩을 해줘야함.
* 이 때 equals 뿐만 아니라 hashCode의 값도 동일해야하므로 hashCode도 오버라이딩 해줘야함.

### TreeSet

* 이진 탐색 트리라는 자료구조 형태로 데이터를 저장하는 컬렉션 클래스임.
* 이진 트리는 모든 노드가 최대 2개의 하위 노드를 가짐.
* 범위 검색과 정렬에 유리하나 데이터 추가, 삭제에는 성능이 더 안나옴.
* Set 인터페이스를 구현했으므로 중복과, 순서를 지키지않음.

* TreeSet은 이진 탐색 트리의 성능을 향상시킨 **레드-블랙 트리** 로 구현되어있음.
 
![Alt text](image-11.png) 

* 레드 블랙 트리란?
  * 일반적인 이진 탐색 트리는 트리의 높이만큼 시간이 걸림.
  * 레드 블랙 트리는 부모노드보다 작은 값을 가지는 노드는 왼족, 큰 값을 가지면 오른쪽으로 배치하여 트리의 균형을 맞춤.

```java
class TreeNode{
	TreeNode left;
	Object element;
	TreeNode right;
}
```

#### 이진 탐색 트리(binary search tree)

* 이진 탐색 트리는 부모노드의 왼쪽에는 부모노드보다 작은 값을, 오른쪽에는 부모노드보다 큰 값을 저장함.
* 데이터가 많아질 수록 추가, 삭제에 걸리는 시간은 더 걸림(비교 횟수가 증가하므로)

#### 이진 탐색 트리 저장과정

* HashSet은 equals()와 hashCode() 로 비교함.
* TreeSet은 compare()을 통해 비교함.
* ex) 7, 4, 9, 1 ,5 를 비교할 때 
	* 첫 번째로 저장되는 값은 루트 (7)
	* 두 번째 값은 루트부터 시작해서 작은 값은 왼쪽에 큰 값은 오른쪽에 저장함. 7밑에 4, 9
	* 그 다음으로 1이 나오므로 4밑에 좌측 자손 노드에는 1이 우측 자손 노드에는 5가 들어감.

#### TreeSet 예제1

```java
public class TreeSetTest {

	public static void main(String[] args) {
		Set<Integer> set = new TreeSet<Integer>();
		
		for (int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(num);
		}
		System.out.print(set + " ");
	}
}
```
```
[1, 6, 16, 17, 24, 39] 
```

* TreeSet은 Set인터페이스를 구현해서 순서를 지키지 않으나 TreeSet은 구현과정에서 이미 정렬하기 때문에 따로 정렬할 필요가 없음.

#### TreeSet 예제2

```java
public class TreeSetTest {

	public static void main(String[] args) {
		TreeSet<Integer> treeSet = new TreeSet<Integer>();
		int[] score = {80, 95, 50, 35, 45, 65, 10, 100};
		
		for (int i = 0; i < score.length; i++) {
			treeSet.add(score[i]);
		}
		
		System.out.println("50보다 작은 값 :" + treeSet.headSet(50));
		System.out.println("50보다 큰 값 :" + treeSet.tailSet(50));
		System.out.println("40 ~ 80사이의 값 :" + treeSet.subSet(40, 80));
	}
}
```
```
50보다 작은 값 :[10, 35, 45]
50보다 큰 값 :[50, 65, 80, 95, 100]
40 ~ 80사이의 값 :[45, 50, 65]
```

### HashMap과 Collections 메서드

* HashMap은 Map을 구현했으므로 앞에서 살펴본 Map의 특징, key와 value를 묶어서 하나의 데이터(entry)로 저장한다는 특징이 있음.
* 순서와 중복을 허용하지않음. 중복의 경우에는 키값은 허용하지않고 값은 허용함.
* 해싱기법으로 데이터를 저장하므로 검색이 빠름.

```java
public class HashMap extends AbstractMap implements Map, Cloneable, Serializable{
	transient Entry[] table;
	...
	static class Entry implements Map.Entry {
		final Object key;
		Object value;
		...
	}
}
```

#### HashMap 예제1

```java
public class HashMapTest {

	public static void main(String[] args) {
		HashMap<String, String> map = new HashMap<String, String>();
		map.put("myId", "1234");
		map.put("asdf", "1111");
		map.put("asdf", "1234");
		
		Scanner sc = new Scanner(System.in);
		
		while(true) {
			System.out.println("id, password 입력");
			System.out.print("id : ");
			String id = sc.next();
			
			System.out.print("password : ");
			String password = sc.next();
			System.out.println();
			
			if(!(map.containsKey(id))){
				System.out.println("입력하신 id는 존재하지않음. 다시 입력");
				continue;
			}
			
			if(!(map.get(id).equals(password))) {
				System.out.println("비밀번호가 일치하지 않습니다. 다시 입력");
			}else {
				System.out.println("id와 비밀번호가 일치합니다.");
				break;
			}
		}
	}
```
```
id, password 입력
id : asdf
password : 1111

비밀번호가 일치하지 않습니다. 다시 입력
id, password 입력
id : asdf
password : 1234

id와 비밀번호가 일치합니다.
```

* HashMap에 id를 중복해서 입력하면 오류가 나지 않음. 하지만 키값은 덮어씌워짐.

#### HashMap 예제2

```java
public class HashMapTest2 {

	public static void main(String[] args) {
		
		HashMap<String, Integer> map = new HashMap<String, Integer>();
		
		map.put("김자바", 90);
		map.put("김자바", 100);
		map.put("이자바", 100);
		map.put("강자바", 80);
		map.put("안자바", 90);
		
		Set set = map.entrySet();
		Iterator it = set.iterator();
		
		while(it.hasNext()) {
			Map.Entry e = (Map.Entry)it.next();
			System.out.println("이름 : " + e.getKey() + ", 점수 : " + e.getValue());
		}
		
		set = map.keySet();
		System.out.println("참가자 명단 : " + set);
		
		Collection values = map.values();
		it = values.iterator();
		
		int total = 0;
		
		while(it.hasNext()) {
			int i = (int)it.next();
			total += i;
		}
		
		System.out.println("총점 : " + total);
		System.out.println("평균 : " + (double)total/set.size());
		System.out.println("최고점수 : " + Collections.max(values));
		System.out.println("최고점수 : " + Collections.min(values));
	}
}
```
```
이름 : 안자바, 점수 : 90
이름 : 김자바, 점수 : 100
이름 : 강자바, 점수 : 80
이름 : 이자바, 점수 : 100
참가자 명단 : [안자바, 김자바, 강자바, 이자바]
총점 : 370
평균 : 92.5
최고점수 : 100
최고점수 : 80
```

#### HashMap 예제3

```java
public class HashMapTest3 {

	public static void main(String[] args) {
		String[] data = { "A","K","A","K","D","K","A","K","K","K","Z","D"};
		
		HashMap<String, Integer> map = new HashMap<String, Integer>();
		
		for (int i = 0; i < data.length; i++) {
			if(map.containsKey(data[i])) {
				int value = map.get(data[i]);
				map.put(data[i], value + 1);
			}else {
				map.put(data[i], 1);
			}
		}
		
		Iterator<?> it = map.entrySet().iterator();
		
		while(it.hasNext()) {
			Map.Entry<String, Integer> entry = (Map.Entry)it.next();
			int value = entry.getValue();
			System.out.println(entry.getKey() + " : " 
					+ printBar('#', value) + " " + value);
		}
	}

	private static String printBar(char c, int value) {
		// c가 value의 개수만큼
		char[] cArr = new char[value];
		
		for (int i = 0; i < cArr.length; i++) {
			cArr[i] = c;
		}
		
		return new String(cArr);	// 이 부분 이해안감 내일 다시보기
	}
}
```
```
A : ### 3
D : ## 2
Z : # 1
K : ###### 6
```

### Collections 메서드

* Arrays가 배열과 관련된 메서드를 제공하는 것처럼, Collections 메서드는 컬렉션과 관련된 메서드를 제공함.
* 컬렉션의 동기화 synchronized 메서드를 제공함.
  * Vector는 동기화가 되어있으나 ArraysList는 동기화를 제공하지않음.

```java
List syncList = Collections.synchronizedList(new ArrayList(...));
```

* 동기화되어있지 않은 new ArrayList 를 넣으면 동기화가능.

* 다양한 Collections 메서드
	* 컬렉션에 저장된 데이터를 보호하기위해 unmodifiable 을 사용하여 변경불가로 만들 수 있음.
	* 객체 한 개만 저장할 때 singleton 을 사용하여 객체를 하나만 반환하게 만들 수 있음.
	* 한 종류의 객체만 저장할 때는 checked 를 사용하여 한 종류의 객체만 저장할 수 있음.
	* 존재하고 어떠한 역할을 하는지만 알아두자.(자주 쓰이지 않음)

* addAll, rotate, swap, shuffle, sort, binarySearch, max, min, fill, nCopies 등등이 있음.
* 자주 쓰이는 sort, max, min 은 잘알아두자.

#### Collections 메서드 예제

```java
public class Collections {

	public static void main(String[] args) {
		
		List<Integer> list = new ArrayList<Integer>();
		
		list.addAll(list);
		System.out.println(list);
		
		list.add(1);
		list.add(5);
		list.add(4);
		list.add(2);
		list.add(7);
		System.out.println(list);
		
		sort(list);
		System.out.println(list);
		
		int max = max(list);
		int min = min(list);
		System.out.println(max + ", " + min);
		
	}
}
```
```
[]
[1, 5, 4, 2, 7]
[1, 2, 4, 5, 7]
7, 1
```

</div>
</details>

<details>
<summary style="font-size:20px">지네릭스</summary>
<div markdown="1">

### 지네릭스 (Generics)

* 지네릭스는 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주는 기능임.
* 지네릭스를 사용함으로써 얻는 장점
  * 타입 안정성 제공.
  * 타입체크와 형변환 생략으로 인한 코드 간결성
  
```java
// 지네릭스 이전 Object 타입
public class ArrayList extends AbstractList{
	private transient Object[] elementData;
	public boolean add(Object p) {...}
	pubvlic Object get(int index) {...}
}

// 지네릭스 사용 
public class ArrayList<E> extends AbstractList<E>{
	private transient E[] elementData;
	public boolean add(E o) { ... }
	public E get(int index) {...}
}
```

* 지네릭스 이전(JDK1.5이전)에는 Object 타입을 불가피하게 사용했지만, 지네릭스를 활용하면 원하는 타입을 지정하기만 하면 됨.

```java
class Tv {...}

ArrayList<Tv> tvList = new ArrayList<Tv>();

Tv t = tvList.get(0);
```

* 타입 변수 E 대신에 제 타입인 Tv를 대입해서 사용하고, Tv를 대입된 타입이라고 함.
* 형변환 필요없이 지네릭스의 도움으로 바로 사용가능함.
* 지네릭스를 사용하지 않는다면?

```java
class Tv {...}

ArrayList list = new ArrayList<();

Tv t = (Tv)list.get(0);
```

* 위의 예제와 같이 형변환을 명시해야 컴파일 에러가 나지 않음.

#### 지네릭스 용어

* 지네릭스의 용어들에 대한 정의를 정리하고 넘어가자.

```java
class Box<T> {}
```

* Box<T> : 지네릭 클래스, 'T의 Box' 또는 'T Box' 라고 읽음.
* T : 타입 변수 또는 타입 매개변수라고함.
* Box : 원시 타입

#### 지네릭 타입과 다형성

```java
ArrayList<Tv> list = new ArrayList<Tv>();		// Ok
ArrayList<Product> list = new ArrayList<Tv>();	// Error

ArrayList<Tv> list = new ArrayList<Tv>();		// Ok
ArrayList<Tv> list = new LinkedList<Tv>();		// Ok
```

* 클래스 Tv와 Product가 서로 상속관계에 있어도 일치해야함.
* 클래스 타입 간에 다형성을 적용하는 것은 가능함. 이 때에도 지네릭 타입은 일치해야함.
* 즉, 참조 변수와 생성자의 대입된 타입은 일치해야함.

```java
ArrayList<Product> list = new ArrayList<Product>();
list.add(new Product());
list.add(new Tv());
list.add(new Audio());
```

* 매개변수의 다형성도 성립함.

#### 제한된 지네릭 클래스

* 타입변수 T에 지정할 수 있는 타입의 종류를 제한함.

```java
class FruitBox<T extends Fruit>{
	ArrayList<T> list = new ArrayList<T>();
	...
} 

FruitBox<Apple> appleBox = new FruitBox<Apple>();	// Ok
FruitBox<Toy> toyBox = new FruitBox<Toy>();			// 에러 Toy는 Fruit 자식이 아님.
```

```java
class Fruit implements Eatable{
	public String toString() {
		return "Fruit";
	}
}
class Apple extends Fruit { public String toString() {return "Apple";}}
class Grape extends Fruit { public String toString() {return "Grape";}}
class Toy { public String toString() { return "Toy";}} 

interface Eatable {}

public class Ex12_3 {

	public static void main(String[] args) {
		FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
		FruitBox<Apple> appleBox = new FruitBox<Apple>();
		FruitBox<Grape> grapeBox = new FruitBox<Grape>();
		
		fruitBox.add(new Fruit());
		fruitBox.add(new Apple());
		fruitBox.add(new Grape());
		appleBox.add(new Apple());
		grapeBox.add(new Grape());
		
		System.out.println("fruitBox-"+fruitBox);
		System.out.println("appleBox-"+appleBox);
		System.out.println("grapeBox-"+grapeBox);
	}
}

class FruitBox<T extends Fruit & Eatable> extends Box<T>{
	
}

class Box<T>{
	ArrayList<T> list = new ArrayList<T>();
	void add(T item) {list.add(item);}
	T get(int i) {return list.get(i);}
	int size() {return list.size();}
	public String toString() {return list.toString();}
}
```
```
fruitBox-[Fruit, Apple, Grape]
appleBox-[Apple]
grapeBox-[Grape]

```

* interface. 구현시 & 기호로 연결함.
* FruitBox는 Fruit 만 상속받고 있으므로 FruitBox<Toy> 이렇게 쓰면 에러.
* 다형성에 의해서 appleBox에 Grape 객체를 담을 수 없고, grapeBox에 Apple 객체를 담을 수 없음. 

#### 지네릭스 제약

* 타입 변수에 대입은 인스턴스 별로 다르게 가능함.
* static멤버에 타입 변수는 사용 불가함.
* static은 모든 인스턴스 변수를 참조할 수 없음.
* 배열 생성할 때 타입 변수 사용불가. 타입 변수로 배열 선언은 가능함.

```java
class Box<T> {
	T[] itemArr;
	...
	T[] toArray(){
		T[] tmpArr = new T[itemArr.length];	// 에러
	}
}
```
* new연산자 때문에 컴파일 시점에 타입T가 뭔지 정확히 알아야하기때문에 사용할 수 없음.

#### 와일드카드

* 하나의 참조 변수로 대입된 타입이 다른 객체를 참조 가능함.

```java
ArrayList<Product> list = new ArrayList<Tv>();
```

* 위의 예제처럼 일치하지 않으면 컴파일 에러가 발생함.
* 지네릭 타입에도 다형성을 적용할 방법은 없을까?? 해서 사용 한 것이 와일드카드.

```java
<? extends T> - 와일드 카드의 상한 제한. T와 자손들만 가능
<? super T> - 와일드 카드의 하한 제한. T와 조상들만 가능
<?> - 제한 없음. 모든 타입이 가능 <? extends Object> 와 동일함.
```

```java
ArrayList<? extends Product> list = new ArrayList<Tv>();		// Ok
ArrayList<? extends Product> list = new ArrayList<Audio>();		// Ok
```

* 지네릭 타입이 <? extends Product> 이면 Product와 Product의 모든 자식이 가능함.

#### 지네릭 메서드

* 지네릭 타입이 선언된 메서드

```java
class FruitBox<T> {
	...
	static <T> void sort<List<T> list, Comparator<? super T> c){
		...
	}
}
```

* 클래스 타입 매개변수<T> 와 메서드의 타입 매개변수 <T>는 별개, 인스턴스 변수와 지역변수 개념과 유사.
* 호출할 때마다 타입을 대입해야함(생략 가능)
* 와일드 카드는 하나의 참조변수로 서로 다른 타입이 대입된 여러 지네릭 객체를 다루기 위함.
* 지네릭 메서드는 메서드를 호출할 때마다 다른 지네릭 타입을 대입할 수 있게 하기 위함.


</div>
</details>

<details>
<summary style="font-size:20px">열거형, 애너테이션</summary>
<div markdown="1">

### 열거형

* 관련된 여러 상수를 같이 묶어 놓은 것. 타입에 안전한 열거형을 제공하기위함.
* 자바의 열거형은 값하고 열거형을 모두 체크함.

```java
// 상수방식
class Card{
	static final int CLOVER = 0;
	static final int HEART = 1;
	static final int DIAMOND = 2;
	static final int SPADE = 3;

	static final int TWO = 0;
	static final int THREE = 1;
	static final int FOUR = 2;

	final int kind;
	final int num;
}
// enum 사용방식
class Card{
	enum Kind {CLOVER, HEART, DIAMOND, SPADE}
	enum Value {TWO, THREE, FOUR}

	final Kind kind;
	final Value value;
}

if(Card.Kind.CLOVER == Card.Value.TWO){		// 컴파일에러
	...
}
```

* 열거형을 이용해서 상수를 정의한 경우는 타입을 먼저 비교하므로 컴파일 에러 발생
* 열거형 상수에 비교연산자는 사용불가하며 compareTo로 비교 가능함.

### 열거형에 멤버 추가

* Enum 클래스에 정의된 ordinal()이 열거형 상수가 정의된 순서를 반환하지만, 열거형 상수의 값으로 사용하지 않는 것이 좋음.
* 내부적인 용도로만 사용되기 때문임.
* 열거형 상수 값이 불규칙적인 경우에는 열거형 상수의 이름 옆에 원하는 값을 괄호()와 함께 적으면됨.
* 먼저 열거형 상수를 모두 정의한 다음에 다른 멤버들을 추가해야하며, 인스턴스 변수와 생성자도 새로 추가해 주어야함..
  
#### 열거형 예제1

```java
enum Direction { 
	EAST, SOURTH, WEST, NORTH;
}

public class EnumTest {

	public static void main(String[] args) {
		Direction d = Direction.EAST;
		System.out.println(d);
		
		for (Direction dArr : Direction.values()) {
			System.out.println(dArr + ", " + dArr.ordinal());
		}
	}
}
```
```
EAST
EAST, 0
SOURTH, 1
WEST, 2
NORTH, 3
```

* d를 호출하면 EAST가 바로 나오고, Direction.values 를 활용하면 Direction들의 배열들을 꺼내어 쓸 수있음.
* 0 번째부터 순서를 알고 싶으면 ordinal을 사용하면됨.

### 애너테이션

* 주석처럼 프로그래밍 언어에 영향을 미치지 않으며, 유용한 정보를 제공함.
  
```java
@Test
public void method(){
	...
}
```

* 단순히 테스트를 위한 메서드임을 알려주는 애너테이션

#### @Deprecated
  
* 더 이상 사용되지 않는 필드나 메서드에 사용함으로써 더 이상 사용하지 않을 것을 권한다는 의미의 애너테이션.

#### @FunctionalInterface

* 함수형 인터페이스를 올바르게 선언했는지를 확인하고, 잘못된 경우 에러를 발생시키는 애너테이션.

#### @SuppressWarnings

* 컴파일러가 보여주는 경고메시지가 나타나지 않게 억제시켜주는 애너테이션.

</div>
</details>

<details>
<summary style="font-size:20px">프로세스와 쓰레드</summary>
<div markdown="1">

### 프로세스와 쓰레드

* 프로세스 : 실행중인 프로그램 , 프로그램을 실행하면 OS로부터 실행에 필요한 자원을 할당받아 프로세스가 됨.
* 프로세스는 프로그램을 수행하는 데 필요한 데이터와 메모리 등의 자원, 쓰레드로 구성되어있음.
* 쓰레드 : 프로세스의 자원을 이용해서 실제로 작업을 수행하는 것.
* 프로세스는 하나 이상의 쓰레드가 존재하며 둘 이상의 쓰레드를 가진 프로세스를 멀티쓰레드 프로세스라고 함.
* ex) 프로세스 : 쓰레드 = 공장 : 일꾼

#### 멀티쓰레딩의 장단점

**멀티쓰레딩의 장점**
* CPU의 사용률을 향상시킴.
* 자원을 보다 효율적으로 사용할 수 있음.
* 사용자에 대한 응답성이 향상됨.
* 작업이 분리되어 코드가 간결해짐.

* 메신저로 채팅하며 파일을 다운받거나 음성대화를 나누는 것이 가능한 이유가 멀티쓰레드로 작성되어 있기 때문임.
* 하나의 서버 프로세스가 여러 개의 쓰레드를 생성해서 쓰레드와 사용자의 요청이 일대일로 처리되도록 프로그래밍해야함.
* 하지만 멀티쓰레딩은 쓰레드가 같은 프로세스 내에서 자원을 공유하며 작업하므로 동기화, 교착상태와 같은 문제를 고려하며 프로그래밍해야함.
* 두 개의 쓰레드로 작업한 시간이 싱글쓰레드로 작업한 시간이 더 걸림.
  * 쓰레드간의 작업 전환에 시간이 더 걸리기 때문임.
  * 작업 전환을 할 때는 작업의 상태, PC 등의 정보를 저장하고 있어 읽어 오는 시간이 더 소요됨.

#### 쓰레드의 구현과 실행

* 쓰레드를 구현하는 방법은 Thread 클래스를 상속받는 방법과 Runnable 인터페이스를 구현하는 방법 두 가지가 있음.
  * 일반적으로 Runnable 인터페이스 방식이 더 자주 쓰이고 좋은 방식 (Thread 단일 상속만 가능하기에)
* Runnable 인터페이스를 구현하는 방법은 재사용성이 높고, 코드의 일관성을 유지할 수 있어 객체지향적인 방법임.

```java
// Thread 상속
class MyThread extends Thread{
	public void run() {...}	// Thread 클래스의 run() 을 오버라이딩
}

// Runnable 인터페이스 구현
class MyThread implements Runnable {
	public void run() {...} // Runnable 인터페이스 run() 구현
}

public interface Runnable{
	public abstract void run();
}
```

* Ruunable 인터페이스는 오로지 run() 만 정의되어 있는 간단한 인터페이스임.
* Runnable 인터페이스를 구현하기 위해서는 추상메서드인 run() 몸통을 만들어주는 것.

#### 쓰레드의 구현과 실행 예제

```java
package ch13;

public class Ex13_1 {

	public static void main(String[] args) {
		
		ThreadEx1_1 t1 = new ThreadEx1_1();
		
		Runnable r = new ThreadEx1_2();
		Thread t2 = new Thread(r);
		// Thread.t2 = new Thread(new ThreadEx1_2());
		
		t1.start();
		t2.start();
	}
}

class ThreadEx1_1 extends Thread{
	@Override
	public void run() {
		for (int i = 0; i < 5; i++) {
			System.out.println(Thread.currentThread().getName());
		}
	}
}

class ThreadEx1_2 implements Runnable{

	@Override
	public void run() {
		for (int i = 0; i < 5; i++) {
			System.out.println(Thread.currentThread().getName());
		}
	}
}
```
```
Thread-0
Thread-1
Thread-1
Thread-1
Thread-1
Thread-1
Thread-0
Thread-0
Thread-0
Thread-0
```

* Runnable과 Thread를 상속받았을 때의 차이점과 사용방법을 알아두자.
* start() 가 호출된 후 실행대기의 상태에 있다가 자신의 차례가 오면 실행됨.
* 한 번 실행이 종료된 쓰레드는 다시 실행할 수 없기에 새로운 쓰레드를 생성한 후에 다시 start()를 호출해야되는점 알아두자.
  * 두 번 실행했을 때 IllegalThreadStateException 오류가 발생함.

#### start() 와 run()

* start() 를 호출해야 하나의 새로운 쓰레드가 생기고 그 호출스택에 run()이 실행되는 것.
* 쓰레드를 실행시킬 때 왜 run() 이 아닌 start() 를 호출할까? 쓰레드가 실행되는 과정을 알아보자.

![Alt text](image-12.png)

**실행흐름**

1. main 메서드에서 쓰레드의 start() 를 호출.
2. start()는 새로운 쓰레드를 생성하고, 쓰레드가 작업하는데 사용될 호출스택을 생성함.
3. 새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행함.
4. 호출스택이 2개이므로 스케줄러가 정한 순서에 의해 번갈아 가면서 수행됨.

* 실행순서는 OS의 스케쥴러에 의해서 실행순서가 결정됨.
* run() 수행이 종료된 쓰레드는 호출스택이 모두 비워지고 쓰레드가 사용하던 호출스택은 사라짐.
* 메인쓰레드가 종료되도 쓰레드가 종료되지 않으면 프로그램은 종료되지않음.

### 쓰레드의 I/O 블락킹

![Alt text](image-13.png)

* 싱글 쓰레드의 블락 구간에서는 아무 일도 하지 못하는 반면
* 멀티 쓰레드는 입력을 기다리는 구간, 다른 쓰레드를 수행함으로써 효울적인 CPU 사용이 가능함.

#### 쓰레드의 I/O 블락킹 예제

```java
package ch13;

import javax.swing.JOptionPane;

public class Ex13_5 {

	public static void main(String[] args) {
		ThreadEx5_1 t1 = new ThreadEx5_1();
		t1.start();
		
		String input = JOptionPane.showInputDialog("아무 값이나 입력하세요.");
		System.out.println("입력하신 값은 " + input + "입니다.");
	}
}

class ThreadEx5_1 extends Thread{
	@Override
	public void run() {
		for (int i = 10; i > 0; i--) {
			System.out.println(i);
			try {
				sleep(1000);
			} catch (Exception e) {
			}
		}
	}
}

```

![Alt text](image-14.png)

* 멀티쓰레드로서 구현했을 때 입력을 기다리면서도 값을 입력하면 console창에 입력한 값이 나올 수 있는 기능을 하는 반면
* 싱글쓰레드는 사용자가 입력을 마치기 전까지는 화면에 숫자가 출력되지 않다가 사용자가 입력을 마치고 나서야 화면에 숫자가 출력됨.

### 쓰레드의 우선순위

* 쓰레드는 우선순위라는 속성(멤버변수)을 가지고 있어 이 우선순위의 값에 따라 쓰레드가 얻는 실행시간이 달라짐.
* 쓰레드의 우선순위를 다르게 함으로써 특정 쓰레드가 더 많은 작업시간을 갖도록 할 수 있음.
  * ex) 파일 다운로드하는 쓰레드보다 채팅하는 쓰레드 우선순위를 높게 설정하는 경우

```java
void setPriority(int newPriority)
int getPriority()

public static final int MAX_PRIORITY = 10	// 최대 우선순위
public static final int MIN_PRIORITY = 1	// 최소 우선순위
public static final int NORM_PRIORITY = 5	// 보통 우선순위
```

* 쓰레드가 가질 수 있는 우선순위 범위는 1~10이며 숫자가 높을수록 우선순위가 높음.
* main메서드를 수행하는 쓰레드는 우선순위가 5이므로 main내에서 생성하는 쓰레드의 우선순위는 자동적으로 5가 됨.

```java
package ch13;

public class Ex13_6 {

	public static void main(String[] args) {
		
		ThreadEx6_1 ex6_1 = new ThreadEx6_1();
		ThreadEx6_2 ex6_2 = new ThreadEx6_2();
		
		ex6_2.setPriority(7);
		
		System.out.println("Priority of 6_1 th(-) : " + ex6_1.getPriority());
		System.out.println("Priority of 6_2 th(|) : " + ex6_2.getPriority());
		ex6_1.start();
		ex6_2.start();
	}
}

class ThreadEx6_1 extends Thread{
	@Override
	public void run() {
		for (int i = 0; i < 100; i++) {
			System.out.print("-");
			for (int j = 0; j < 100000; j++) {	// 시간 지연용
				
			}
		}
	}
}

class ThreadEx6_2 extends Thread{
	@Override
	public void run() {
		for (int i = 0; i < 100; i++) {
			System.out.print("|");
			for (int j = 0; j < 100000; j++) {	// 시간 지연용
				
			}
		}
	}
}
```
```
Priority of 6_1 th(-) : 5
Priority of 6_2 th(|) : 7
-|-|-|-||||-|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||-----------------------------------------------------------------------------------------------
```

* ex6_1, ex6_2 모두 main에서 생성하였기에 우선순위인 5를 상속받음.
* 그 후 ex6_2 의 우선순위를 setPriority를 통해 7로 변경한 다음 start를 호출하여 쓰레드를 실행함.
* 쓰레드를 실행하기 전에만 우선순위를 변경할 수 있는점을 기억하자.
* 이론적으로는 우선순위가 높은 ex6_2의 쓰레드 종료시간이 더 빠름.
  * 1~10은 JVM에서 정해놓은 우선순위이고 OS에서는 32단계로 달라 희망사항을 스케쥴러에게 전달할 뿐임.
  * OS 스케쥴러가 참고해본다는 수준에 불과함.

#### 쓰레드 그룹

* 쓰레드 그룹은 서로 관련된 쓰레드를 그룹으로 다루기 위한 것임.
* 모든 쓰레드는 반드시 하나의 쓰레드 그룹에 포함되어 있어야함.
* 쓰레드 그룹을 지정하지 않고 생성한 쓰레드는 main 쓰레드 그룹에 속함.
* 자신을 생성한 쓰레드의 그룹과 우선순위를 상속받음.

```java
// 생성자
ThreadGroup(String name)
ThreadGroup(ThreadGroup parent, String name)
// 활성상태 쓰레드 수, 그룹 수 반환
int activeCount()
int activerGroupCount()
```

### 데몬 쓰레드

* 일반 쓰레드의 작업을 돋는 보조적인 역할을 수행함.
* 일반 쓰레드가 모두 종료되면 데몬 쓰레드는 자동적으로 종료됨.
* 데몬 쓰레드는 가비지 컬렉터, 워드프로세서 자동저장, 화면자동갱신 등이 있음.
* 무한 루프와 조건문을 이용해서 실행 후 대기하다가 특정 조건이 만족되면 작업을 수행하고 다시 대기하도록 작성함.

```java
public void run(){
	while(true){
		try{
			Thread.sleep(3 * 1000);
		}catch(InterruptedException e){

		}
		if(autoSave) autoSave();
	}
}

// 데몬 쓰레드 메서드
boolean isDaemon()
void setDaemon(boolean on)
```

* 무한루프와 특정조건을 활용하여 데몬 쓰레드를 작성한다는 것 알아두자.
* 쓰레드를 생성한 다음 실행(start()를 호출하기 전)에 setDaemon(true)을 실행해야함.
  * 그렇지 않으면 IllegalThreadStateException 발생

### 데몬 쓰레드 예제

```java
package ch13;

public class Ex13_7 implements Runnable{

	static boolean autoSave = false;
	
	public static void main(String[] args) {
		// 메인쓰레드
		Thread t = new Thread(new Ex13_7());
		t.setDaemon(true);	// 이 부분이 없으면 종료되지 않음.
		t.start();
		
		for (int i = 0; i <= 10; i++) {
			try {
				Thread.sleep(1000);
			}catch (InterruptedException e) {
				
			}
			System.out.println(i);
			
			if(i==5) {
				autoSave = true;
			}
		}
		System.out.println("프로그램 종료");
	}

	// 데몬 쓰레드(보조) - 일반쓰레드가 하나도 없을 때 같이 종료됨.
	@Override
	public void run() {
		while(true) {
			try {
				Thread.sleep(3*1000);
			} catch (InterruptedException e) {
				
			}
			if(autoSave) {
				autoSave();
			}
		}
	}
	public void autoSave() {
		System.out.println("작업파일 자동저장완료");
	}
}
```
```
0
1
2
3
4
5
6
7
작업파일 자동저장완료
8
9
10
프로그램 종료
```

* 3초마다 변수 autoSave를 확인해서 true이면 자동 저장 메서드를 반복하는 데몬쓰레드를 작성함.
* 만일 이 쓰레드를 데몬 쓰레드로 설정하지 않았다면, 이 프로그램은 강제종료하지 않는 한 영원히 종료되지 않았을 것임.
  * 데몬쓰레드 역할이 t.setDaemon(true) 이 부분임.

### 쓰레드의 상태

**쓰레드의 상태**

![Alt text](image-15.png)

**쓰레드 변화과정**

![Alt text](image-16.png)

1. 쓰레드를 생성(NEW)하고 start() 를 호출한다고해서 바로 실행되지않음. 
	* 실행대기열에 저장되어 자신의 차례가 될 때까지 기다려야하며, 큐 자료구조의 상태로 먼저 실행대기열에 들어온 쓰레드가 먼저 실행됨.
2. 실행대기상태(RUNNABLE)에 있다가 자신의 차례가 되면 실행상태가 됨.
3. 주어진 실행시간이 다되거나 yield()를 만나면 다시 실행대기상태가 되고 다음 차례의 쓰레드가 실행상태가 됨.
4. 실행중에 suspend(), sleep(), wait(), join(), I/O block에 의해 일시정지상태(WAITING, BLOCKED) 가 될 수 있음
   * I/O block은 입출력작업에서 발생하는 지연상태를 말함. 사용자의 입력이 끝나면 다시 실행대기상태가됨.
5. 지정된 일시정지시간이 다되거나(time-out), notify(), resume(), interrupt() 가 호출되면 일지정지상태를 벗어나 다시 실행대기열에서 자신의 차례를 기다림.
6. 실행을 모두 마치거나 stop()이 오출되면 쓰레드는 소멸됨.

* 그네타기에 비유, 일시정지는 벤치에서 쉬는 상태에 비유해서 알고있자.

### 쓰레드의 실행제어

![Alt text](image-17.png)

* **static** sleep - 쓰레드 일시정지(잠듬), 지정한 시간 지나면 자동 실행대기상태 
* join - 지정된 시간동안 쓰레드 실행, (다른 쓰레드 기다리기)
* interrupt - 자고 있거나 기다리고 있는 것 깨우기, 실행대기상태로 만듬
* stop - 쓰레드 즉시 종료
* suspend - 일시정지
* resume - 일시정지 실행대기상태
* **yield** - 실행시간 다른 쓰레드에게 양보 후 자신은 실행대기상태

* static이 붙은 sleep과 yield 는 자기 자신에게만 호출이 가능함.

#### sleep()

* 현재 쓰레드에 지정된 시간동안 멈추게함.
* 예외처리를 해야함. (InterrupedException) 은 Exception의 자손이므로 필수로 예외처리를 해주어야함.
* 자기 자신에게 적용되는 메서드임.

```java
// 3초면 3*1000 을 지정함.
static void sleep(long millis)

// 예외처리 대신 메서드 사용(매번 try catch 해줘야하기에)
void delay(long millis){
	try{
		Thread.sleep(millis);
	}catch(InterruptedException e){

	}
}
```

#### interrupt()

* 대기상태(WAITING)인 쓰레드를 실행대기 상태(RUNNABLE)로 만듬.
  * sleep, join, wait에 의해 작업이 중단된 상태


```java
void interrupt()				// false -> true 변경
boolean isInterrupted()			// 쓰레드 interrupted 상태 반환
static boolean interrupted()	// false 초기화
```

#### suspend(), resume(), stop()

* suspend()는 sleep()처럼 쓰레드를 멈추게하며, 정지된 쓰레드는 resume()을 통해 다시 실행대기 상태가됨.
* stop()은 호출되는 즉시 쓰레드가 종료됨.
* 교착상태에 빠지기 쉬워 deprecated 된 상태임.

#### join() 과 yield()

**join()**

* 쓰레드 자신이 하던 작업을 잠시 멈추고 다른 쓰레드가 지정된 시간동안 작업을 수행하도록 할 떄 join()을 사용함.
* 시간을 지정하지 않으면, 해당 쓰레드가 모두 마칠 때 까지 기다리게됨.
* 작업 중에 다른 쓰레드의 작업이 먼저 수행되어야할 필요가 있을 때 join()을 사용함.
* join() 도 sleep() 처럼 대기상태에서 벗어날 수 있고 try-catch문으로 감싸야함.
* sleep() 과 달리 특정 쓰레드에 대해 동작하므로 static 메서드가 아님.

**yield()**

* 쓰레드 자신에게 주어진 실행시간을 다음 차례의 쓰레드에게 양보함.
* 예를 들어 스케쥴러에 의해 1초의 실행시간을 할당받은 쓰레드가 0.5초 시간동안 작업한 상태에서 yield()가 호출되면 나머지 0.5초는 포기하고 다시 실행대기상태가됨.
* yield() 와 interrupt()를 적절히 사용하면 효율적인 실행이 가능함.

### 쓰레드의 동기화(synchronization)

* 멀티 쓰레드는 여러 쓰레드가 같은 자원을 공유하기 때문에 작업에 영향을 미칠 수가 있음.
* 동기화 : 한 쓰레드가 진행중인 작업을 **다른 쓰레드가 간섭하지 못하게 막는 것.**
* 동기화하려면 간섭받지 않아야 하는 문장들을 임계 영역으로 설정해야함.
  * 임계 영역 : **다른 쓰레드가 간섭하지 못하게 여러 문장들을 하나로 묶는 것**
* 임계영역은 락을 얻은 단 하나의 쓰레드만 출입가능(객체 1개에 락 1개)

#### synchronized 를 이용한 동기화

```java
// 메서드 전체를 임계 영역으로 지정
public synchronized void calcSum(){
	...
}

// 특정한 영역을 임계 영역으로 지정
synchronized(객체의 참조변수){
	...
}
```

* 임계 영역은 최소화해야함. 1번에 1개의 쓰레드만 임계 영역에 들어갈 수 있기 때문임.
* 
#### synchronized 를 이용한 동기화 예제

```java
package ch13;

public class Ex13_12 {

	public static void main(String[] args) {
		Runnable r = new RunnableEx12();
		Thread t1 = new Thread(r);
		Thread t2 = new Thread(r);
		t1.start();
		t2.start();
	}
}

class Account{
	
	private int balance = 1000; // 직접 접근을 막기 위해 private 으로 해야 동기화가 의미가 있음.
	
	public int getBalance() {
		return balance;
	}
	public synchronized void withdraw(int money) {
		if(balance >= money) {
			try {
				Thread.sleep(1000);
			}catch(InterruptedException e) {
				
			}
			balance -= money;
		}
	}
}

class RunnableEx12 implements Runnable{

	Account acc = new Account();
	
	@Override
	public void run() {
		while(acc.getBalance() > 0) {
			int money = (int)(Math.random() * 3 +1) * 100;
			acc.withdraw(money);
			System.out.println("balance:"+acc.getBalance());
		}
	}
	
}
```
```
balance:700
balance:500
balance:200
balance:100
balance:0
balance:0
```

* synchronized 를 붙이지 않으면 잔고가 음수가 될 수 있음. 왜 일까?
  * 쓰레드 A,B가 동기화되지않아서 200원에서 두 번의 랜덤함수를 통해 money 를 빼기때문에 음수가 될 수 있음
  * 하지만 synchronized 를 통해 자물쇠를 걸어 임계영역으로 설정한다면 A가 자물쇠를 건동안 한 번의 쓰레드 작업을 거치고나서 B가 작업을 수행함.
  * 그러므로 음수의 결과값은 나오지 않음.
  * 즉, 동시에 두 가지 if문을 타지 않도록 synchronized 로 동기화해줬기에 이런 결과가 나온 것임.

### wait() 과 notify()

* synchronized 예제로 동기화를 통해 공유 데이터를 보호하는 것을 보았음.
* 하지만 특정 쓰레드가 객체의 락을 가진 상태로 무한 반복 또는 오랜 시간을 보낸다면 이것도 문제가 됨.
* 예를 들어 계좌에 출금할 돈이 부족해서 한 쓰레드가 락을 보유한 채로 돈이 입금될 때 까지 오랜 시간 기다리면, 다른 쓰레드들은 락을 기다려야함.
* 이러한 상황을 개선하기 위해 고안된 것이 wait() 과 notify() 임.

* 동기화된 임계 영역의 코드를 수행하다가 작업을 더 이상 진행할 상황이 아니면 wait() 을 호출하여 락을 반납하고 기다리게함.
* 그러면 다른 쓰레드가 락을 얻어 해당 객체에 대한 작업을 수행할 수 있게 됨.
* 후에 작업을 진행할 수 있는 상황이 되면 notify()를 호출하여 작업을 중단했떤 쓰레드가 다시 락을 얻어 작업을 진행하게됨.

> wait() 호출 -> 실행 중이던 쓰레드 객체의 대기실에서 통지를 기다림 -> notify() 호출 시 대기실(waiting pool)에 있던 임의의 쓰레드에게 통보를 보냄
>
> notifyAll() -> 대기실(waiting pool) 에 있는 모든 쓰레드에게 통보를 보냄.

#### wait() 과 notify() 예제

```java
package ch13;

import java.util.ArrayList;

public class Ex13_14 {

	public static void main(String[] args) throws InterruptedException {
		
		Table table = new Table();
		
		new Thread(new Cook(table), "COOK").start();
		new Thread(new Customer(table, "donut"), "CUST1").start();
		new Thread(new Customer(table, "burger"), "CUST2").start();
		
		Thread.sleep(5000);
		System.exit(0);
	}
}

class Table{
	String[] dishNames = { "donut", "donut", "burger" };
	final int MAX_FOOD = 6;
	private ArrayList<String> dishes = new ArrayList<String>();
	
	public synchronized void add(String dish) {
		if(dishes.size() >= MAX_FOOD) {
			return;
		}
		dishes.add(dish);
		System.out.println("Dishes: " + dishes.toString());
	}
	public boolean remove(String dishName) {
		synchronized (this) {
			while(dishes.size() == 0) {
				String name = Thread.currentThread().getName();
				System.out.println(name+" is waiting.");
				try {
					Thread.sleep(500);
				}catch (InterruptedException e) {
				}
			}
			for (int i = 0; i < dishes.size(); i++) {
				if(dishName.equals(dishes.get(i))) {
					dishes.remove(i);
					return true;
				}
			}
		}
		
		return false;
	}
	
	public int dishNum() {
		return dishNames.length;
	}
}

class Customer implements Runnable{
	private Table table;
	private String food;
	
	public Customer(Table table, String food) {
		super();
		this.table = table;
		this.food = food;
	}

	@Override
	public void run() {
		while(true) {
			try {
				Thread.sleep(10);
			}catch (InterruptedException e) {
			}
			String name = Thread.currentThread().getName();
			
			if(eatFood()) {
				System.out.println(name + " ate a " + food);
			}else {
				System.out.println(name + " failed to eat. :(");
			}
		}
	}
	
	boolean eatFood() {
		return table.remove(food);
	}
}

class Cook implements Runnable {
	private Table table;
	
	public Cook(Table table) {
		this.table = table;
	}
	
	public void run() {
		while(true) {
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try {
				Thread.sleep(100);
			}catch (InterruptedException e) {
				// TODO: handle exception
			}
		}
	}
}
```

```
Dishes: [donut]
CUST2 is waiting.
CUST1 ate a donut
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
CUST2 is waiting.
```

* 이해하기 어려운 예제로 여러번 복습해서 보자.
* 여러 쓰레드가 공유하는 객체인 테이블의 add() 와 remove() 를 동기화함.
* 손님 쓰레드가 원하는 음식이 테이블에 없으면 failed to eat 을 출력하고 테이블에 음식이 없으면 계속 기다림..
* 이유는 손님 쓰레드가 테이블 객체의 lock 을 쥐고 기다리기 떄문임.
* 이럴 때 사용하는 것이 바로 wait() & notify() 임.
* 손님 쓰레드가 lock을 쥐고 기다리는게 아니라, wait()으로 lock을 풀고 기다리다가 음식이 추가되면 notify()로 통보를 받고 다시 lock을 얻어서 진행함.

#### wait() 과 notify() 예제2

```java
package ch13;

import java.util.ArrayList;

public class Ex13_15 {
	public static void main(String[] args) throws InterruptedException {
		
		Table2 table = new Table2();
		
		new Thread(new Cook2(table), "COOK").start();
		new Thread(new Customer2(table, "donut"), "CUST1").start();
		new Thread(new Customer2(table, "burger"), "CUST2").start();
		
		Thread.sleep(2000);
		System.exit(0);
	}
}

class Table2{
	String[] dishNames = { "donut", "donut", "burger" };
	final int MAX_FOOD = 6;
	private ArrayList<String> dishes = new ArrayList<String>();
	
	public synchronized void add(String dish) {
		if(dishes.size() >= MAX_FOOD) {
			String name = Thread.currentThread().getName();
			System.out.println(name+" is waiting.");
			try {
				wait();
				Thread.sleep(500);
			} catch (Exception e) {
			}
		}
		dishes.add(dish);
		notify();
		System.out.println("Dishes: " + dishes.toString());
	}
	public void remove(String dishName) {
		synchronized (this) {
			String name = Thread.currentThread().getName();
			
			while(dishes.size() == 0) {
				System.out.println(name+" is waiting.");
				try {
					wait();
					Thread.sleep(500);
				}catch (InterruptedException e) {
				}
			}
			while(true) {
				for (int i = 0; i < dishes.size(); i++) {
					if(dishName.equals(dishes.get(i))) {
						dishes.remove(i);
						notify();
						return;
					}
				}	
				
				try {
					System.out.println(name+" is waiting.");
					wait();
					Thread.sleep(500);
				} catch (InterruptedException e) {
				}
			}
			
		}
	}
	
	public int dishNum() {
		return dishNames.length;
	}
}

class Cook2 implements Runnable {
	private Table2 table;
	
	public Cook2(Table2 table) {
		this.table = table;
	}
	
	public void run() {
		while(true) {
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try {
				Thread.sleep(10);
			}catch (InterruptedException e) {
			}
		}
	}
}

class Customer2 implements Runnable{
	private Table2 table;
	private String food;
	
	public Customer2(Table2 table, String food) {
		super();
		this.table = table;
		this.food = food;
	}

	@Override
	public void run() {
		while(true) {
			try {
				Thread.sleep(10);
			}catch (InterruptedException e) {
			}
			String name = Thread.currentThread().getName();
			
			table.remove(food);
			System.out.println(name + " ate a " + food);
		}
	}
}
```
```
Dishes: [donut]
CUST2 is waiting.
Dishes: [burger]
CUST1 ate a donut
CUST2 ate a burger
Dishes: [donut]
CUST1 ate a donut
CUST1 is waiting.
Dishes: [donut]
CUST1 ate a donut
Dishes: [donut]
CUST2 is waiting.
Dishes: [donut, burger]
Dishes: [donut, burger]
CUST1 ate a donut
CUST2 ate a burger
CUST1 is waiting.
Dishes: [burger, donut]
```

* 이전 예제에서 wait() 과 notify()를 추가함.
* 테이블에 음식이 없을 때뿐만 아니라, 원하는 음식이 없을 때도 손님이 기다리도록 코드를 수정함.
* 하지만 waiting pool에 요리사 쓰레드와 손님 쓰레드가 같이 기다려, notify()호출 후 누가 통지를 받을지 알 수 없음.
* 만약 테이블의 음식이 줄어들어서 notify() 가 호출되면 요리사 쓰레드가 통지를 받아야함.
* 여기서 손님 쓰레드가 통지를 받으면 lock을 얻어도 여전히 자신이 원하는 음식이 없어서 다시 waiting pool에 들어가게됨.

</div>
</details>

<details>
<summary style="font-size:20px">람다와 스트림</summary>
<div markdown="1">

### 람다식

* 람다식은 메서드를 하나의 '식' 으로 표현한 것
* 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로, 람다식을 '익명 함수'라고도 함.
* 반환타입과 메서드 이름을 제거함.

```java
// 메서드를 간단한 식으로
int max(int a, int b){
	return a > b ? a : b;
}

//(람다식 적용 후 )
(a, b) -> a > b ? a : b;

// 반환값이 존재할 때, return문 생략 가능
(int a, int b) -> {
	return a > b ? a : b;
}

//(람다식 적용 후 )
(int a, int b) -> a > b ? a : b;

// 매개 변수 하나인 경우, 괄호 생략 가능(타입 없을 떄)
(a) -> a * a    ==>>   a -> a * a

(int a) -> a * a  ==>>  int a -> a * a (에러)
```

* 람다식은 익명 함수가 아니라 익명 객체.

### 함수형 인터페이스

* 하나의 추상메서드만 선언된 인터페이스

```java
package ch14;

public class LamdaTest1_1 {

	public static void main(String[] args) {
		
		MyFunction f =  (a, b) -> a > b ? a : b;

/*
		MyFunction f = new MyFunction() {

			@Override
			public int max(int a, int b) {
				return a > b ? a : b;
			}
		};
*/		
		int value = f.max(3, 5);
		System.out.println(value);
		
	}
}

interface MyFunction{
	int max(int a, int b);
}
```

* 함수형 인터페이스 타입의 참조변수로 람다식을 참조할 수 있음.
* 함수형 인터페이스는 단 하나의 추상메서드만 가져야함.
* 람다식을 다루기 위한 참조변수의 타입은 함수형 인터페이스로 함.(MyFunction)

#### 함수형 인터페이스 매개변수, 반환타입 예제

```java
package ch14;

public class LamdaTest1_2 {

	static void execute(MyFunction2 f) {
		f.run();
	}
	
	static MyFunction2 getMyFunction2() {
		MyFunction2 f = () -> System.out.println("f3.run()");
		return f;
	}
	
	
	public static void main(String[] args) {
		// 람다식 MyFunction의 run()구현
		MyFunction2 f1 = () -> System.out.println("f1.run()");
		
		// 익명클래스로 run()구현
		MyFunction2 f2 = new MyFunction2() {
			
			@Override
			public void run() {
				System.out.println("f2.run()");
			}
		};
		
		MyFunction2 f3 = getMyFunction2();
		
		f1.run();
		f2.run();
		f3.run();
		
		execute(f1);
		execute( () -> System.out.println("run()"));
	}
}

@FunctionalInterface
interface MyFunction2{
	void run();
}
```
```
f1.run()
f2.run()
f3.run()
f1.run()
run()
```

### java.util.function 패키지

* 대부분의 메서드 타입은 매개변수가 없거나 한 개, 두 개, 반환값은 없거나 한 개 형식으로 되어있음.
* 이를 위해서 매번 새로운 함수형 인터페이스를 정의하지 말고 가능하면 정의해놓은 패키지의 인터페이스를 활용하자는 뜻으로 사용함.

```java

//패키지
java.lang.Runnable
// void run()	-> 	매개변수도 없고, 반환값도 없음

//패키지
Supplier<T>
// T get()	-> 	매개변수는 없고, 반환값만 있음

//패키지
Consumer<T>
// void accept(T t)	-> 매개변수만 있고, 반환값이 없음

//패키지
Function<T,R>
// R apply(T t)	-> 일반적인 함수로, 하나의 매개변수를 받아서 결과를 반환

//패키지
Predicate<T>
//	boolean test(T t)	-> 조건식을 표현하는데 사용되며 매개변수는 하나이고, 반환 타입은 boolean
```

* 매개변수도 두 개일 때는 이름앞에 접두사 'Bi' 붙임. BiSupplier 는 매개 변수는 없으므로 존재하지 않음.
  * ex) BiConsumer, BiPredicate, BiFunction
* 만일 두 개 이상의 매개변수를 갖는 함수형 인터페이스가 필요하다면 직접 만들어서 사용해야함.
  
**UnaryOperator, BinarayOperator**

* UnaryOperator<T> 는 Function의 자손이며 매개변수와 결과의 타입이 같음.
* BinaryOpertaor<T> 는 BiFuntion의 자손, BiFunction과 달리 매개변수의 결과와 타입이 같음.

#### java.util.function 패키지 예제

```java
package ch14;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class Ex14_2 {
	public static void main(String[] args) {
		// Supplier 매개변수가 없고 반환값만 있음
		Supplier<Integer> s = () -> (int)(Math.random() * 100) + 1;
		// Consumer 매개변수만 있고 반환값은 없음
		Consumer<Integer> c = i -> System.out.print(i+", ");
		// Predicate 매개변수는 하나 반환 타입은 boolean
		Predicate<Integer> p = i -> i % 2 == 0;
		// Function 매개변수를 받아 결과 반환
		Function<Integer, Integer> f = i -> i/10*10;
		
		List<Integer> list = new ArrayList<Integer>();
		
		makeRandomList(s, list);
		System.out.println(list);
		printEvenNum(p, c, list);
		List<Integer> newList = doSomething(f, list);
		System.out.println(newList);
		
		
	}
	static<T> List<T> doSomething(Function<T, T> f, List<T> list){
		List<T> newList = new ArrayList<T>(list.size());
		
		for(T i : list) {
			newList.add(f.apply(i));
		}
		return newList;
	}
	
	static <T> void makeRandomList(Supplier<T> s, List<T> list) {
		for (int i = 0; i < 10; i++) {
			list.add(s.get());
		}
	}
	
	static <T> void printEvenNum(Predicate<T> p, Consumer<T> c, List<T> list) {
		System.out.print("[");
		for(T i : list) {
			if(p.test(i)) {
				c.accept(i);
			}
		}
		System.out.println("]");
	}
}
```
```
[46, 35, 51, 39, 34, 78, 85, 44, 8, 16]
[46, 34, 78, 44, 8, 16, ]
[40, 30, 50, 30, 30, 70, 80, 40, 0, 10]
```

* Supplier(get), Consumer(accept), Predicate(test), Function(apply) 4개의 사용방법을 잘알아두자.

### Predicate 결합

* Predicate 매개변수를 하나 받아 boolean 반환.
* and, or, not으로 연결하여 하나의 식을 구성하는 것 처럼 여러 Predicate를 연결하여 하나로 결합할 수 있음.
* default, static, 추상메서드 인터페이스가 가질 수 있는 메서드를 가질 수 있음

```java
Predicate<Integer> notP = p.negate();	// ! not
Predicate<Integer> all = notP.and(q).or(r);		// 100 <= i && i < 200 || i % 2 == 0

System.out.println(all.test(2))		// true
```

### Predicate 결합 예제

```java
package ch14;

import java.util.function.Predicate;

public class Ex14_3 {

	public static void main(String[] args) {
		Predicate<Integer> p = i -> i < 100;
		Predicate<Integer> q = i -> i < 200;
		Predicate<Integer> r = i -> i%2 == 0;
		Predicate<Integer> notP = p.negate();	// i >= 100;
		
		Predicate<Integer> all = notP.and(q.or(r));
		System.out.println(all.test(150));
		
		String str1 = "abc";
		String str2 = "abc";
		
		Predicate<String> p2 = Predicate.isEqual(str1);
		boolean result = p2.test(str2);
		System.out.println(result);
	}
}
```
```
true
true
```

### 컬렉션 프레임웍과 함수형 인터페이스

![Alt text](image-18.png)

```java
list.forEach(i -> System.out.print(i+ ","));	// list 모든 요소 출력
list.removeIf(x -> x%2==0 || x%3==0);	// 2 or 3의 배수 제거
list.replaceAll(i -> i*10);		// 모든 요소 10 곱하기
// map의 모든 요소 {k, v} 형식 출력
map.forEach((k,v) -> System.out.print("{"+k+","+v+"}","));
```

### 메서드 참조

* 람다식이 하나의 메서드만 호출하는 경우 메서드 참조를 통해 더 간략히 나타낼 수 있음.
* 클래스이름::메서드이름 형식으로 나타냄.

```java
Function<String, Integer> f = (String s) -> Integer.parseInt(s);

// 메서드 참조식
Function<String, Integer> f = Integer::parseInt;
```

### 메서드 참조 예제

```java
import java.util.function.Function;

public class Ex14_4 {

	public static void main(String[] args) {
		
//		Function<String, Integer> f = (String s) -> Integer.parseInt(s);
//		System.out.println(f.apply("100")+200);	// 숫자 300
		
		// 메서드 참조식 -> 클래스이름::메서드이름
		Function<String, Integer> f = Integer::parseInt;
		System.out.println(f.apply("100")+200);	// 300
	}
}
```

* 헷갈리면 메서드 참조식을 다시 람다식으로 나타내는 연습을 해보자.

### 생성자의 메서드 참조

```java
// 람다식
Supplier<Myclass> s = () -> new MyClass();	// 객체를 생성해서 줌.

// 메서드 참조
Supplier<Myclass> s = () -> MyClass::new

// 람다식
Function<Integer, MyClass> s = (i) -> new MyClass(i);

// 메서드 참조
Function<Integer, Myclass> s = MyClass::new;

// 람다식
Function<Integer, int[]> f = x -> new int[x];

// 메서드 참조
Function<Integer, int[]> f2 = int[]::new;
```

* 많은 수의 데이터를 다룰 때 스트림을 사용함.
  * List를 정렬할 때는 Collections.sort()를, 배열을 정렬할 때는 Arrays.sort()를 표준화 없이 다뤄짐.
  * 이를 해결하기 위한 것이 스트림.
* 스트림은 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서드를 정의

```java
public class StreamsTest {

	public static void main(String[] args) {
		 String[] str = { "aaa", "bbb", "ccc" };
		 List<String> strList = Arrays.asList(str);
		 
		 System.out.println(strList);
		 
		 Stream<String> stream1 = strList.stream();
		 Stream<String> stream2 = Arrays.stream(str);
		 
		 stream1.sorted().forEach(System.out::println);
		 stream2.sorted().forEach(System.out::println);

		// 정렬된 결과를 새로운 List에 담아서 반환함.
		 stream2 = Arrays.stream(str);
		 List<String> sortedList = stream2.sorted().collect(Collectors.toList());
		 System.out.println(sortedList);

		// 스트림은 1회용이기에 컬렉션 요소를 모두 읽으면 다시 생성해줘야함.
		 stream1 = strList.stream();
		 long numOfStr = stream1.count();
		 System.out.println(numOfStr);
	}
}
```
```
[aaa, bbb, ccc]
aaa
bbb
ccc
aaa
bbb
ccc
[aaa, bbb, ccc]
3
```

* 스트림은 데이터 소스로부터 데이터를 읽기만할 뿐, 데이터 소스를 변경하지는 않음.
* 필요하다면, 정렬된 결과를 컬렉션이나 배열에 담아서 반환할 수 있음.
* 스트림은 작업을 내부 반복으로 처리함.

#### 스트림 만들기 

**컬렉션**

* 스트림으로 작업하려면 배열, 컬렉션, 임의의 수 등. 스트림을 우선적으로 생성해야함.
* 컬렉션 최고 조상인 Collection에 stream()이 정의되어 있음.
  * 자손인 List와 Set을 구현한 컬렉션 클래스들은 모두 이 메서드로 스트림을 생성할 수 있음.

```java
Stream<E> stream();	// Collection 인터페이스 메서드

// list1을 소스로 하는 스트림 instStream1 생성
List<Integer> list1 = Arrays.asList(1,2,3,4,5);
Stream<Integer> intStream1 = list1.stream();

// list1을 사용하려면 최종연산을 수행해줘야함.
intStream1.forEach(System.out::println);
intStream1.forEach(System.out::println);	// 에러 발생
```
```
1
2
3
4
5
```

* 한번 생성한 스트림은 두 번 호출할 수 없음.

**배열**

```java
Stream<String> strStream1 = Stream.of("a", "b", "c");
Stream<String> strStream2 = Arrays.stream(new String[] {"a", "b", "c"});
IntStream intStream2 = Arrays.stream(new int[] {1,2,3}); 
Stream<int[]> intStream3 = Stream.of(new int[] {1,2,3});
```

* 문자열 스트림과 int, long, double 등 기본형 배열을 소스로 하는 스트림을 생성하는 메서드도 존재함.

**임의의 수**

```java
// 난수로 이루어진 스트림 반환 - 무한 스트림
// IntStream ints(), LongStream longs(), DoubleStream doubles()

// 무한스트림
IntStream intStream4 = new Random().ints();
// 유한스트림
intStream4.limit(5).forEach(System.out::println);
```
```
1745314093
-1497720991
466713899
-1325267381
-1215782904
```

* 난수를 생성하는 Random 클래스들에는 해당 타입의 난수들로 이루어진 스트림을 반환함.
* 이 메서드들은 크기가 정해지지 않은 무한스트림이므로 **limit()** 를 같이 사용해서 유한 스트림으로 만들어줘야함.

**특정 범위의 정수**

```java
IntStream intStream5 = IntStream.range(1, 5);
intStream5.forEach(System.out::print);
```
```
1234
```

* range() 와 같이 지정된 범위의 연속된 정수를 스트림으로 생성해서 반환할 수 있음.
* rangeClosed() 는 end의 범위까지 포함해서 반환함.

**람다식 iterate(), generate()**

```java
Stream<Integer> evenStream = Stream.iterate(0, n->n+2);
evenStream.forEach(System.out::print);	// 0, 2, 4, 6 ... 2의 배수로 무한 증가
```

* Stream 클래스의 iterate()와 generate()는 람다식을 매개변수로 받아 무한 스트림을 생성함.
* generate() 도 무한 스트림을 생성해서 반환하지만, 이전 결과를 이용해서 다음 요소를 계산하지는 않음.
* interate() 와 generate() 는 기본형 스트림 타입의 참조변수로 다룰 수는 없음.

**파일과 빈 스트림**

```java
Stream<Path> Files.list(Path dir)
Stream<String> Files.lines(Path path)

// 빈 스트림 : 요소가 없는 비어있는 스트림 생성
Stream emptyStream = Stream.emptry();	// empty는 빈 스트림을 생성해서 반환함.
long count = emptyStream.count()		// count값 0
```

* list()는 지정한 디렉토리에 있는 파일의 목록을 소스로 하는 스트림을 생성해서 반환함.

### 스트림 연산

* 스트림이 제공하는 다양한 연산을 이용하면 복잡한 작업들을 간단히 처리할 수 있음.
* 스트림이 제공하는 연산은 중간 연산, 최종 연산으로 분류 할 수 있음.
* 중간 연산은 연산결과를 스트림으로 반환하여 중간 연산을 연속해서 연결할 수 있음.
* 반면에 최종 연산은 스트림의 요소를 소모하며 연산을 수행하므로 한번만 연산이 가능함.

```java
String[] strArr = {"aa","abb","acc","dd","aa"};
Stream<String> stream = Stream.of(strArr);
stream.distinct().limit(5).sorted().forEach(System.out::println);
```
```
aa
abb
acc
dd
```

**중간연산**

* distinct() : 중복제거
* filter(Predicate<T> predicate) : 조건에 안 맞는 요소 제외
* limit(long maxSize) : 스트림 일부 잘라내기
* skip(long n) : 스트림 일부 건너뛰기
* peek(Consumer<T> action) : 스트림 요소 작업수행
* sorted() : 스트림 요소 정렬
* map, flatMap : 스트림 요소 반환

* 모든 중간연산의 반환은 Stream 이며, map() 이 핵심 역할.

**최종연산**

* void forEach(Consumer<? super T> action) : 각 요소 지정된 작업 수행
* long count() : 스트림 요소 개수 반환
* Optional<T> max(Comparator<? super T> comparator) : 스트림 최대값 반환
* Optional<T> min(Comparator<? super T> comparator) : 스트림 최소값 반환
* Optional<T> findAny() : 스트림 요소 하나 반환
* Optional<T> findFirst() : 첫 번째 요소
* Object[] toArray() : 모든 요소 배열 반환
* Optional<T> reduce(BinaryOperator<T> accumulator) : 스트림 요소 하나씩 줄여가며 계산
* R collect(Collector<T,A,R> collector) : 스트림 요소 수집

* 최종 연산은 reduce()와 collect() 가 핵심 역할.

### 스트림 중간연산

**skip(), limit()**

```java
Stream<T> skip(long n)
Stream<T> limit(long maxSize)

IntStream intStream = IntStream.rangeClosed(1, 10)		// 1 ~ 10 요소 가진 스트림
intStream.skip(3).limit(5).forEach(System.out::print);	// 45678
```

**filter(),distinct()**

* distinct()는 중복 제거, filter()는 주어진 조건에 맞지 않는 요소 걸러내기

```java
Stream<T> filter(Predicate<? super T> predicate)
Stream<T> distinct()

IntStream intStream = IntStream.of(1,2,2,3,3,3,4,5,5,6);
intStream.distinct().forEach(System.out::print);	// 123456

IntStream intStream = IntStream.rangeClosed(1, 10)			// 1 ~ 10 요소 가진 스트림
intstream.filter(i -> i%2 ==0).forEach(System.out::print);	// 246810
```

**sorted()**

* 스트림 정렬할 때 사용

```java
Stream<T> sorted()
Stream<T> sorted(Comparator<? super T> comparator)	// 지정된 Comparator 정렬
```

**Comparator 메서드**

```java
comparing(Function<T, U> keyExtractor)
comparing(Function<T, U) keyExtractor, Comparator<U> keyComparator)
```

* 스트림 요소가 Comparable을 구현한 경우, 매개변수 하나짜리를 사용하면되고 아니면 정렬기준을 지정해줘야함.

**map()**

```java
Stream<R> map(Function<? super T, ? extends R> mapper)

/*
filterSteram.map(File::getName)
	.filter(s -> s.indexOf('.') != -1)
	.map(s -> s.substring(s.indexOf('.') + 1))
	.map(String::toUpperCase)
	.distinct()
	.forEach(System.out::print);
*/
```

* map도 중간연산자이기에 filter 처럼 하나의 스트림에 여러 번 적용가능함.

**peek()**

```java
.peek(s->System.out.printf("filename=%s%n", s))	// 파일명 출력..
```

* 연산과 연산 사이에 올바르게 처리되었는지 확인하려면 peek()을 사용함.
* forEach() 와 달리 스트림의 요소를 소모하지 않으므로 연산 사이에 여러 번 넣어도 문제 X
* 주로 filter 나 map 의 결과를 확인할 때 사용함.

**flatMap()**

* 스트림의 스트림을 스트림으로 바꿔줌
* 여러 배열에 담긴 문자열을 하나의 Stream으로써 사용할 때 flatMap을 사용하자.

```java
// map()
Stream<String[]> -> (map(Arrays::stream)) -> Stream<Stream<String>>

// flatMap()
Stream<String[]> -> (flatMap(Arrays::stream)) -> Stream<String>
```

### Optional<T>

* Optional<T>는 T타입의 객체를 감싸는 래퍼 클래스.
* Optional타입의 객체에는 모든 타입의 객체를 담을 수 있음.
* 최종 연산의 결과를 그냥 반환하는게 아니라 Optional 객체에 담아서 반환 하면 반환된 결과가 null인지 간단히 처리 가능함.
* 널 체크를 위한 if문 없이도 NullPointerException이 발생하지 않는 보다 간결하고 안전한 코드 작성 가능.

```java
public final class Optional<T> {
	private final T value;	// 모든 타입에 대한 객체 저장 가능
}

public class OptionalTest {

	public static void main(String[] args) {
		String str1 = "abc";
		Optional<String> optional1 = Optional.of(str1);
		Optional<String> optional2 = Optional.of("abc");
		Optional<String> optional3 = Optional.ofNullable(null);

		System.out.println(optional1.get());	// 저장된 값 반환, null이면 예외발생
		System.out.println(optional3.orElse("ABC"));	// null일 때 반환할 값 지정, 값이 있으면 값 반환
		System.out.println(optional1.orElseGet(() -> new String()));	// 람다식 사용가능 String::new
		System.out.println(optional3.orElseThrow(NullPointerException::new));	// null 이면 예외발생

		// isPresent, ifPresent
		if (Optional.ofNullable(optional1).isPresent()) {	// 값이 null이면 false, 아니면 true
			System.out.println(str1);	// abc 출력됨.
		}

		Optional.ofNullable(str1).ifPresent(System.out::println);	// 널이 아닐 때만 작업 수행, 아니면 아무 일도 안함.
	}
}

Optional<String> optional = Optional.empty();	// 빈 객체로 초기화
```

* null 대신 빈 Optional<T> 객체를 사용하자.
  * NullpointException 줄이기 위함.

#### OptionalInt, OptionalLong, OptionalDouble

* IntStream과 같은 기본형 스트림의 최종 연산 일부는 Optional 대신 OptionalInt, OptionalLong, OptionalDouble을 반환함.
  * 더 높은 성능을 위함.

```java
public final class OptionalInt {
	private final boolean isPresent;	// 값 저장되어 있으면 true
	private final int value;	// int 타입 변수
}

OptionalInt optInt1 = OptionalInt.of(0)	// isPresent : true
OptionalInt optInt2 = OptionalInt.empty()	// isPresent : false

```

* Optional 에서는 get()으로 가져왔으나 타입에 따라 getAsInt(), getAsLong(), getAsDouble()에 유의하자.

### 스트림의 최종연산 

* 최종 연산은 스트림의 요소를 소모해서 결과를 만들어냄.
* 그러므로 최종 연산 후에는 스트림은 닫히게 되고 더 이상 사용할 수 없음.

```java
void forEach(Consumer<? super T> action)		// 병렬 경우 순서 보장 X
void forEachOrdered(Consumer<? super T> action)	// 병렬 경우에도 순서 보장 O

public class OptionalTest1 {

	public static void main(String[] args) {
		IntStream.range(1, 10).sequential().forEach(System.out::print);	// 순서 보장 x
		System.out.println();
		IntStream.range(1, 10).sequential().forEachOrdered(System.out::print);	// 순서 보장 o
		System.out.println();
		IntStream.range(1, 10).parallel().forEach(System.out::print);	// 순서 보장 x
		System.out.println();
		IntStream.range(1, 10).parallel().forEachOrdered(System.out::print);	// 순서 보장 o
	}
}
```

* sequential() -> 직렬스트림
* parallel() -> 병렬스트림 : 여러 쓰레드가 나눠서 작업 (순서보장이 안됨) 순서보장하기위해 forEachOrdered 사용함.

**조건검사**

```java
boolean allMatch (Predicate<? super T> predicate)	// 모든 요소 조건 만족하면 true
boolean anyMatch (Predicate<? super T> predicate)	// 한 요소라도 조건 만족하면 true
boolean noneMatch (Predicate<? super T> predicate)	// 모든 요소가 만족하지 않으면 true

boolean hasFailedStu = stuStream.anyMatch(s -> s.getTotalScore() <= 100);	// 낙제자가 있는지 여부?

Optional<T> findFirst()	// 첫 번째 요소 반환, 결과가 null일 수 있음
Optional<T> findAny()	// 아무거나 하나 반환, 병렬 스트림에 사용
```

**reduce()**

* 스트림의 요소를 하나씩 줄여가며 누적연산 수행함.

```java
Optional<T> reduce(BinaryOperator<T> accumulator)	// 초기값이 없으므로 Optional null 파악
T 	reduce(T identity, BinaryOperator<T> accumulator)	// identity - 초기값, accumulator - 이전 연산결과와 스트림의 요소에 수행할 연산

int count = intStream.reduce(0, (a,b) -> a + 1);
int sum = intStream.reduce(0, (a,b) -> a + b);

// 이것을 잘 알아두자
int a = identity;	// 누적 결과를 저장할 변수

for(int b : stream){
	a = a + b;	// sum()
}
```

### collect() 와 collectors

* 최종 연산 중에서도 가장 복잡하고 유용하게 활용될 수 있는 것이 collect()임.
* collect() 가 스트림의 요소를 수집하려면, 어떻게 수집할 것인가에 대한 방법이 바로 컬렉터(collector) 임.

```java
object collect(Collector collector)	// Collector 를 구현한 클래스의 객체를 매개변수로
object collect(Supplier supplier, BiConsumer accumulator, BiConsumer combiner)	// 잘안쓰임

public interface Collector<T, A, R> {	// T(요소)를 A에 누적한 다음, 결과를 R로 변환하여 반환
	Supplier<A> supplier();
	BiConsumer<A, T> accumulator();
	...
}

// 스트림 배열로 변환
Student[] stuNames = studentStream.toArray(Student[]::new);	// OK 람다식 : i -> new Student[i]
Student[] stuNames = studentStream.toArray();	// 에러
```

* reduce() 는 리듀싱 (스트림 요소 전체에 대한 리듀싱)
* collect() 는 그룹별 리듀싱의 차이점이 있음
* Collectors 클래스는 다양한 기능의 컬렉터를 제공함.

**스트림 통계**

* counting(), summingInt()

```
long count = stuStream.count();
long count = stuStream.collect(counting());	// Collectors.counting()
```

* collect 를 통해 그룹별로 총점 계산이 가능함.

**리듀싱 reducing()**

* collectors 가 제공함. reduce 와 동일하나 그룹별 리듀싱이 가능함.

```java
Collector reducing(BinaryOperator<T> op)
Collector reducing(T identity, BinaryOperator<T> op)
```

* joining() - 문자열 스트림의 요소를 모두 연결

```java
String studentNames = stuStream.map(Student::getName).collect(joining());
```

### 스트림의 그룹화화 분할

* partitioningBy()는 스트림을 2분할함.
* groupingBy()는 스트림을 n분할함.
* 둘 다 collectors에 있는 메서드임.

```java
Map<Boolean, List<Student>> stuBySex = stuStream.collect(partitioningBy(Student::isMale));	// 학생들을 성별로 분할
List<Student> maleStudent = stuBySex.get(true)	// Map에서 남학생 목록을 얻음
```

#### 스트림의 그룹화 - groupingBy()

```java
Map<Integer, List<Student>> stuByBan = stuStream.collect(groupingBy(Student::getBan, toList()));	// toList() 생략가능
```

</div>
</details>