# Nam_Gung_Sung_BootCamp
남궁성강사님 9기 부트캠프 (23.10.16 ~ 24.03.15)

1. 프로그래밍 기초(4주) - 알고리즘 기본(400문제), Java, 객체지향개념과 설계, TDD, HTML & CSS
2. 웹프로그래밍(4주) - Spring + MyBatis, SQL기본(MySQL), JavaScript기본, Web기본
3. 개인 프로젝트(4주) - Spring으로 쇼핑몰 만들기, JavaScript심화, DB모델링, git, Spring Boot + JPA
4. 팀 프로젝트(8주) - 1차 개발, 교차 테스트, 1차 개발 리뷰, 2차 개발, 최종 테스트, 2차 개발 리뷰. 프로젝트 발표


## 자바의 정석 나만의 요약집 정리 1~13장 

<details>
<summary style="font-size:20px">자바의 정석</summary>
<div markdown="1">

**기본형타입 8가지**

* boolean(1), char(2), byte(1), short(2), int(4), long(8), float(4), double(8)

**객체지향 4대 핵심개념 적고, 한줄로 설명**

1. 캡슐화 : 외부로부터 데이터를 보호하기 위해서
2. 상속 : 두 클래스를 자식,부모관계를 맺어주고 기존 클래스로부터 새로운 클래스를 작성하는 것
3. 추상화 : 클래스의 공통된 기능을 모아서 부모 클래스로 만드는 것
4. 다형성 : 부모 타입의 참조변수로 자식 클래스의 인스턴스를 생성하는 것

**객체지향 특징 세 가지**

1. 코드의 재사용성
2. 유지보수 용이
3. 코드 중복 제거

**클래스**

* 정의 및 용도 : 객체를 정의하고 생성해서 사용하기 위함.

1. 객체를 정의해놓은 설계도
2. 사용자 정의 타입
3. 변수 + 메서드의 묶음

* 클래스를 인스턴스화 -> 인스턴스(객체)

**객체**

* 실제로 존재하는 것 (인스턴스 변수의 묶음)
* 객체 == 인스턴스

**변수의 종류**

1. 클래스영역 
   1. cv : 클래스변수 - 클래스가 메모리에 올라갈 때 생성, 객체를 생성할 필요 X, 공통적인 속성으로 사용
   2. iv : 인스턴스변수 - 객체를 생성할 때 생성, 객체를 생성해야 사용 가능, 개별 속성으로 사용
2. 메서드영역
   1. lv : 지역변수 - 클래스이외의 영역 (메서드, 생성자, 초기화블럭), 메서드 종료시 자동제거됨.

* cv는 하나의 저장공간을 공유하므로 항상 공통된 값을 갖고 iv는 각기 다른 값을 가짐.

**클래스메서드와 인스턴스메서드**

* static 메서드는 인스턴스 메서드 사용 불가 why? 
  * static 메서드는 클래스가 메모리에 올라갈 때 생성되는 반면 객체는 생성시에 만들어지므로 없을 경우가 있을 수도 있어서.
* 인스턴스 메서드에서는 static 메서드를 호출 가능함.

**static을 붙이는 경우**

1. 클래스의 멤버변수 중에서 모든 인스턴스에 공통된 값을 유지하는 경우 static을 붙임.
2. 인스턴스 변수나, 인스턴스 메서드를 사용하지 않는 메서드에 static을 붙임.
   
**오버로딩 조건3가지**

1. 메서드의 이름이 같아야함.
2. 매개변수의 타입이나 개수가 달라야함.
3. 반환타입은 영향이 없음.

**오버라이딩 조건3가지**

1. 부모타입의 예외개수보다 적어야함.
2. 부모타입의 접근 제어자보다 좁으면 안됨. 
3. 선언부가 일치함.

**생성자 조건5가지**

* 인스턴스 초기화 메서드

1. 클래스와 이름이 같아야함.
2. 리턴값이 없음.
3. 생성자는 반드시 한 개 존재해야함.
4. 생성자가 없으면 컴파일러가 기본 생성자를 하나 생성해줌.
5. 생성자의 첫째 줄에는 this() 나 super()가 들어가야함.

**생성자 this()**

1. 생성자에서 다른 생성자를 호출할 때 this()를 사용함.
2. 다른 생성자 호출 시 첫 줄에서만 사용 가능함.(다른 생성자로 인해 호출이전의 초기화 작업이 무의미하므로)

**참조변수 this**

* 인스턴스 변수와 지역변수의 이름이 같을 때 구분하기위함.
* this가 붙으면 iv이고 안붙으면 매개변수와 가까운 lv임.
* 인스턴스 자신을 가르키는 참조변수.
* static 메서드에서는 사용 불가함.

**클래스 변수, 인스턴스 변수 초기화 순서 과정**

* 멤버변수 - 자동초기화, 지역변수 - 직접 초기화해줘야함.
* 클래스변수는 클래스가 메모리에 올라갈 때 초기화되고, 인스턴스 변수는 인스턴스가 생성될 때 초기화됨.

* 클래스 변수
1. 기본값 -> 명시적 초기화 -> 클래스 초기화 블럭 static{} 
   
* 인스턴스 변수
1. 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블럭 {} -> 생성자

* cv -> iv 순으로 초기화되며, 자동(기본값) -> 간단(명시적 초기화) -> 복잡순(초기화 블럭, 생성자) 으로 초기화됨.

**기본형 매개변수, 참조형 매개변수**

* 기본형 매개변수는 변수의 값을 읽기만 가능
* 참조형 매개변수는 변수의 값을 읽고 변경 가능

**상속**

1. 기존 클래스로 다른 클래스를 작성하는 것
2. 두 클래스간의 부모와 자식으로 관계를 맺어주는 것
3. 자식의 멤버개수는 부모보다 적을 수 없음.
4. 자식은 부모의 모든멤버를 상속받음(생성자, 초기화블럭 제외)

* 자바는 단일상속만 허용함 (비중이 높은 클래스만 상속하고, 나머지는 포함관계 활용)
* 자식클래스 extends 부모클래스
* 상속 관계 ~는 ~이다 ( is a 관계)
* 포함 관계 ~는 ~를 가지고 있다 ( has a 관계) **(대부분의 경우 포함관계임)**

**Objects클래스는 iv가 하나도 없는데, 인스턴스 메서드를 가지는 이유**

* Objets 클래스는 모든 클래스의 부모 클래스로 자식 클래스들이 오버라이딩해서 iv를 쓸 수 있기 때문임.

**참조변수 super**

* 객체 자신을 가르키는 참조변수
* 조상의 멤버를 자신의 멤버와 구분할 때 사용

**부모 생성자 super()**

1. 부모 생성자 호출 시 사용 (생성자와 초기화 블럭은 상속이 안되므로)
2. 부모 멤버는 부모의 생성자를 호출해서 초기화
3. 자식의 생성자는 자신이 선언한 변수만 초기화 할 수 있음.
4. 생성자의 첫 줄에 반드시 생성자를 호출해야함.

**접근제어자**

* public > protected > default > private 
* 전체 > 같은 패키지, 자식 클래스 > 같은 패키지 > 같은 클래스 순으로 접근 제어 권한을 가짐.

1. 외부로부터 데이터를 보호하기 위함
2. 외부에는 불필요한, 내부적으로만 사용되는 부분을 감추기 위함.

**final**

1. 클래스 - 상속이 불가능함.
2. 메서드 - 오버라이딩이 불가능함.
3. 변수 - 상수로써 활용함.

**다형성**

1. 부모타입 참조변수로 자식타입 객체를 다룰 수 있음.
2. 하나의 배열에 여러 종류의 객체를 저장할 수 있음.

* 참조변수가 사용할 수 있는 멤버의 개수는 인스턴스 멤버개수보다 같거나 적어야함.
* 참조변수타입과 인스턴스타입은 보통 일치하지만 일치하지 않을 수도 있음.

**추상클래스**

1. 미완성 설계도
2. 인스턴스로 생성불가
3. 인스턴스 변수, 생성자, 메서드를 일반 클래스와 같이 사용 가능
4. abstract 가 붙은 메서드는 자식 클래스에서 용도에 맞게 오버라이딩하여 사용함.
5. 클래스의 공통적인 기능을 찾아내서 부모클래스로 만듬으로써 사용함.

**인터페이스**

1. 추상메서드의 집합
2. 밑그림 역할
3. 인스턴스화 할 수 없으며 상수와, 추상메서드만을 가질 수 있음.
4. 추상클래스보다 추상화 정도가 높음.

* 인터페이스의 조상은 인터페이스만 가능(Object가 최고조상이 아님)
* 다중 상속 가능이 가능함.
* public, static, final, abstract 전부 생략 가능함.
* 상속과 구현 동시에 가능함.
* 인터페이스 타입의 변수로 인터페이스를 구현한 클래스의 인스턴스 참조 가능함.
* 일부만 구현할 경우 클래스앞에 abstract를 붙여서 추상 클래스로 만들어줘야함.

**인터페이스 장점**

1. 두 객체간의 중간 역할을 함으로써 객체간에 느슨한 결합을 가능하게 도와줌.
2. 서로 관계없는 클래스들을 형제 관계로 맺어줌으로써 활용 가능함.
3. 설계를 진행할 때 밑그림의 역할로 인터페이스를 활용하면 재사용성에 용이함.

**추상클래스 vs 인터페이스**

* 추상적인 용도는 동일하게 쓰이나 인터페이스는 iv, 생성자를 가질 수 없음

**예외**

* 예외처리 정의 - 예외 발생에 대비한 코드 작성
* 예외처리 목적 - 프로그램의 비정상적인 종료 방지

**에러 3가지**

1. 컴파일에러 : 컴파일 시에 발생하는 에러
2. 런타임에러 : 프로그램 실행 시에 발생하는 에러
3. 논리적에러 : 프로그래머의 작성 의도와 다르게 동작하는 것

**예외 클래스**

1. Exception 클래스들 : 사용자의 실수와 같은 외적인 요인에 의해서 발생하는 예외
2. RuntimeException 클래스들 : 프로그래머의 실수로 발생하는 예외

**예외 처리 방법5가지**

1. try-catch-finally - 예외 발생한 메서드 안에서 처리
2. 메서드 예외 선언
3. 예외 강제로 발생 시키기
4. 사용자 예외 선언
5. 예외 되던지기

**연결된 예외 장점2가지**

1. check예외를 unchecked예외로 바꿀 수 있음.
2. 큰 분류의 예외로 묶어서 사용할 수 있음.

**checked예외를 unchecked예외로 바꿔서 사용하는 이유**

* 예외처리를 선택적으로함으로써 무분별한 try-catch 문을 사용하지 않기 위함

**얕은 복사와 깊은 복사**

1. 얕은 복사 : 원본과 복사본이 같은 객체를 참고하며 단순 Cloneable 인터페이스를 구현한 clone 을 통한 복제를 사용함.
2. 깊은 복사 : 원본과 복사본이 다른 객체를 참고하고 원본의 객체를 복사하여 참조함.

**불변이란?**

* 객체 생성 후에 상태를 변경할 수 없는 것
* 재할당은 가능하지만 한번 할당하면 내부 데이터는 변경할 수 없음.
* 대표적인 불변 객체로는 String이 있음.
* 필드에서 사용할 때는 final을 붙여서 사용함.

1. 멀티쓰레드 환경에서 동기화를 고려하지 않아도됨.
2. GC 성능 향상.

**StringBuffer vs StringBuilder**

* 두 가지 모두 자신의 주소를 반환하며 가변적인 문자열을 다룰 때 유리함.
* StringBuffer는 동기화를 지원하고, StringBuilder는 동기화를 지원하지 않습니다.
* 쓰레드와 관련이 없으면 성능은 StringBuilder > StringBuffer > String 이므로 관련이 없을 때는 이와 같이 사용하자.
* 사용법은 동일함.

**Math 클래스 생성자가 private인 이유?**

* Math 클래스는 인스턴스변수가 하나도 없어서(전부 static) 인스턴스를 생성할 필요가 없기 때문임.

**래퍼클래스**

* 기본형 값들을 객체로 변환하여 작업을 수행할 때 사용함.
* 오토박싱 : 기본형 값을 래퍼 클래스의 객체로 자동 변환

**컬렉션 프레임웍**

* 컬렉션 : 다수의 객체를 모아놓은 것
* 프레임웍 : 표준화된 프로그래밍 방식
* 컬렉션 프레임웍 : 다수의 객체를 모아놓은 표준화된 프로그래밍 방식

**컬렉션 프레임웍 핵심 인터페이스**

1. List
   * 순서 O, 중복 O
   * LinkedList, ArrayList, Stack, Vector
   * Collection 인터페이스를 상속받고 있음
2. Set
   * 순서 X, 중복 X
   * HashSet, TreeSet
   * Collection 인터페이스를 상속받고 있음
3. Map
   * 순서 X, Key 는 중복 X, Value 는 중복 O

**ArrayList**

* Vector는 동기화되어있지만 ArrayList는 동기화되어있지 않음.
* List 인터페이스를 구현하여 순서가 유지되고 중복을 허용함.

**ArrayList 삭제과정**

1. ArrayList는 index 번째 요소를 삭제함. ex) data[0] ~ data[5]
2. 중간 데이터 data[2] 2번째 요소를 삭제한다는 가정하에 list.remove(2); 호출함.
3. 삭제할 데이터 아래의 데이터를 한칸씩 위로 복사하여 삭제할 데이터 덮어씌우기
4. System.arraycopy(data, index+1, data, index, size-index-1)
5. 데이터가 한칸씩 옮겨졌으므로 마지막 데이터는 null로 변경 data[size-1] = null;
6. 데이터가 삭제되었으므로 size하나 감소 size--;
7. 마지막 데이터를 삭제하는 경우는 복사과정을 건너띄고 5번부터 수행함.

**LinkedList**

* 다음요소와 이전요소의 주소, 데이터를 저장할 수 있음.
* ArrayList에 비해서 접근 속도는 느리나, 비순차적인 데이터의 추가/삭제는 빠름.
* ArrayList가 접근 속도는 더 빠르고, 순차적인 데이터의 추가/삭제는 더 빠름.

**스택 & 큐**

* 스택 (Stack) - LastInFirstOut (LIFO) 구조 ex) 수식괄호검사, 브라우저 뒤/앞
  * 저장 - push(), 추출 - pop()
  * ArrayList 로 구현하는 것이 유리함
* 큐 (Queue) - FirstInFirstOut (FIFO) 구조 ex) 최근사용문서, 버퍼
  * 저장 - offer(), 추출 - poll()
  * LinkedList 로 구현하는 것이 유리함 (데이터를 꺼낼 때마다 데이터 복사가 발생)

**Comparator와 Comparable**

* Comparable - 기본 정렬기준을 구현하는데 사용하며 기본적으로 제공하는 인터페이스임.
* Comparator - 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용.

**이진 검색 트리(binary search tree)**

1. 모든 노드는 최대 두 개의 자식노드를 가질 수 있음
2. 왼쪽 자식 노드 값이 부모 노드의 값보다 작고 오른쪽은 부모보다 커야함.
3. 검색과 정렬에 유리함.
4. 노드의 추가 삭제에 시간이 오래 걸림(배열보다 느림)
5. TreeSet, TreeMap 사용

**해싱**

* 해시함수를 이용해서 해시테이블에 데이터를 저장하고 검색하는 기법
* ArrayList와 LinkedList 의 조합
  
**지네릭스**

* 컴파일시 타입 체크를 해주는 기능

1. 타입 안전성 제공
2. 형변환 생략으로 코드 간결성 향상

**지네릭스 제약 2가지**

1. static 멤버에 타입 변수 사용 불가
2. 배열 생성할 때 타입 변수 사용 불가.

**제한된 지네릭 클래스**

* extends 로 대입할 수 있는 타입을 제한함.

```java
<T extends Animal> // Animal 의 자식타입만 지정가능함.
```

**와일드카드**

* 하나의 참조 변수로 대입된 타입이 다른 객체를 참조 가능

```java
<? extends T>  - T의 자손들 저장 가능
<? super T>    - T의 부모들 저장 가능
<?>            - 모든 타입이 가능 (T extends Object와 동일함) 
```

**지네릭 메서드**

* 메서드 선언부에 지네릭 타입이 선언된 메서드 
* 메서드를 호출할 때마다 타입을 대입할 수 있음.

```java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

**열거형**

* 관련된 상수들을 묶어 놓은 것.
* enum 클래스 에 정의된 값들은 객체.
* 열거형의 생성자는 private(외부의 호출을 막기위함)

**애너테이션**

* 프로그래밍에 영향을 주지 않고 주석처럼 사용하며 유용한 정보를 제공함.
* 메타 애너테이션 : 애너테이션의 적용대상이나 유지기간을 지정하는데 사용함. (@Target, @Inherited)

**프로세스와 쓰레드**

* 프로그램 : 실행 가능한 파일(HDD, SSD에 존재함)
* 프로세스 : 실행중인 프로그램 (공장)
  * 모든 프로세스에는 최소한 하나 이상의 쓰레드가 존재함
  * 데이터, 메모리, 자원, 쓰레드로 구성되어있음
* 쓰레드 : 하나의 프로세스 자원으로 작업을 수행하는 것 (일꾼)
  * Thread 상속과, Runnable 구현 방법 2가지.
  * 한번 실행된 쓰레드는 재사용 불가함.

**멀티쓰레드**

* 하나의 프로세스 안에서 여러 쓰레드가 동시에 작업을 수행하는 것.
* 동기화, 교착상태의 단점이 존재함.
  
**멀티쓰레드 장점**
  * 자원 효율적 사용
  * CPU의 사용률 향상
  * 사용자 응답성 향상
  * 코드 간결화

**싱글쓰레드 vs 멀티쓰레드**

* 멀티쓰레드는 사용자의 입력을 기다리는 동안 다른 쓰레드가 작업하므로 효율적인 CPU 사용 가능
* 멀티쓰레드는 두 쓰레드가 번걸아가면서 작업할 때 발생하는 작업전환으로 인해 시간이 더 소요됨.

**병행과 병렬**

* 병행 : 여러 작업을 동시에 작업하는 것
* 병렬 : 큰 작업을 나누어 작업하는 것

**데몬쓰레드**

* 일반 쓰레드의 작업을 돕는 보조적인 역할을 수행 
* 일반 쓰레드가 종료되면 데몬 쓰레드는 강제 종료됨.
* ex) GC, 화면자동갱신

**쓰레드의 실행제어**

1. 생성 start()
2. 생성 후 실행대기상태 (RUNNABLE)
3. 실행상태에서 yield() 양보하면 다시 실행대기상태, stop() 하면 소멸(TERMINATED)
4. 실행상태에서 suspend(), wait(), join(), sleep(), I/O block 하면 일시정지 상태 (WAITING)
5. 일시정지 상태(WAITING)에서 resume(), interrupt(), notify() 하면 다시 실행대기상태(RUNNABLE)

* sleep()과 yield()는 static 메서드이므로 자기 자신에게 사용 가능함.

**쓰레드 동기화**

* 한 쓰레드가 작업중일 때 다른 쓰레드가 간섭하지 못하도록 막는 것 (synchronize)
  * 메서드 전체 임계 영역 설정
  * 특정한 영역 임계 영역 설정
* 공유 데이터를 사용하는 임계영역은 lock을 획득한 하나의 쓰레드만 수행가능, lock을 반납해야 다른 쓰레드가 수행가능함.

**Lock과 Condition 동기화**

* wait()과 notify()를 개선한 방법

1. ReentrantLock - 배타 lock 으로 재진입이 가능한 lock, Mutex 뮤텍스 특징을 가짐
2. ReentrantReadWriteLock - 공유 lock으로 읽기에는 공유적이고, 쓰기에는 배타적인 lock, Semaphore 세마포어 특징을 가짐
3. StampedLock - 공유 lock에 낙관적 lock 가능 추가, true && false 로 lock 설정가능함.

**volatile**

* 자주 바뀌는 값이며, 캐시의 값 불일치를 해소시켜줌

**fork & join 프레임웍**

* 병렬처리를 쉽게 해주기 위함.
* compute() 추상 메서드를 통해 구현하여 사용.
* fork() - 작업을 나누는 비동기 메서드
* join() - 작업을 합치는 동기 메서드

**스트림**

1. 스트림 생성 
2. 중간 연산 (n번 수행 가능)
    * skip, limit, distinct, filter, map, flatmap, peek, sorted
3. 최종 연산 (1번)
    * foreach, sum, count, max, min, allMatch, anyMatch, noneMatch, findFirst, reduce, collect

</div>
</details>


## ORACLE 나만의 요약집 정리

<details>
<summary style="font-size:20px">ORACLE</summary>
<div markdown="1">

**DDL,DML, DCL, TRANSACTION**

1. DDL  
    * CREATE, ALTER, DROP, RENAME, TRUNCATE, COMMENT
2. DML
    * SELECT, INSERT, UPDATE, DELETE
3. DCL
    * GRANT, REVOKE
4. TRANSACTION
    * COMMIT, ROLLBACK, SAVEPOINT

**DISTINCT**

* SELECT 절에 DISTINCT 키워드를 통해서 중복을 제거 가능함.
* 컬럼이 여러 개면 여러 개의 컬럼에 대해서 중복을 제거함.
* FOR문을 돌면서 중복을 제거하기 때문에 성능이 좋지 않음.
* GROUP BY 도 중복을 제거해주지만 GROUP BY 는 집게함수를 쓸 때 사용하고 그게 아니면은 가독성이 좋은 DISTINCT 를 사용하자.

**DISTINCT COUNT연산 파히기**

```SQL
SELECT p_date
	, COUNT(DISTINCT column_name)
FROM table_name
WHERE p_date BETWEEN DATE_FORMAT('20211006', 'yyyy-MM-dd') AND DATE_FORMAT('20211008', 'yyyy-MM-dd')
GROUP BY p_date

-- 튜닝 후 
SELECT p_date
	, COUNT(column_name)
FROM (
	SELECT p_date
	    , column_name
	FROM table_name
	WHERE p_date BETWEEN DATE_FORMAT('20211006', 'yyyy-MM-dd') AND DATE_FORMAT('20211008', 'yyyy-MM-dd')
	GROUP BY p_date, column_name
) tmp
GROUP BY p_date
```

* 튜닝 후에 수정된 쿼리는 서브 쿼리 안에서 GROUP BY 를 통해 중복이 제거된 중간 데이터 결과 셋을 생성함.
* GROUP BY 연산은 다수의 리듀스가 작업을 분배하여 처리하여 결과적으로 제일 바깥에 있는 COUNT 연산은 크기가 감소된 중간 데이터 결과 셋을 입력으로 사용함.

**ORACLE JOIN**

1. INNER JOIN 

    * EQUIJOIN - 컬럼이 있는 값들이 = 연산자를 사용하여 정확하게 일치하는 경우
    * NON-EQUIJOIN - 한 컬럼의 값이 다른 컬럼의 값과 정확히 일치하지 않는 경우

```SQL
-- EQUI JOIN 
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID = D.ID;
    
-- ANSI INNER JOIN
SELECT 
    *
FROM 
    S_EMP E INNER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;
```
2. OUTER JOIN

    * OUTER JOIN : 조인 테이블의 값이 존재하지 않아도 메인 테이블 데이터가 조회됨. 조인 테이블의 값을 가져오지 못하면 NULL로 표시됨.
        * LEFT OUTER JOIN - 왼쪽 테이블이 메인 테이블이 되며 조인 컬럼에 (+) 를 붙이면 해당 컬럼의 테이블이 조인 테이블이됨.
        * RIGHT OUTER JOIN - 오른쪽 테이블이 메인 테이블이 되며 조인 컬럼에
        (+) 를 붙이면 해당 컬럼의 테이블이 조인 테이블이됨. (특별한 경우가 아닌 이상 RIGHT OUTER JOIN을 사용하는 경우는 드뭄)
    * FULL OUTER JOIN : ANSI JOIN 에서만 사용하고 조인되어도 조회되고 조인이 안되어도 모두 조회됨. (자주 쓰이지는 않음)

```SQL
-- LEFT OUTER JOIN     
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D 
WHERE 
    E.DEPT_ID = D.ID(+);
    
-- RIGHT OUTER JOIN
SELECT 
    *
FROM   
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID(+) = D.ID;
    
-- ANSI LEFT OUTER JOIN 
SELECT 
    *
FROM 
    S_EMP E LEFT OUTER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;
    
-- ANSI RIGHT OUTER JOIN
SELECT 
    *
FROM 
    S_EMP E RIGHT OUTER JOIN S_DEPT D
    ON E.DEPT_ID = D.ID;
```     
3. SELF JOIN 

    * SELF JOIN : 1개의 테이블에 두 개의 별칭을 부여해서 2개의 테이블인 것처럼 간주한 뒤 JOIN하는 방법, 다른 컬럼을 통해서 위계 또는 관계를 알 수 있는 모습으로 조회할 수 있음.

```SQL
-- SELF JOIN
SELECT 
    W.ID 사번,
    W.NAME 사원명,
    M.ID 매니저아이디,
    M.NAME 매니저이름    
FROM 
    S_EMP W, S_EMP M
WHERE 
    W.MANAGER_ID = M.ID;

-- 김정미와 같은 직책을 가지는 사원의 이름, 직책, 급여, 부서번호 
-- 서브 쿼리 활용
SELECT
    NAME, TITLE, SALRAY, DEPT_ID
FROM 
    S_EMP
WHERE 
    1=1
    AND TITLE = (SELECT 
                    TITLE
                FROM
                    S_EMP
                WHERE
                    NAME = '김정미')
    AND NAME <> '김정미';

-- SELF JOIN 활용 
SELECT 
    E2.NAME, E2.TITLE, E2.SALARY, E2.DEPT_ID
FROM 
    S_EMP E1, S_EMP E2
WHERE
    1=1
    AND E1.TITLE = E2.TITLE
    AND E1.NAME = '김정미'
    AND E2.NAME != '김정미';
```

4. CROSS JOIN

    * CROSS JOIN : 두 테이블의 데이터가 서로 한번씩 조인되므로 테이블행은 조회된 메인 테이블과 조인 테이블의 행의 개수를 * 해줌.

```SQL
-- CROSS JOIN 
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D
WHERE 
    1=1
    AND E.TITLE = '사원'
    AND D.NAME = '영업부';
    
-- ANSI CROSS JOIN 
SELECT 
    *
FROM 
    S_EMP E CROSS JOIN S_DEPT D
WHERE 
    1=1
    AND D.NAME = '영업부'
    AND E.TITLE = '사원';
```

**SET연산자**

* 중복된 건을 배제한 작업을 수행한 후에 집한 연산을 적용함.
* UNION 은 중복 작업을 진행한 뒤에 연산을 수행하므로 UNION ALL보다 쿼리 성능이 좋지 않음.(당연한 것)

1. UNION : 중복을 제거한 합집합
2. UNION ALL : 합집합
3. INTERSECT : 교집합
4. MINUS : 차집합

**SUBQUERY**

1. 스칼라 서브 쿼리 
    * SELECT 절에 사용하며, 단일 컬럼(1개의 값)을 반환함.
    * 다중 행의 값이 조회되면 오류발생.

```SQL
    SELECT 
        ID,
        NAME,
        TITLE, 
        DEPT_ID,
        (
            SELECT 
                NAME DNAME
            FROM 
                S_DEPT D
            WHERE 
                E.DEPT_ID = D.ID
                AND NAME = '기획부'
        ) DNAME
    FROM 
        S_EMP E
```

2. 인라인 뷰
    * FROM 절에 사용하며, VIEW와 사용적인 측면에서 동일함

```SQL
-- 부서별로 평균 급여보다 높은 급여를 받는 사원은?
SELECT 
    *
FROM 
(
    SELECT 
        ID,
        NAME,
        SALARY,
        DEPT_ID,
        (
        SELECT 
            AVG(SALARY)
        FROM 
            S_EMP E1
        WHERE 
            E1.DEPT_ID = E2.DEPT_ID
        GROUP BY 
            DEPT_ID
        ) AV_SALARY
    FROM 
        S_EMP E2
) A
WHERE 
    A.SALARY > A.AV_SALARY;
```

3. 중첩 서브 쿼리
    * WHERE, HAVING 절에 사용하며, 다중 컬럼 또는 다중 행을 반환함.

```SQL
-- 부서별로 평균 급여보다 높은 급여를 받는 사원은?
SELECT 
    E1.NAME,
    E1.SALARY
FROM 
    S_EMP E1
WHERE 
    E1.SALARY > 
            (
                SELECT 
                    AVG(SALARY) 평균급여
                FROM 
                    S_EMP E2
                WHERE 
                    E1.DEPT_ID = E2.DEPT_ID
                GROUP BY 
                    DEPT_ID
            );
```

**CONSTRAINT**

* 데이터의 무결성을 지키기 위해 제한된 조건
* 즉, 테이블이나 속성에 부적절한 데이터가 들어오는 것을 사전에 차단하도록 정해 놓은 것

* NOT NULL
    * NULL값 설정 불가
* UNIQUE
    * 중복간 설정 불가
* CHECK
    * 지정한 조건에 맞지 않는 값은 설정할 수 없음.
* PRIMARY KEY
    * 테이블에는 단 하나의 PK만 허용됨.
    * UNIQUE 컬럼에 대한 인덱스가 자동 생성됨.
    * 중복값과 NULL값 설정 불가
* FOREIGN KEY
    * 부모 테이블의 값과 일치하거나 NULL 이어야함.
    * 참조하고자 하는 컬럼이 PK 또는 UNIQUE 제약조건이 있어야함.
* DEFAULT

```SQL
-- 제약 조건 조회
SELECT * FROM USER_CONSTRAINTS WHERE TABLE_NAME = 'S_EMP';

-- 제약 조건 추가
ALTER TABLE S_EMP MODIFY MAILID NOT NULL;
ALTER TABLE S_EMP ADD CONSTRAINT UNIQUE_MAILID UNIQUE(MAILID);
ALTER TABLE S_EMP ADD CONSTRAINT PK_ID PRIMARY KEY(ID);

-- 제약 조건 삭제
ALTER TABLE S_EMP DROP CONSTRAINT PK_S_EMP;
ALTER TABLE S_EMP DROP CONSTRAINT UNIQUE_MAILID;
```

**DICTIONARY**

* 데이터베이스에 대한 정보를 가짐
* ORACLE SERVER에 의해서 생성되고 유지보수

**SEQUENCE**

* 오라클에서는 자동 증가 컬럼을 사용할 수가 없음.
* 때문에 오라클에서 컬럼의 값을 증가시키기 위해서는 주로 시퀀스를 사용함

* INCREMENT BY : 시퀀스 실행 시 증가시킬 값
* START WITH : 시퀀스의 시작값이다. (MINVALUE과 같거나 커야 한다)
* MINVALUE : 시퀀스가 시작되는 최솟값이다.
* MAXVALUE : 시퀀스가 끝나는 최댓값이다.
* NOCYCLE | CYCLE : NOCYCLE (반복안함), CYCLE(시퀀스의 최댓값에 도달 시 최솟값 1부터 다시시작)
* NOCACHE | CACHE : NOCACHE(사용안함), CACHE(캐시를 사용하여 미리 값을 할당해 놓아서 속도가 빠르며, 동시 사용자가 많을 경우 유리)
* NOORDER | ORDER : NOORDER(사용안함), ORDER(요청 순서로 값을 생성하여 발생 순서를 보장하지만 조금의 시스템 부하가 있음)

```SQL
-- 해당 유저에 생성된 모든 시퀀스 확인 방법
SELECT * FROM user_sequences;

-- SEQUENCE 생성
CREATE SEQUENCE ID
    INCREMENT BY 1
    START WITH 26
    MINVALUE 1
    MAXVALUE 99999
    NOCYCLE
    NOCACHE
    NOORDER;

-- SEQUENCE 삭제
DROP SEQUENCE ID;

-- SEQUENCE 수정
ALTER SEQUENCE ID MAXVALUE 9999;
ALTER SEQUENCE ID INCREMENT BY 2;

-- SEQUENCE 사용, NEXTVAL을 사용하여 일련번호를 생성할 수 있음.
SELECT 
    ID.NEXTVAL
FROM 
    DUAL;
```
**INDEX**

* 테이블의 데이터를 좀 더 빠르게 검색하기 위해 사용하는 데이터베이스 Object.
* ORACLE SERVER 가 최적화 방법을 따라 어떤 Index를 사용할 것인지, 사용하지 않을 것인지 결정
* B+Tree 의 검색방법으로 디스크 입출력 횟수를 줄임.
* 자동으로 생성되기도 하고 사용자가 필요에 의해 만들기도함.
* INDEX는 논리적, 물리적으로 테이블과는 독립적임.
* ORACLE SERVER가 자동적으로 INDEX를 사용하고 유지보수함.
* 인덱스는 검색속도를 증가시키지만 항상 빠른 것은 아니고, 많이 만든다고해서 좋은 것도 아님.
* 테이블과 연관된 인덱스가 많을 수록 오라클 서버 부담은 증가함.

```SQL
-- INDEX 조회
SELECT * FROM IND;

-- INDEX 생성
-- CREATE INDEX INDEX_NAME ON TABLE_NAME(COLUMN...)
CREATE INDEX T_INDEX ON S_EMP(NAME);
```

**INDEX 효율적 사용**

1. INDEX가 존재하지만 사용되지 않는 경우
    * INDEX 컬럼이 비교되기 전에 변형이 일어난 경우
    * 부정(NOT, <>)으로 조건을 기술한 경우
    * INDEX 컬럼이 NULL로 비교할 경우
    * OPTIMIZER 취사선택

```SQL
-- 부정으로 조건을 기술한 경우 INDEX 타게 하는 방법
SELECT 
    ID, NAME, TITLE
FROM 
    S_EMP
WHERE 
    TITLE <> '사원';    -- INDEX 사용안됨

SELECT 
    ID, NAME, TITLE 
FROM 
    S_EMP E
WHERE
    NOT EXISTS (
                SELECT 
                    'X'
                FROM 
                    S_EMP
                WHERE 
                    E.TITLE = '사원'
               );       -- INDEX 사용됨
```

**INDEX 생성, 비생성**

1. 인덱스 생성 권장 X
    * 테이블이 자주 변경될 때
    * 컬럼이 조회의 조건으로 사용되는 경우가 별로 없을 때
    * 테이블이 작거나, 조회가 행의 10% 정도 이상을 검색할 때
2. 인덱스 생성 권장 O
    * 컬럼에 NULL값이 많이 포함되있을 때
    * 1개 이상의 컬럼이 함께 WHERE, JOIN조건으로 자주 사용될 때
    * 테이블이 크고, 테이블에서 조회되는 행의 수가 전체의 10%정도 일 때

**VIEW**

* 간단한 뷰에서는 DML 연산 수행가능
* 테이블이나 다른 뷰를 기초로 한 가상의 테이블
* 선택적인 내용을 보여줌으로써 데이터베이스에 대한 액세스를 제한함.(보안적인 강점)
* 한 개의 뷰로 여러 테이블에 대한 데이터 검색 가능
* UNION, JOIN, GROUP BY 를 사용한 쿼리는 DML 사용 불가함.

```SQL
-- VIEW 생성
CREATE OR REPLACE VIEW MY_VIEW AS
(
SELECT 
    *
FROM 
    S_EMP
);
-- VIEW 조회
SELECT * FROM MY_VIEW;
SELECT * FROM USER_VIEWS;

-- VIEW 삭제
DROP VIEW MY_VIEW;
```

**SYNONYM**

* ALIAS 같이 이름을 줄여주는 역할이며 테이블의 이름을 설정해주는 것
* 특정 OBJECT에 부여하는 또 다른 이름이며 사용자의 편의나 참조를 빠르게 하기 위해 사용함.
* 

```SQL
CREATE [OR REPLACE] [PUBLIC]
SYNONYM '[스키마명].시노님명'
    FOR '스키마명.대상오브젝트명'

-- 시노님 생성
CREATE SYNONYM MY_EMP FOR S_EMP;

-- 시노님 조회
SELECT * FROM MY_EMP;

-- 시노님 삭제
DROP SYNONYM MY_EMP;
```

**NVL**

* NULL 값을 포함하는 컬럼을 지정된 값으로 변경하는데 사용함.
* NVL(형식1, 형식2) - 형식 1 : NULL값 포함 컬럼, 형식 2 : 변경하려는 값
* NVL2(형식1, 형식2, 형식 3) - NULL이면 형식3, 아니면 형식2를 출력함.

```SQL
SELECT ID, NAME, NVL(REGION_ID, 10) FROM S_DEPT;
SELECT ID, NAME, NVL2(REGION_ID, 20, 30) FROM S_DEPT;
```

**DECODE**

* 값을 비교하여 해당하는 값을 돌려주는 함수
* CASE WHEN THEN 을 사용하지만 오라클에서는 DECODE를 자주 사용함.
* DECODE(형식, 비교값1, 결과치1, 기본치)

```SQL
SELECT 
    SALARY,
    DECODE(SALARY/1000, 0, 'E', 'A')    -- 0이면 'E', 아니면 'A'
FROM 
    S_EMP;
```

**TRIGGER**

* 임의의 테이블에 DML이 수행 됐을 때, 데이터베이스에서 **자동적으로 동작하도록 작성된 프로그램**임.
* 테이블과 별도로 데이터베이스에 저장됨.

```SQL
CREATE [ OR REPLACE ] TRIGGER 트리거명
BEFORE | AFTER
[ 동작(INSERT, UPDATE, DELETE) ] ON 테이블명 
[ REFERENCING  NEW | OLD  TABLE AS 테이블명 ]
[ FOR EACH ROW ]
[ WHEN 조건식 ]
트리거 BODY문

CREATE OR REPLACE TRIGGER oracle_trigger
   BEFORE
   INSERT ON oracleStudy
   REFERENCING NEW TABLE AS new_trigger
   FOR EACH ROW
   WHEN new_trigger.점수 = ''
   BEGIN
     SET new_table.점수 = '0';
   END;
```

## ORACLE 실습

```SQL

-- CRETATE TABLE
create table TEST2 as 
(
select 
    * 
from    
    s_emp
);

CREATE TABLE TEST3
(
  ID VARCHAR2(2)  
);

-- 컬럼 추가
ALTER TABLE TEST3 ADD NAME VARCHAR(6);

-- PK 추가
ALTER TABLE TEST3 ADD PRIMARY KEY (ID);

-- PK 확인
SELECT 
    A.TABLE_NAME, A.CONSTRAINT_NAME, B.COLUMN_NAME
FROM 
    USER_CONSTRAINTS A,
    ALL_CONS_COLUMNS B
WHERE 
    1=1
    AND A.CONSTRAINT_NAME = B.CONSTRAINT_NAME
    AND A.CONSTRAINT_TYPE = 'P'
    AND A.TABLE_NAME = 'TEST3'
    AND A.OWNER = B.OWNER;

-- INSERT    
INSERT INTO TEST3
(
    ID,
    NAME,
    GENDER,
    DESCRIBE
)
VALUES 
(
    1, 
    'SON',
    'M',
    'INSERT TEST'
);

-- TABLE DATA TYPE 확인
SELECT 
    DATA_TYPE
FROM 
    COLS
WHERE 
    TABLE_NAME = 'TEST3'
    AND COLUMN_NAME = 'ID';

-- CREATE, DELETE, INSERT 변형
CREATE TABLE TEST4 AS 
SELECT * FROM S_DEPT;

DELETE FROM TEST4;

INSERT INTO TEST4 
(
    SELECT 
        *
    FROM 
        S_DEPT
);

-- UPDATE
INSERT INTO TEST4 
(
    ID, 
    NAME,
    REGION_ID
)
VALUES 
(
    12,
    'IT개발부',
    6
);

UPDATE TEST4 
    SET 
        ID = '119'
WHERE 
    NAME = 'IT개발부';

-- DISTINCT 
SELECT 
    DISTINCT NAME
FROM 
    TEST4;

-- GROUP BY 위와 결과 동일함
SELECT 
    NAME 
FROM 
    TEST4
GROUP BY 
    NAME;

-- ALIAS 두 단어로 구성되었으면 이중 따옴표 사용 
SELECT 
    NAME,
    "직장인 연봉"
FROM 
(
SELECT 
    NAME, SALARY * 12 "직장인 연봉"
FROM 
    S_EMP
);

-- GROUP BY 
-- 각 부서별 평균 급여 2000이상 부서만
SELECT
    TITLE,
    AVG(SALARY)
FROM 
    S_EMP
GROUP BY 
    TITLE
HAVING 
    AVG(SALARY) >= 2000;

-- 각 직책별 급여 총합 구하기(직책 부장인 사람 제외), 급여 총합이 3000이상인 직책만, 급여 총합에 대한 오름차순 정렬
SELECT 
    TITLE,
    MAX(SALARY) M
FROM 
    S_EMP
WHERE 
    TITLE != '부장'
GROUP BY 
    TITLE
HAVING 
    MAX(SALARY) >= 3000
ORDER BY 
    MAX(SALARY) ASC;

-- 각 부서별 직책 사원 직원들 평균급여
SELECT 
    TITLE,
    AVG(SALARY)
FROM 
    S_EMP
WHERE   
    TITLE = '사원'
GROUP BY 
    TITLE;

-- 각 부서내 각 직책별 몇 명의 인원이 있는지?
SELECT 
    TITLE,
    DEPT_ID,
    COUNT(*)
FROM 
    S_EMP
WHERE 
    TITLE IS NOT NULL
GROUP BY 
    TITLE,DEPT_ID;

-- 각 부서내에서 몇 명의 직원이 근무하는지?
SELECT 
    DEPT_ID,
    COUNT(ID) 
FROM 
    S_EMP
GROUP BY 
    DEPT_ID;

-- 각 부서별 급여의 최소값과 최대값 (같으면 출력 X)
SELECT 
    DEPT_ID,
    MIN(SALARY),
    MAX(SALARY)
FROM 
    S_EMP
GROUP BY 
    DEPT_ID
HAVING 
    MIN(SALARY) != MAX(SALARY);

-- EQUI JOIN 
SELECT 
    E.NAME, D.NAME
FROM 
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID = D.ID;
    
-- ANSI INNER JOIN
SELECT 
    E.NAME, D.NAME
FROM 
    S_EMP E INNER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;

-- 직원 테이블과 부서 테이블을 JOIN하여 사원의 이름, 부서, 부서명
SELECT 
    E.NAME, E.DEPT_ID, D.NAME
FROM 
    S_EMP E, S_DEPT D
WHERE
    1=1
    AND E.DEPT_ID = D.ID;   

-- 가장 적은 평균급여를 받는 직책에 대해 그 직책과 평균급여(서브쿼리)
SELECT 
    TITLE, 
    AVG(SALARY)
FROM 
    S_EMP
HAVING
    AVG(SALARY) = (
                    SELECT 
                        MIN(AVG(SALARY))
                    FROM 
                        S_EMP
                    GROUP BY 
                        TITLE  
                  )
GROUP BY 
    TITLE; 


-- PIVOT
SELECT 
    *
FROM 
    (
        SELECT 
            ID, 
            TO_CHAR(START_DATE, 'MM') || '월' YYM
        FROM 
            S_EMP
    )
PIVOT
    (
        COUNT(*)
        FOR YYM IN ('01월', '02월', '03월')
    );

-- DECODE
SELECT 
    ID,
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '01', 1, 0)) "1월",
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '02', 1, 0)) "2월",
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '03', 1, 0)) "3월"
FROM 
    S_EMP
GROUP BY 
    ID;

-- ROLLUP 그룹별 합계
SELECT 
    DEPT_ID, TITLE, COUNT(*)
FROM 
    S_EMP
GROUP BY 
    ROLLUP(DEPT_ID, TITLE);
    
-- CUBE 그룹별 합계 및 소계
SELECT 
    DEPT_ID, TITLE, COUNT(*)
FROM 
    S_EMP
GROUP BY 
    CUBE(DEPT_ID, TITLE)
ORDER BY 
    DEPT_ID;

-- RANK 행별 순위 계산
SELECT 
    ID, 
    NAME, 
    DEPT_ID, 
    SALARY , 
    RANK() OVER(PARTITION BY DEPT_ID ORDER BY SALARY) RANK
FROM 
    S_EMP;

-- 자신의 급여가 자신이 속한 부서의 평균 급여보다 적은 직원의 이름, 급여, 부서번호
SELECT 
    NAME, DEPT_ID, SALARY
FROM 
    S_EMP E1
WHERE 
    SALARY < 
            (
            SELECT 
                AVG(SALARY)
            FROM 
                S_EMP E2
            WHERE 
                E1.DEPT_ID = E2.DEPT_ID
            GROUP BY 
                DEPT_ID
            )
;

-- 본인의 급여가 각 부서별 평균 급여 중 어느 한 부서의 평균 급여보다 적은 급여를 받는 직원에 대해 이름, 급여, 부서번호를 출력하시오
SELECT 
    NAME, SALARY, DEPT_ID
FROM 
    S_EMP E1
WHERE
    SALARY < ANY(
                SELECT 
                    AVG(SALARY)
                FROM 
                    S_EMP E2
                GROUP BY 
                    DEPT_ID
                );

-- 본인이 다른 사람의 관리자로 되어 있는 직원의 사번, 이름, 직책, 부서번호
SELECT 
    ID, NAME, TITLE, DEPT_ID
FROM 
    S_EMP E1
WHERE 
    EXISTS (
            SELECT 
                ID
            FROM 
                S_EMP E2
            WHERE 
                E1.ID = E2.MANAGER_ID
            );
```

</div>
</details>