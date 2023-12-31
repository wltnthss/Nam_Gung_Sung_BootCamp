# Day12 요약 및 헷갈리는 개념

## Design Pattern

* 객체 지향 설계 패턴이며 자주 쓰이는 디자인패턴 기억해두기. 나올 때마다 정리해서 하나씩 외워두자.

1. 싱글턴 패턴 ( SingleTon Pattern )
    * 클래스의 인스턴스, 즉 객체를 하나만 만들어 사용하는 패턴
2. 템플릿 메서드 패턴 ( Template Method Pattern )
    * 상위 클래스의 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴
3. 팩터리 메서드 패턴 ( Factory Mrthod Pattern )
    * 오버라이드된 메서드가 객체를 반환하는 패턴
4. 어댑터 패턴 ( Adapter Pattern )
    * 호출당하는 쪽의 메소드를 호출하는 쪽의 코드에 대응하도록 중간에 변환기를 통해 호출하는 패턴
5. 프록시 패턴 ( Proxy Pattern )
    * 제어 흐름을 조정하기 위한 목적으로 중간에 대리자(proxy)를 두는 패턴
6. 데코레이터 패턴 ( Decorator Pattern )
    * 메서드 호출의 반환값에 변화를 주기 위해 중간에 장식자를 두는 패턴
7. 옵저버 패턴(Observer Pattern)
    * 변화가 일어났을 때, 미리 등록된 다른 클래스에 통보해주는 패턴을 구현한 것. event listner가 대표적인 사용 예
8. 파사드 패턴(Facade Pattern)
    * 여러개의 객체와 실제 사용하는 서브 객체 사이에 복잡한 의존관계가 있을 때, 중간에 facade라는 객체를 두고, 여기서 제공하는 interface만을 활용하여 기능을 사용하는 방식
9. 전략 패턴 ( Strategy Pattern )
    * 클라이언트가 전략을 생성해 전략을 실행할 컨텍스트에 주입하는 패턴
    * 스프링의 DI 의존성기술은 이 전략패턴을 사용한 것

## 다형성

* 부모클래스 타입의 참조변수로 자식클래스의 인스턴스를 참조할 수 있도록 한 것.
* 어떤 타입에 대한 instanceof 연산의 결과가 true 라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻함.
* super.x, child.x, super.method(), this.method() 가 있으면 최신으로 오버라이딩된 자식의 메서드가 호출됨.
* 객체 배열 예제 다시 풀어보기.

### 객체 배열 예제

```java

// 부모클래스  Fruit 생성
public class Fruit {
	
	String name;
	int price;
	int fresh;
	int bP;
	
	public Fruit() {
		price = 0;
		fresh = 0;
	}

	public Fruit(int price, int fresh) {
		this.price = price;
		this.fresh = fresh;
		bP = (int)price / 10;
	}
}

// 자식 클래스 Grape
public class Grape extends Fruit{
	
	public Grape() {
		super(3000, 65);
	}

	@Override
	public String toString() {
		return "Grape";
	}
}

// 자식 클래스 Apple
public class Apple extends Fruit{

	public Apple() {
		super(2000, 90);
	}

	@Override
	public String toString() {
		return "Apple";
	}
}

import java.util.ArrayList;
import java.util.List;

// 구매자 클래스
public class Buyer {

	int money = 10000;
	int bP;
	List<Fruit> list = new ArrayList<Fruit>();
	
	public void buy(Fruit f) {
		if(f.price > money) {
			System.out.println("잔고가 부족합니다.");
			System.out.println(f + "을/를 구입하려면 "+f.price+"원이 필요합니다.");
			return;
		}
		money = money - f.price;
		bP = bP + f.bP;
		list.add(f);
		System.out.println(f+"을/를 구입하셨습니다.");
	}
	
	public void summary() {
		int sum = 0;
		String itemList = "";
		int gCnt  = 0;
		int aCnt  = 0;
		
		for (Fruit fruit : list) {
			sum += fruit.price;
			itemList += fruit + " ";
			if(fruit.toString().equals("Grape")) {
				gCnt++;
			}else if(fruit.toString().equals("Apple")) {
				aCnt++;
			}
		}
		
		System.out.println("현재 잔액은 "+money+"원 이고, 포인트는 "+bP+"입니다.");
		System.out.println("구입하신 총 금액은 " +sum+ "원 입니다.");
		System.out.print("구입하신 물건 리스트는 총 "+list.size()+"개 이며,");
		System.out.print("사과가 "+aCnt+"개 이고, 포도는 " +gCnt+"개 입니다.");
	}
}
```
```
Grape을/를 구입하셨습니다.
Apple을/를 구입하셨습니다.
Apple을/를 구입하셨습니다.
Grape을/를 구입하셨습니다.

현재 잔액은 0원 이고, 포인트는 1000입니다.
구입하신 총 금액은 10000원 입니다.
구입하신 물건 리스트는 총 4개 이며,사과가 2개 이고, 포도는 2개 입니다.
```