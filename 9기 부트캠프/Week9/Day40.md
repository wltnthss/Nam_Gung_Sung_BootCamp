# Day40 요약

## 강사님 카드게임 코드 분석

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      img {
        width: 60px;
        height: 100px;
      }
    </style>
  </head>
  <body>
    <button id="showBtn" onclick="show()">보이기</button>
    <button id="hideBtn" onclick="hide()">숨기기</button>
    <button id="shuffleBtn" onclick="shuffle()">섞기</button>
    <div id="board"></div>
    <script>
      const FILE_PATH = "cardImg";
      const EXTENSION = ".png";
      const BACK_IMG_SRC = FILE_PATH + "/" + "back" + EXTENSION;

      var cardArr = []; // 모든 카드의 이름을 담을 배열
      var firstCard = null; // 첫 번째로 클릭한 카드

      window.onload = function () {
        // 1. board를 초기화
        initBoard();
        // 2. imgTag에 이벤트 등록
        addEventToImgTag();
      };

      // 게임판(board)를 초기화
      function initBoard() {
        // 배열 cardArr을 초기화
        initCardArr();

        // <img>를 생성해서 <div id=board>에 추가
        var board = document.getElementById("board");
        board.innerHTML = createImgTag();
      }

      // <img>에 이벤트 등록
      function addEventToImgTag() {
        var imgTagArr = document.getElementsByTagName("img");

        for (i = 0; i < imgTagArr.length; i++) imgTagArr[i].onclick = imgClick;
      }

      // imgTag.src가 뒷면인지 확인.
      function isBack(imgTag) {
        return imgTag.src.indexOf("back") != -1;
      }

      // 카드를 뒤집는 함수. imgTag.src가 뒷면이면 앞면, 앞면이면 뒷면으로
      function flip(imgTag) {
        var card = cardArr[indexOf(imgTag)];
        imgTag.src = isBack(imgTag) ? getImagePath(card) : BACK_IMG_SRC;
      }

      // 배열 cardArr에서 imgTag의index를 찾아서 반환하는 함수
      function indexOf(imgTag) {
        var imgTagArr = document.getElementsByTagName("img");
        for (i = 0; i < imgTagArr.length; i++)
          if (imgTagArr[i] == imgTag) return i;

        return -1;
      }

      // <img>를 클릭했을 때 호출되는 handler
      function imgClick(e) {
        var clickedCard = e.srcElement; // e.srcElement는 <img>

        // 이미 열린 카드를 클릭하면 alert();
        if (!isBack(clickedCard)) {
          alert("이미 뒤집어진 카드입니다.");
          return;
        }

        // 카드를 뒤집는다.
        flip(clickedCard);

        // 두번째 카드인 경우
        if (firstCard) {
          // 첫번째 카드와 두번째 카드를 비교한다.
          (function (card) {
            setTimeout(compareAndFlip, 1000, card);
          })(clickedCard);
        } else {
          // 첫번째 카드인 경우
          // 클릭한 카드를 첫번째 카드로 저장한다.
          firstCard = clickedCard;
        }
      }

      // 두 카드를 비교해서 다르면, 다시 뒤집는다.
      function compareAndFlip(clickedCard) {
        // 첫번째 카드와 두번째 카드를 비교한다.
        if (equals(firstCard, clickedCard)) {
          // 두카드가 같은 경우
        } else {
          // 두 카드가 다른 경우. 다시 뒤집는다.
          flip(clickedCard);
          flip(firstCard);
        }

        // firstCard를 초기화
        firstCard = null;
      }

      // 두 카드가 같은지 비교. 본인의 상황에 맞게 로직 구현
      // 숫자가 같고 무늬가 같은 색이면 true를 반환하게 구현하시오.
      function equals(firstCard, secondCard) {
        // console.log(indexOf(firstCard));
        // console.log(indexOf(secondCard));
        // return indexOf(firstCard)%26==indexOf(secondCard);
        return Math.round(Math.random()); // 임시 구현
      }

      // cardArr초기화
      function initCardArr() {
        // for(i=1;i<=4;i++)
        // for(j=1;j<=13;j++)
        // cardArr.push(i+"_"+j);
        for (i = 0; i < 52; i++) cardArr.push(i);
      }

      // 52개의 <img>를 생성해서 문자열로 반환하는 함수
      function createImgTag() {
        var tmp = "";

        for (i = 0; i < cardArr.length; i++)
          tmp += "<img src='" + getImagePath(cardArr[i]) + "'>";

        return tmp;
      }

      // cardArr의 요소를 넣으면, <img>의 src형식에 맞게 생성해서 반환
      function getImagePath(card) {
        return FILE_PATH + "/" + card + EXTENSION;
      }

      // showBtn클릭시, 모든 카드를 뒷면으로 변경
      function show() {
        setImgSrc("BACK");
      }

      // hideBtn클릭시, 모든 카드를 앞면으로 변경
      function hide() {
        setImgSrc("FRONT");
      }

      // side의 값이 FRONT면 앞면, BACK이면 뒷면을 보여주는 함수
      function setImgSrc(side) {
        var imgTagArr = document.getElementsByTagName("img");

        for (i = 0; i < imgTagArr.length; i++)
          imgTagArr[i].src =
            side != "BACK" ? getImagePath(cardArr[i]) : BACK_IMG_SRC;
      }

      // shuffleBtn클릭시의 handler
      function shuffle() {
        // 배열 cardArr를 석는다.
        cardArr.sort((a, b) => Math.random() - 0.5);
        show(); // cardArr을 화면에 보여준다.
      }
    </script>
  </body>
</html>
```
