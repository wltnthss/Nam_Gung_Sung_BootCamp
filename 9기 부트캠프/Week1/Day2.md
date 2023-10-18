# Day2 요약 및 헷갈리는 개념

* 기본형 타입의 저장 값 범위
    * byte : -128 ~ 127 (2의 7승)
    * short : -32,768 ~ 32,767 (2의 15승)
    * int : 2,147,483,647 ~ (2의 31승, 약 20억)
    * long : -9,223 ~ (2의 63승)

* float와 double의 정밀도
    * float는 정밀도 7자리, double은 정밀도 15자리
    * 높은 정밀도의 실수형을 사용할 때는 double을 사용해야함.
    * 사용하지 않으면 값의 오차가 생길 수 있음.
    * 

```java
public class QuizTest {

	public static void main(String[] args) {
		
		System.out.printf("i | ex1  | ex2 \n");
		System.out.print("---------------");
		System.out.println();
		
		for (int i = 1, j = 3*i; i <= 9; i++, j++) {
			System.out.printf("%d  | %d  |  %d \n", i, (j%3)+1, (j/3));
		}		
	}
}
```
```
i | ex1  | ex2 
---------------
1  | 1  |  1 
2  | 2  |  1 
3  | 3  |  1 
4  | 1  |  2 
5  | 2  |  2 
6  | 3  |  2 
7  | 1  |  3 
8  | 2  |  3 
9  | 3  |  3 
```