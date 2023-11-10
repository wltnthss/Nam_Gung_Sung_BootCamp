# Day20 요약 및 헷갈리는 개념

## LinkdList

```java
class Node{
    Node next;      // 다음 노드 주소
    Node previous   // 이전 노드 주소
    Object obj;     // 데이터
}
```

* 불연속적 데이터 연결
* 이중 연결리스트로 구성되어있음.

## Stack & Queue

* Stack - LIFO (LastInFirstOut)
    * push() 추가, pop() 삭제
* Queue - FIFO (FirstInFirstOut)
    * offer() 추가, poll() 삭제

## Iterator

* 배열에 있는 정보를 추상화 -> 몇 개인지 알면 같이 코드가 수정되어야하나 추상화시킴으로써 값이 존재하면 값을 줌.
* Collection 클래스의 인터페이스 (List, Set) 

```java
public interface Collection{
    public Iterator iterator();
    ...
}
```

## Arrays

* copyOf(), fill(), setAll(), sort(), binarySearch(), equals(), toString(), asList(Object...a)
* 탐색 - 순차 탐색, 이진 탐색
    * asList(Object...a) - 얕은 복사이므로 반환한 크기 변경, 추가, 삭제 불가능함.
    * binarySearch() - 정렬 후 탐색(이진 탐색)
    * 이진 탐색 - 정렬된 값에 가운데 값을 구해가면서 탐색함.

## Comparator 과 Comparable

* Comparable - 기본 정렬기준을 구현하는데 사용 (자기 자신과 객체 비교)
* Comparator - 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용 (o1, o2 두 객체를 비교)
* sort
    * 1. 정렬 대상
    * 2. 정렬 기준 (비교 기준)
    * 3. Set은 순서가 없어서 사용할 수 없음

## HashSet

* 순서 X, 중복 X
* Set 인터페이스 구현한 대표적인 컬렉션
* boolean add 는 중복을 허용하지 않으므로 저장할 객체의 equals()와 hashCode()를 호출함.
    * 저장하는데 성능이 좋지 않음 (일일이 equals(), hashCode() 를 호출해야하므로)

## TreeSet

```java
class TreeNode{
    TreeNode left;      // 왼쪽 자식노드
    TreeNode right;     // 오른쪽 자식노드
    Object element;     // 데이터
}
```

* LinkedList 는 하나씩 TreeSet은 두 개씩
* 작은 쪽을 왼쪽 큰 쪽을 오른쪽에 트리 구조로 데이터를 넣음.
* 범위 검색에 유리할 때 사용. 
    * ex) TresSet에 담긴 50~80의 데이터
* 트리 순회(전위, 중위, 후위) - 트리의 모든 노드를 한번씩 읽는 것.
* 중위 순회하면 오름차순으로 정렬됨.

## HashMap

* 순서 X, 중목 O (키 X, 값 O)
* LinktedHashMap 은 순서 O -> 순서를 유지할 때 사용함.
* 대용량 데이터 검색에 유리함.
* 해싱 기법으로 데이터를 저장함. Map 인터페이스를 구현하여 데이터를 키와 쌍으로 저장함.
* 똑같은 키가 두번 들어가면 마지막 값을 엎어침.
* 있는 데이터를 찾기는 쉬우나, 없는 데이터 (즉, 어떤 범위의 어떤 데이터가 없는지 찾기 어려운 단점)

```java
Entry[] table;

// 키와 값을 한 쌍으로 묶은 것이 Entry 임.
```

* 해싱 : 해시함수로 해시테이블에 데이터를 저장, 검색함.
    * 1. key를 대입
    * 2. 해시함수를 통해 hashCode()로 반환
    * 3. 해시코드를 반환함

## TreeMap

* 대용량은 HashMap, 범위, 소용량 검색은 TreeMap을 사용하자.
* 범위검색, 정렬에 장점을 가짐.

* Tree 알고리즘은 유사함.

## Properties 

* 설정파일을 쌍으로 저장할 경우 사용 (file을 읽고 쓸 때 자주 사용함.)
* Map 과 똑같음 (Map은 Object, Object), (Properties는 String, String) 으로 이루어져있음 타입의 차이만 있음.

## Collections

* 가지고 있는 메서드는 Arrays 와 유사함.
* 동기화(synchronized), 변경불가(unmodifiable), 싱글톤(singleton), 한 종류 객체 (checked) 를 사용할 수 있음.