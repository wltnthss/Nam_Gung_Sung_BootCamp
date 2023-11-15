# Day23 요약 및 헷갈리는 개념

## 13장 쓰레드

**sleep()**

* 지정된 시간동안 쓰레드를 멈추게함.

```java
try{
    Thread.sleep(1000); // 1초
}

void delay(long millies) {
    try{
        Thread.sleep(millies);
    } catch (InterruptedException e){

    }
}
```

* 매번 예외처리는 번거롭기에 delay 함수와 같이 자주 사용함.

**interrupt() 와 interrupted()**

* 대기상태인 쓰레드를 실행대기 상태로 만듬.

```java
while(!interrupted()){
    // interrupted() 결과가 false이면 반복
}
```

**yield()**

* 쓰레드 자신에제 주어진 실행시간을 다음 차례의 쓰레드에게 양보함.
* return() 과 다르게 종료하지않고 멈춤

**join()**

* 지정된 시간동안 쓰레드가 작업하는 것을 기다림.
* main()을 실행하다가 join()을 만나면 작업이 끝날 때까지 기다림.
* interrupt()를 호출하고 필요하다면 join()도 같이 사용해주자.

## 쓰레드 동기화 - synchronized

* **한 쓰레드가 작업을 진행하는 동안 다른 쓰레드가 간섭하지 못하도록 막는 것**
* lock을 획득한 쓰레드가 공유 데이터를 사용하는 영역(임계 영역)을 수행하고나면 lock을 반납해야 다른 쓰레드가 lock을 다시 획득하고 임계 영역 수행함.
* 멀티쓰레드에서만 의미가 있음.

## 쓰레드 동기화 - wait(), notify(), notifyAll()

* wait() - 객체의 lock()을 풀고 쓰레드를 해당 객체의 waiting pool에 넣음
* notify() - 작업을 진행하고자할 때 호출해서 중단했던 쓰레드가 다시 락을 얻어 작업 진행
* notifyAll() - 기다리고 있는 모든 객체에게 통보

**Lock & Condition**

* wait(), notify() 는 lock을 하나만 얻을 수 있어 개선하고자 만듬.

## 14장 람다와 스트림

**람다식**

* 함수를 간단한 식으로 표현하는 방법

* Supplier<T> - 매개변수 X 반환값 O
* Consumer<T> - 매개변수 O 반환값 X
* Function<T, R> - 매개변수 O 반환값 O
* Predicate<T> - 매개변수 O 반환 타입 boolean