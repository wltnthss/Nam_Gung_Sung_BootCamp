
# 2장 변수

* 변수 : 하나의 값을 저장할 수 있는 저장공간.
* 타입 : 깂을 담을 그릇의 종류.
* 타입 기본형 - 8개

1. 숫자 
* 논리 - boolean - true,false
* 정수 - byte, short, int, long - 1, 2, 4, 8
* 실수 - float, double - 4, 8
* 문자 - char

2. 문자
string - 0+개

> "모든 값은 타입이 있고, 타입을 모르면 해석은 불가합니다."

## 2장 핵심

(1) 변수선언
(2) 변수에 읽기, 쓰기
(3) 두 변수 값 교환
(4) 형변환 : A타입 - > B타입
(5) 자동형변환

# 3장 연산자

* 연산자 - 연산을 수행하는 기호

* 우선 순위 - 상식 + 괄호
* 결합 법칙 
    * L -> R, 단항&대입만 R -> L
* 산술변환
    * int, long 큰 것중 큰 타입으로 일치
    * int보다 작은 타입으로 변환

# 4장 조건문 & 반복문

* if(조건식) { 조건식이 참일때 실행 }
* while(조건식) { 조건식이 참인동안 반복 }
* for(int i=1; i<=n; i++) { 반복할 문장 }

```java
package ForTest;

public class Ex1 {

	public static void main(String[] args) {
		
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < 5; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```
```
*****
*****
*****
*****
*****
```

```java
package ForTest;

public class Ex2 {

	public static void main(String[] args) {
		
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < i; j++) {
				System.out.print(" ");
			}
			System.out.print("*");
			System.out.println();
		}
	}
}

```
```
*
 *
  *
   *
    *
```

```java
package ForTest;

public class Ex3 {

	public static void main(String[] args) {
		for (int i = 5; i > 0; i--) {
			for (int j = 0; j < i; j++) {
				System.out.print(" ");
			}
			System.out.print("*");
			System.out.println();
		}
	}
}

```
```
     *
    *
   *
  *
 *
```

```java
package ch4;

public class Ex4 {
	public static void main(String[] args) {

        for (int i = 0; i < 5; i++) {
        	for (int j = 0; j < 5; j++) {
        		if(i == j || 4-i == j) {
        			System.out.print("*");
            	}else {
            		System.out.print(" ");
            	}
			}
        	System.out.println();
		}
	}
}
```
```
*   *
 * *
  *  
 * * 
*   *
```

```java
package ForTest;

public class Ex5 {

	public static void main(String[] args) {
		
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j <= i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}

```
```
*
**
***
****
*****
```

```java
package ForTest;

public class Ex6 {

	public static void main(String[] args) {

		for (int i = 5; i >= 0; i--) {
			for (int j = 0; j < i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}

```
```
*****
****
***
**
*
```

```java
package ForTest;

public class Ex7 {

	public static void main(String[] args) {
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < i + 5; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}

```
```
*****
******
*******
********
*********
```

```java
package ForTest;

public class Ex8 {

	public static void main(String[] args) {
		
		for (int i = 0; i < 5; i++) {
			
			for (int j = 1; j < 5-i; j++) {
				System.out.print(" ");
			}
			
			for (int j = 0; j < (2 * i) + 1; j++) {
				System.out.print("*");
			}			
			System.out.println();
		}
	}
}

```
```
    *
   ***
  *****
 *******
*********
```

```java
package ForTest;

public class Ex9 {

	public static void main(String[] args) {
		for (int i = 2; i > 0; i--) {
			
			for (int j = 1; j < 3-i; j++) {
				System.out.print(" ");
			}
			for (int j = 0; j < 2*i + 1; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
		
		for (int i = 0; i < 3; i++) {
			for (int j = 1; j < 3-i; j++) {
				System.out.print(" ");
			}
			for (int j = 0; j < 2*i + 1; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}

```
```
*****
 ***
  *
 ***
*****
```
```java
public class Ex10 {

	public static void main(String[] args) {
		
		// 방법1
		for (int i = 1, n = 1; i <= 5; i++) {
			for (int j = 1; j <= 5; j++) {
				System.out.print(((n+1 <= j) && (j <= 5-n)) ? " " : "*");
			}
			System.out.println();
			if(i < 3) {
				n++;
			}else {
				n--;
			}
		}
		System.out.println();
		// 방법2
		for(int i = 0; i < 3; i++) {
			for(int j = 0; j <= i; j++) {
				System.out.printf("*");
			}
			for(int j = 0; j < 3*2 - 2*(i+1); j++) {
				System.out.printf(" ");
			}
			for(int j = 0; j <= i; j++) {
				System.out.printf("*");
			}
			System.out.println();
		}
				
		for(int i = 1; i < 3; i++) {
			for(int j = 0; j < (3-i); j++) {
				System.out.printf("*");
			}
			for(int j = 0; j < 2*i; j++ ) {
				System.out.printf(" ");
			}
			for(int j = 0; j < (3-i); j++) {
				System.out.printf("*");
			}
			System.out.println();
		}
	}
}
```
```
*   *
** **
*****
** **
*   *

*    *
**  **
******
**  **
*    *
```