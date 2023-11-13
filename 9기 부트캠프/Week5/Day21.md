# Day21 요약 및 헷갈리는 개념

## 12장 

1. Generics
    * **컴파일시 타입 체크**
    * 옛날버전에서는 Object 로만 타입을 체크했으나 지금은 제네릭클레스를 활용함.
    * **형변환 필요성 제거** , 코드 간결성
    * **타입 안전성 제공**
    * Object 범위는 너무 넓기에 모든 타입이 가능한 타입변수 T를 1개 지정함으로써 사용함.
    * 컴파일러가 타입을 체크하게 함으로써 OOP 설계에 유리한 장점을 가짐.
    * RuntimeException 을 컴파일러가 대신 하게 하기 위함.
        * NullPointException
        * ClassCastException
        * ArithmeticException
        * IndexOutOfBoundsException (Iterator 도 같은 기능)

```java
class Box<T>{
    T[] objArr;
    T getItem(int index {
        return objArr[index];
    })
}
```

* 인터페이스 구현를 구현할 때는 implements 가 아닌 extends 를 사용하며 & 기호로 연결함.

```java
class FruitBox<T extends Fruit & Eatable>
```

**와일드카드**

```java
<? extends T>   // T와 그 자손들이 가능함.
<? super T>     // T와 그 조상들이 가능함.
<?>             // 모든 타입이 가능함 (? extends Object)와 동일함.
```

* FruitBox<Fruit> -> FruitBox<? extends Fruit> 으로 바꾸면 Fruit에 속한 자식 타입이면 사용 가능함. (다형성 적용)

**지네릭메서드**

```java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

* 지네릭메서드 - 호출할 때마다 다른타입을 지정가능함
* 대입된 타입은 컴파일러가 추정하여 생략가능함.

```java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```

* 타입 T 를 요소로 하는 List를 매개변수로 받음.
* T는 Comparable을 구현한 클래스이어야하고, T 또는 그 조상의 타입을 비교하는 Comparable 이어야함.

2. Enumeration
    * 상수, 값에 이름을 붙인 것.
    * JDK 버전이 높아지며 값 + 타입까지 체크함. (다른 언어에서도 활용을 많이 함)
    * ex) int i = MAX_VALUE; 

3. Annotation
    * Comment - 주석역할로 활용하기 시작함 (@Tests, @Override)

**열거형(enum)**

```java
class Card{
    enum Kind {CLOVER ...}
    enum Value { TWO ...}

    final Kind kind;
    final Value value
}
```

* 타입이 Kind, Value에 유의하기.
* 열거형은 하나하나가 객체임.
* 생성자는 private -> 객체를 제한하기위함.
* 모든 열거형은 추상 클래스 Enum 의 자식임. (객체를 생성하지 말고 부모클래스로 사용하지 않기 위함)
* 열거형은 객체인 것을 명심하고 넘어가자.

**애너테이션**

* 주석처럼 사용하며 프로그래밍에 영향은 주지 않으면서 유용한 정보를 제공함.

> 지네릭스 이해안된 부분 강의 다시 보기
