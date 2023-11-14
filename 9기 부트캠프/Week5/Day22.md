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

**싱글쓰레드 vs 멀티쓰레드**

* 싱글쓰레드 : 사용자가 입력 안하면 무한정 기다려야함 (blocking)
* 멀티쓰레드 : 입력을 기다리는 동안 다른 쓰레드가 다른 작업을 처리 가능함.
* 멀티쓰레드는 쓰레드간의 작업 전환(context switching)이 일어나므로 시간이 더 걸림.
* 병행 : 여러 개의 작업을 동시에 진행함
* 병렬 : 큰 작업을 여러개로 나눠서 처리함
    * 어떻게 나눠서 사용할 것인가?

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

**쓰레드 우선순위**

* 우선순위를 다르게함으로써 특정 쓰레드가 더 많은 작업시간을 가지기 위함.
* 기본 우선순위는 5, 쓰레드는 상대적이며 숫자가 높을 수록 우선순위가 높음.
* 범위는 1~10

**데몬 쓰레드**

* 일반 쓰레드의 작업을 돕는 보조적인 역할을 수행함.
* 일반 쓰레드 종료 시에 자동적으로 종료됨.
* GC, 화면자동갱신 등에 사용됨.
* 무한루프와 조건문을 이용하여 특정조건 만족시 수행
* GC는 갈비지 컬렉터 - JVM에서 메모리를 주기적으로 검사하며 사용하지 않는 객체가 있으면 객체를 자동으로 제거해주는 역할을 하는 청소부.

```java
void setDaemon(boolean on) // true 하고 start() 하면됨.

public void run(){
    while(true){
        try{
            Thread.sleep(3 * 1000);
        } catch(Exception e){

        }

        if(autoSave){
            autoSave();
        }
    }
}
```

**쓰레드 실행제어**

```java
static void sleep(long millies)     // 잠자기
static void yield()                 // 양보하기
void join()                         // 기다리기
void interrupt()                    // 깨우기
```

* suspend(), resume(), stop() 은 교착상태를 만들어 deprecated 되었음.
* sleep() 과 yield() 는 잠자기와 양보의 기능을 하는데 이는 static 메서드이므로 자신에게 동작함.



