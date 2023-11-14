# Day22 요약 및 헷갈리는 개념

## 13장 쓰레드

* 프로세스 : 실행중인 프로그램 (공장)
    * 데이터, 메모리, 자원, 쓰레드러 구성
    * 반드시 하나 이상의 쓰레드가 존재해야함
* 쓰레드 : 프로세스의 자원을 이용해서 작업을 수행하는 것 (일꾼)
* 멀티쓰레드 : 둘 이상의 쓰레드로 구성

**멀티쓰레드**

* 하나의 프로세스에서 여러 개의 쓰레드가 동시에 작업을 수행하는 것
* 동기화, 교착상태의 단점

1. CPU 사용률 향상
2. 자원 효율적 사용
3. 사용자 응답성 향상
4. 코드 간결성

**멀티프로세스 vs 멀티쓰레드**

* 멀티프로세스는 자원 낭비 (매모리 공간낭비가 많음)
* 멀티쓰레드는 동기화, 교착상태(deadlock) 문제가 발생함.

**쓰레드 구현과 생성**

1. Thread 상속 방법
    * 자바는 단일 상속이므로 Thread 상속시 다른 클래스는 상속받을 수 없는 단점

```java
class MyThread1 extends Thread{
    public void run() { ... }
}

MyThread1 t1 = new MyThread1();
t1.start();
```

2. Runnable 인터페이스 구현 방법
    * 재사용성이 높고, 일관성 유지됨.

```java
class MyThread2 implements Runnable {
    public void run() { ... }
}

Thread t2 = new Thread(new MyThread2);
t2.start();
```

**start(), run()**

* run()은 단순히 main메서드에서 메서드를 호출하는 것 뿐임.
* start() 를 호출해야 호출스택을 생성한 다음 run()을 호출함.
* main()이 종료되어도 다른 쓰레드가 작업을 마치지 않았으면 프로그램은 종료되지 않음. 