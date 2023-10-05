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