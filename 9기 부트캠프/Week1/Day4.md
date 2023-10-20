# Day4 요약 및 헷갈리는 개념

**배열활용**

* 최대값, 최소값, sum -> for문 1개
* 정렬 -> for문 2개


## 클래스

1. 설계도
2. 인스턴스 변수와 메서드를 모아놓은 것
3. 사용자정의타입

### 배열 문제 풀이 (헷갈렸던 문제만)

```java
// 피보나치 수열
package Practice;

public class Ex4_11 {

	public static void main(String[] args) {
		int num1 = 1;
		int num2 = 1;
		int num3 = 0;
		System.out.print(num1+","+num2);
		
		for (int i = 0; i < 8; i++) {
			/*
			 * i가 0일 때 num3 = num1+num2;  1+1 = 2
			 * i가 1일 때 num3 = num2+num3;  1+2 = 3
			 * i가 2일 때 num3 = num3+num1;  2+3 = 5
			 */
			num3 = num1 + num2;
			num1 = num2;
			num2 = num3;
			System.out.print(","+num3);
		}
	}
}

```
```
1,1,2,3,5,8,13,21,34,55
```

```java
package Practice;

public class Ex4_12 {
    
	/*
    구구단 일부분 다음과 같이 출력
	 * i=2 , j=1  \t  i=3, j=1  \t  i=4, j=1
	 * i=2 , j=2  \t  i=3, j=2  \t  i=4, j=2
	 * i=2 , j=3  \t  i=3, j=3  \t  i=4, j=3
	 * 띄어쓰기
	 * i=5 , j=1  \t  i=6, j=1  \t  i=7, j=1
	 * i=5 , j=2  \t  i=6, j=2  \t  i=7, j=2
	 * i=5 , j=3  \t  i=6, j=3  \t  i=7, j=3
	 * 띄어쓰기
	 * i=8 , j=1  \t  i=9, j=1
	 * i=8 , j=2  \t  i=9, j=2
	 * i=8 , j=3  \t  i=9, j=3
	 * 
	 */
	public static void main(String[] args) {
		for (int i = 1; i <= 9; i++) {
			for (int j = 1; j <= 3; j++) {
				int x = ((i-1) / 3) * 3 + j+1;
				int y = i % 3 == 0 ? 3 : i % 3;
				System.out.print(x+"*"+y+"="+x*y+"\t");
				if(x == 9) {
					break;
				}	
			}
			System.out.println();
			if(i % 3 ==0) {
				System.out.println();
			}
			
		}
	}
}

```
```
2*1=2	3*1=3	4*1=4	
2*2=4	3*2=6	4*2=8	
2*3=6	3*3=9	4*3=12	

5*1=5	6*1=6	7*1=7	
5*2=10	6*2=12	7*2=14	
5*3=15	6*3=18	7*3=21	

8*1=8	9*1=9	
8*2=16	9*2=18	
8*3=24	9*3=27	
```

```java
package Practice;

public class Ex5_8 {

    /*
    *   숫자 개수 세고, 개수만큼 '*' 찍기
    */
	public static void main(String[] args) {
		int[] answer = { 1,4,4,3,1,4,4,2,1,3,2 };
		int[] counter = new int[4];
		
		for (int i = 0; i < answer.length; i++) {
			counter[answer[i]-1]++;
		}
		
		for (int i = 0; i < counter.length; i++) {
			System.out.print(counter[i]);
			
			for (int j = 0; j < counter[i]; j++) {
				System.out.print("*");
			}
			
			System.out.println();
		}
	}
}

```
```
3***
2**
2**
4****
```

```java
package Practice;

public class Ex5_9 {
	public static void main(String[] args) {
        /*
        *   배열 시계방향 90도 회전하여 출력
        */
		char[][] star = {
						{'*','*',' ',' ',' '},
						{'*','*',' ',' ',' '},
						{'*','*','*','*','*'},
						{'*','*','*','*','*'}
						};
		
		char[][] result = new char[star[0].length][star.length]; 	//char[5][4];
		
		for (int i = 0; i < star.length; i++) {
			for (int j = 0; j < star[i].length; j++) {
				System.out.print(star[i][j]);
			}
			System.out.println();
		}
		System.out.println();

		for (int i = 0; i < star.length; i++) {				// 0 ~ 4
			for (int j = 0; j < star[i].length; j++) {		// 0 ~ 5
				result[j][star.length-i-1] = star[i][j];
			}
		}
		
		for (int i = 0; i < result.length; i++) {
			for (int j = 0; j < result[i].length; j++) {
//				System.out.printf("[%d,%d]", i, j);
				System.out.print(result[i][j]);
			}
			System.out.println();
		}
		System.out.println();
		
	}
}

```
```
**   
**   
*****
*****

****
****
**  
**  
**  
```

```java
package Practice;

public class Ex5_11 {

	public static void main(String[] args) {
		
		int [][] score = {
				{100, 100, 100}
			   ,{20, 20, 20}
			   ,{30, 30, 30}
			   ,{40, 40, 40}
			   ,{50, 50, 50}
		};
		
		int[][] result = new int[score.length+1][score[0].length+1];	//[6][4];
		int sum  = 0;
		
		for (int i = 0; i < score.length; i++) {	// 5
			for (int j = 0; j < score[i].length; j++) {		//3
				/*
				 * (0,3) (1,3), (2,3), (3,3), (4,3) 더한값 오른쪽
				 * (5,0) (5,1), (5,2) 더한값 아래쪽
				 * (5,3) -> 아래쪽끝 오른쪽끝 덧셈
				 */
				result[i][j] = score[i][j];
				result[i][score[0].length] += result[i][j];
				result[score.length][j] += result[i][j];
				result[score.length][score[0].length] += result[i][j];
				
			}
		}
		
		for (int i = 0; i < result.length; i++) {
			for (int j = 0; j < result[i].length; j++) {
				System.out.printf("%4d", result[i][j]);
			}
			System.out.println();
		}
	}
}
```
```
 100 100 100 300
  20  20  20  60
  30  30  30  90
  40  40  40 120
  50  50  50 150
 240 240 240 720
```