# Day10 요약 및 헷갈리는 개념

* 배열 섞는게 아직까지 조금 헷갈림.. 주말사이 배열관련 10문제 찾아서 풀어보고 정리하기

## 포커 문제 (코드 리팩토링 체크)

```java
package Tdd;

import static org.junit.Assert.*;

import java.util.HashSet;
import java.util.Set;

import org.junit.Test;

class Card {
   int num;
   String kind;

   public Card() {

   }

   public Card(int num, String kind) {
      this.num = num;
      this.kind = kind;
   }

   @Override
   public String toString() {
      
      String num = "";
      String kind = "";
      
      // 10 - A 11 - J 12 - Q 13 - K
      switch(this.num) {
         case 10:
            num = "A";
            break;
         case 11:
            num = "J";
            break;
         case 12:
            num = "Q";
            break;
         case 13:
            num = "K";
            break;
         default:
            num = this.num + "";
      }
      
      switch(this.kind) {
      case "SPADE":
         kind = "♠";
         break;
      case "DIAMOND":
         kind = "◆";
         break;
      case "CLOVER":
         kind = "♣";
         break;
      case "HEART":
         kind = "♥";
         break;
      default:
   }
      return num + " " + kind;
   }
}

public class MethodTest3 {

   /*
    * 5장의 카드를 받아서 평가하는 String rankCheck(Card[] cards)를 작성하시오.
    * 
    * Card[] cards = { new Card(0, "SPADE"), 
    *                new Card(1, "DIAMOND"), 
    *                new Card(2, "CLOVER"), 
    *                new Card(3, "HEART"), ... };
    * 
    * String rank = rankCheck(cards); 
    * print(rank);
    * 
    * ex) 
    * 1. " NO PAIR " 
    * 2. " 1 PAIR " -> A A 2 3 4 
    * 3. " 2 PAIR " -> A A 2 2 3 
    * 4. " THREE CARD " -> A A A 2 1 
    * 5. " FULL HOUSE " -> A A A 2 2 ( 1THREE CARD,1PAIR ) 
    * 6. " FOUR CARD " -> A A A A 10 
    * 7. " STRAIGHT " -> 4 5 6 7 8 ( 5 숫자 연속) 
    * 8. " FLUSH " -> ◆ ◆ ◆ ◆ ◆ ( 모두 같은 무늬 ) 
    * 9. " STRAIGHT && FLUSH
    */

   private static String rankCheck(Card[] cards) {

      Card card;                            // 카드 배열 담을 객체
      String rslt = "";                     // 메세지 비교
      int count = 0;                        // 각 배열 요소 중복값 체크
      int countST = 0;						// STRAIGHT 개수 체크 4이면 STRAIGHT
      boolean isFlush = false;				// FLUSH 유무
      
	  /*
	  * 5개의 카드 값 검증 given
	  */
      System.out.println("========= 카드 패 목록 =========");
	  for (int i = 0; i < cards.length; i++) {
	     card = cards[i];
	     System.out.println(card);
	  }
      
	  /*
	   * NO PAIR ~ STRAIGHT && FLUSH 계산
	   */
	  
	  // NO PAIR ~ FOUR CARD
	  for (int i = 0; i < cards.length -1; i++) {
	     for (int j = i+1; j < cards.length; j++) {
	        // 각 배열의 요소 중복값 비교
	        if(cards[i].num == cards[j].num) {
	           count++;
	        }
	     }
	  }
      
      // STRAIGHT
      for (int i = 1; i < cards.length; i++) {
         if((cards[i-1].num + 1) == (cards[i].num)) {
        	 countST++;
         }else {
         }
      }
      
      // FLUSH
      Set<String> set = new HashSet<String>();
      
      for (int i = 0; i < cards.length; i++) {
    	  set.add(cards[i].kind);
 	  }
      if(set.size() == 1) {
    	  isFlush = true;
      }
      
      /*
       * then
       */
      if(count == 0) {
         rslt = "NO PAIR";
      }else if(count == 1) {
         rslt = "1 PAIR";
      }else if(count == 2) {
         rslt = "2 PAIR";
      }else if(count == 3) {
         rslt = "THREE CARD";
      }else if(count == 4) {
         rslt = "FULL HOUSE";
      }else if(count == 6) {
         rslt = "FOUR CARD";
      }
      // STRAIGHT
      if(countST == 4 && count == 0) {
    	  rslt = "STRAIGHT";
      }
      if(isFlush) {
    	  rslt = "FLUSH";
      }
      if(countST == 4 && isFlush) {
    	  rslt = "STRAIGHT && FLUSH";
      }
         
      /*
       * 데이터 체크
       */
      System.out.println("========= 데이터 체크 =========");
      System.out.println("countST가 4면 STRAIGHT : " + countST);
      System.out.println("count 개수 : " + count);
      System.out.println("rslt : " + rslt);
      
      return rslt;
   }
   
   @Test
   public void test1() {
      Card[] cards = { new Card(9, "SPADE"),
                       new Card(10, "SPADE"),
                       new Card(11, "SPADE"),
                       new Card(12, "HEART"),
                       new Card(13, "SPADE")
                     };
      // NO PAIR, 1 PAIR, 2 PAIR, THREE CARD, FULL HOUSE, FOUR CARD
      // STRAIGHT, FLUSH, STRAIGHT && FLUSH
      assertTrue(rankCheck(cards) == "STRAIGHT"); 
      System.out.println();
   }
}
```
```
========= 카드 패 목록 =========
9 ♠
A ♠
J ♠
Q ♥
K ♠
========= 데이터 체크 =========
countST가 4면 STRAIGHT : 4
count 개수 : 0
rslt : STRAIGHT
```