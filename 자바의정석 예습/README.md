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


