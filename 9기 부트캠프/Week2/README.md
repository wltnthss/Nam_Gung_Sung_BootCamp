# 둘째 주 

## 배열문제 연습 풀이.

		// 1. 하나의 배열에서 중복되는 수 찾아서 중복되는 수 출력
		
		// 2. 하나의 배열에서 중복되는 수 찾아서 중복되지 않는 수 출력
		
		// 3. 하나의 배열의 요소가 인접한 수 인지 체크 인접한 수이면 true 아니면 false
		
		// 4. 하나의 배엘여서 앞뒤 값 바꾸어 출력
		
		// 5. 하나의 배열에서 정렬해서 출력
		
		// 6. 하나의 배열에서 최대값 최소값 출력
		
		// 7. 숫자 야구 게임 (4자리 수) 
        
```java
package Practice;

import java.util.Arrays;
import java.util.Scanner;

public class Self_ArrayTestEx1_1 {
	public static void main(String[] args) {
		
		int[] arr1 = {0, 1, 3, 6, 7, 3, 4, 2, 7};
		int[] arr2 = new int[arr1.length];
		
		// 1. 하나의 배열에서 중복되는 수 찾아서 중복되는 수 출력  
		for (int i = 0; i < arr1.length; i++) {
			arr2[arr1[i]]++;
		}

		System.out.println("중복되는 수");
		for (int i = 0; i < arr2.length; i++) {
			if(arr2[i] > 1) {
//				System.out.print(i + " ");	// 3, 7
			}
		}
		// 2. 하나의 배열에서 중복되는 수 찾아서 중복되지 않는 수 출력
		System.out.println();
		System.out.println("중복되지 않는 수");
		for (int i = 0; i < arr2.length; i++) {
			if(arr2[i] == 1) {
//				System.out.print(i + " ");	// 0, 1, 2, 4, 6
			}
		}
		
		// 3. 하나의 배열의 요소가 인접한 수 인지 체크 인접한 수이면 true 아니면 false
		System.out.println();
		System.out.println("인접한 수 체크");
		int[] arr3 = {1 ,2, 3, 4, 5};
		int cnt = 0;
		
		for (int i = 1; i < arr3.length; i++) {
//			System.out.println("arr3[i] : " + arr3[i]);
//			System.out.println("arr3[i-1] : " + arr3[i-1]);
			if(arr3[i-1] + 1 == arr3[i]) {
				cnt++;
			}
		}
		
		if(cnt == 4) {
//			System.out.println(true);
		}else {
//			System.out.println(false);
		}
		
		System.out.println();
		System.out.println("앞뒤 값 바꾼 배열값");
		// 4. 하나의 배열여서 앞뒤 값 바꾸어 출력
		int[] arr4 = {5, 2, 7, 4, 8};
		// 8 4 7 2 5
		for (int i = arr4.length; i > 0; i--) {
//			System.out.print(arr4[i-1] + " ");
		}
		
		System.out.println();
		System.out.println("배열 요소 정렬");
		// 5. 하나의 배열에서 정렬해서 출력
		for (int i = 0; i < arr4.length; i++) {
//			System.out.println("arr4[i] : " + arr4[i]);
//			System.out.println("i : " + i);
			for (int j = 0; j < arr4.length; j++) {
				int k = arr4[j];
//				System.out.println("arr4[j] : " + arr4[j]);
				if(arr4[i] < arr4[j]) {
					int tmp = arr4[i];
					arr4[i] = arr4[j];
					arr4[j] = tmp;
				}
			}
		}
		
		for (int i : arr4) {
//			System.out.print(i + " ");
		}
		System.out.println();
		System.out.println("하나의 배열에서 최대값 최소값 출력");
		// 6. 하나의 배열에서 최대값 최소값 출력
		int[] arr5 = {7, 4, 6, 1, 5, 2, 9, 12};
		int max = arr5[0];
		int min = arr5[0];
		for (int i = 0; i < arr5.length; i++) {
			for (int j = 0; j < arr5.length; j++) {
				if(arr5[i] > max) {
					max = arr5[i];
					arr5[i] = arr5[j];
					arr5[j] = max;
				}else if(arr5[i] < min){
					min = arr5[i];
					arr5[i] = arr5[j];
					arr5[j] = min;
				}
			}
		}
//		System.out.println(max);
//		System.out.println(min);
		
		// 7. 숫자 야구 게임 (4자리 수)
		System.out.println();
		System.out.println("숫자 야구 게임 (4자리)");
		int count = 0;			// 5번 넘어가면 게임 종료
		int[] answer = {6, 3, 8, 5};
		int[] arr6 = new int[4];
		int S = 0;
		int B = 0;
		Scanner sc = new Scanner(System.in);
		
		do {
			for (int i = 0; i < arr6.length; i++) {
				arr6[i] = sc.nextInt();
				// 입력한 숫자와 answer을 비교
				if(arr6[i] == answer[i]) {
					S++;
				}else {
					B++;
				}
			}
			count++;
			System.out.println(S+"S"+B+"B 입니다.");
			if(S == 4) {
				System.out.println("정답입니다");
				break;
			}
			System.out.println("남은 시도 횟수는 " + (5-count) + " 회 입니다.");
			S = 0;
			B = 0;
			if(count == 5) {
				System.out.println("사용 시도 횟수를 초과했습니다.");
			}
		}while(count < 5);
	}
}
```		

## 다형성 (인터페이스, 추상화) 정리 및 예제 정리. 

### 인터페이스

* 추상화보다 더 유연하고 추상적이며 추상화 클래스가 미완성 설계도라면 인터페이스는 그 미완성 설계도를 그리는 밑그림.
* 추상 메서드의 집합이며 다중 상속이 가능함.
* 인터페이스도 필드를 선언할 수는 있지만 변수가 아닌 상수로서 정의가 가능함.
* public static final 과 public abstract 제어자는 생략 가능함.

```java
interface 인터페이스이름{
    public static final 타입 상수이름 = 값;
    public abstract 타입 메서드이름(매개변수목록);
}

// --------------------------------------------------------

interface TV {
    int MAX_VOLUME = 10; // public static final 생략 가능
    int MIN_VOLUME = 10;

    void turnOn(); // public abstract 생략 가능
    void turnOff();
    void changeVolume(int volume);
    void changeChannel(int channel);
}
```

![Alt text](image-2.png)

* 인터페이스는 extends 대신 implements 라는 구현이라는 키워드를 사용함으로써 부모 - 자식 관계를 연관시키는게 아닌 클래스를 확장 시켜 다양하게 이용하는데 중점을 둠.
* 클래스가 구현하는 인터페이스의 메서드 중 일부만 구현한다면 abstract 로 추상클래스로서 선언해야함.

```java
interface Animal {
    void walk();
    void run();
    void breed();
}

// Animal 인터페이스를 일부만 구현하는 포유류 추상 클래스
abstract class Mammalia implements Animal {
    public void walk() { ... }
    public void run() { ... }
    // public void breed() 는 자식 클래스에서 구체적으로 구현하도록 일부로 구현하지 않음 (추상 메서드로 처리)
}

class Lion extends Mammalia {
    @Override
    public void breed() { ... }
}
```

### 인터페이스 자체 상속

![Alt text](image-3.png)

* 인터페이스끼리의 상속은 다중 상속이 가능함.
* 클래스의 상속과 마찬가지로 자식은 부모의 정의된 멤버를 모두 상속 받음.
* 필드의 경우는 기본적으로 static 이므로 구현체를 따라가지 않음.

```java
interface Changeable{
    /* 채널을 바꾸는 기능의 메서드 */
    void change();
}

interface Powerable{
    /* 전원을 껐다 켰다 하는 메서드 */
    void power(boolean b);
}

// 채널 기능과 전원 기능을 가진 인터페이스들을 하나의 인터페이스로 통합 상속
interface Controlable extends Changeable, Powerable { 
	// 인터페이스끼리 다중 상속하면 그대로 추상 멤버들을 물려 받음
}

// 클래스에 통합된 인터페이스를 그대로 상속
class MyObject implements Controlable {
	public void change() {
        System.out.println("채널을 바꾸는 기능의 메서드");
    }
    public void power(boolean b) {
        System.out.println("전원을 껐다 켰다 하는 메서드");
    }
}

public class Main {
	public static void main(String[] args) {
        // 인터페이스 다형성 (인터페이스를 타입으로 취급해서 업캐스팅 가능)
        Controlable[] o = { new MyObject(), new MyObject() };
        o[0].change();
        o[0].power(true);
        
        // 각각 단일 인터페이스로도 타입으로 사용이 가능하다. (그러나 지니고 있는 추상 메서드만 사용이 가능하다)
        Changeable inter1 = new Changeable();
        inter1.change(); 

        Powerable inter2 = new Powerable();
        inter2.power(true);
    }
}

interface Iflower {
    int ex = 10; // 각각 public static final
}

interface IPlant extends Iflower {
    int ex = 20; // 각각 public static final
}

class Tulip implements IPlant {
    int ex = 30; // 그냥 인스턴스 변수
}

public class Main {
	public static void main(String[] args) {
        // 클래스 타입 객체로 ex 멤버에 접근하면, 클래스 인스턴스 변수로 접근
        Tulip t =  new Tulip();
        System.out.println(t.ex); // 30

        // 인터페이스 타입 객체로 멤버에 접근하면, 인터페이스 static 상수로 접근
        Iflower a = new Tulip();
        System.out.println(a.ex); // 10 - 좋지않은 방법
        System.out.println(Iflower.ex); // 10 - 클래스 static 처럼 '인터페이스.멤버' 로 접근

        IPlant b = new Tulip();
        System.out.println(b.ex); // 20 - 좋지않은 방법
        System.out.println(IPlant.ex); // 20 - 클래스 static 처럼 '인터페이스.멤버' 로 접근
    }
}
```

### default 메소드 

* 디폴트 메서드는 인터페이스 구현 이후, 모든 구현체들에게 함수를 만들어주고 싶을 때 사용됨.
* 접근 제어자가 public 이며 생략 가능하고, 자식 클래스에서 오버라이딩하여 재정의 가능함.

```java
interface Calculator {
    int plus(int i, int j);
    int multiple(int i, int j);

    // default로 선언함으로 메소드를 구현할 수 있다.
    default int sub(int i, int j){      
        return i - j;
    }
}

// Calculator인터페이스를 구현한 MyCalculator클래스
class MyCalculator implements Calculator {
    // 추상 메서드만 구현해줌
    @Override
    public int plus(int i, int j) { return i + j; }
    @Override
    public int multiple(int i, int j) { return i * j; }
}

public class Main {
    public static void main(String[] args){
        MyCalculator mycal = new MyCalculator();
        
        // 인터페이스 타입으로 업캐스팅
        Calculator cal = (Calculator) mycal; // 괄호 생략해도 됨

        // 인스턴스의 인터페이스 디폴트 메서드 호출
        int value = cal.sub(5, 10);
        System.out.println(value); // -5
    }
}
```

* 다중 인터페이스들 간의 디폴트 메서드 충돌

```java
interface A1{
    public void styleA();

    // 메소드 시그니처가 같은 디폴트 메서드
    default public void styleSame(){
        System.out.println("A1 인터페이스의 디폴트 메서드 입니다.");
    }
}

interface B1{
    public void styleB();

    // 메소드 시그니처가 같은 디폴트 메서드
    default public void styleSame(){
        System.out.println("B1 인터페이스의 디폴트 메서드 입니다.");
    }
}

class MultiInterface implements A1, B1 {
    @Override
    public void styleA() {}
    @Override
    public void styleB() {}

    // 두 인터페이스 디폴트 메서드중 A1 인터페이스의 디폴트 메서드를 오버라이딩 하여 구현
    default public void styleSame(){
        System.out.println("A1 인터페이스의 디폴트 메서드 입니다.");
    }
}

public class Main {
    public static void main(String[] args) {
        MultiInterface m1 = new MultiInterface();
        m1.styleSame(); // "A1 인터페이스의 디폴트 메서드 입니다."
    }
}
```

* 부모 클래스의 메서드가 상속되고 디폴트 메서드는 무시됨.
* 인터페이스 쪽의 디폴트 메서드를 사용할 필요가 있다면, 필요한 쪽의 메서드와 같은 내용으로 그냥 오버라이딩 해버리면 됨.

### default 메소드의 super

### 추상화

### 인터페이스, 추상화 동시 사용