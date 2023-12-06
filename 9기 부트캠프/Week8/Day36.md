# Day36 요약

## 디버깅

## js 카드게임과제

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
    img {
        width:50px;
        height:70px;
        transition: transform 0.1s;
        perspective: 1100px;
        transition: 0.1s;
        transform-style: preserve-3d;
    }
    img:hover{
        transform: scale(1.3);
    }
</style>
</head>
<body>

<button onclick="showAll()">show All</button>
<button onclick="hideAll()">hide All</button>
<button onclick="shuffle()">shuffle</button><br>

<div id="board">
    <!-- 52장의 카드를 보여준다. -->
</div>

<script>

    // css 확인
    // document.addEventListener('DOMContentLoaded', () => {

    //     const cards = document.querySelectorAll('img');
    //     for(const card of cards){
    //         card.addEventListener("click", flipper)
    //     }

    //     function flipper(event){
    //         const target = event.currentTarget;
    //         target.style.transform = "rotateY(180deg)"

    //         setTimeout(() => {
    //             target.style.transform = "rotateY(180deg)"
    //         }, 1000);
    //     }
    // })

    window.onload = function() {
        // 시작과 동시에 셔플
        shuffle();
        // 1초 뒤 alert 창 이후 카드패 숨기기
        setTimeout(function() {
            alert('=== Game Start ===')
            hideAll();
        }, 1000);
    }

    const CARD_LENGTH = 52;

    // 이미지 담을 배열
    let board = [];
    // cards 주소
    let cards;
    // 클릭 한 카드 담을 배열
    var clickedCardArr = [];
    // 클락 한 카드 주소
    let clickedCards;
    // 맞추면 1점 추가
    let score;

    let tmp = ''

    for(let i=0; i<CARD_LENGTH; i++){
        tmp += `<img src = "img/${i}.png" alt="">`
    }
    let boardId = document.getElementById('board');
    boardId.innerHTML = tmp;

    // 모든 이미지 태그 선택
    cards = document.querySelectorAll('img');

    // ============================================== css 추가 미완
    for (let j=0; j<cards.length; j++){
        // board[j] 순서대로 img 태그 담기
        board[j] = cards[j].src;
        let isBack = cards[j]   
    }
    
    
    
    // 클릭 한 카드 클릭시 오픈 메서드
    for (let j=0; j<cards.length; j++){

        cards = document.querySelectorAll('img');

        cards[j].addEventListener('click', function(e) {

            cards[j].setAttribute('id', 'front')
            cards[j].setAttribute('name', 'opened')
            
            clickedCards = document.querySelectorAll('img[name="opened"]');

            setTimeout(function(){

                clickedCards = document.querySelectorAll('img[name="opened"]');

                cards[j].src = board[j]
                // 클릭 한 카드 숫자 비교를 img src 
                let idx = '';
               // img 태그의 숫자를 읽어서 카드 숫자 비교
                idx = cards[j].src
                // let cardNum = idx.substring(idx.lastIndexOf('/')+1, idx.lastIndexOf('.'))
                let cardNum = idx.substring(idx.lastIndexOf('/')+1, idx.lastIndexOf('.'))
                clickedCardArr.push(parseInt(cardNum%13))

                let selectedOne = clickedCardArr[0];
                let selectedTwo = clickedCardArr[1];

                if(clickedCardArr.length >= 2){
                    if(selectedOne === selectedTwo){
                        for(let i=0; i<clickedCards.length; i++){
                            clickedCards[i].setAttribute('name', 'corrected')
                        }
                        clickedCardArr = [];
                    }else{
                        // 카드가 불일치한 경우
                        setTimeout(() => {
                            for (let j=0; j<clickedCards.length; j++){
                                clickedCards[j].src = 'img/back.png'
                                cards[j].setAttribute('id', 'back')
                            }
                            clickedCardArr = [];
                        }, 1000);
                    }
                    // 선택한 카드 담는 배열 초기화
                    clickedCardArr = [];
                }
            }, 500);
        });
    }
    // /클릭 한 카드 클릭시 오픈 메서드 끝

    // 카드의 순서를 뒤섞는다.
    function shuffle() {
        // sort
        board.sort((a, b) => Math.random() -0.5);

        // sort한 배열 cards 에 넣기
        for(let i=0; i<cards.length; i++){
            cards[i].src = board[i];
        }
        // 초기화
        clickedCardArr = []
    }

    //모든 카드를 덮는다.(뒷면이 보이게 한다.)
    function hideAll() {

        cards = document.querySelectorAll('img');

        // 2. 선택한 모든 카드의 src 속성 img/back.png 로 변경
        for(let i=0; i<cards.length; i++){
            cards[i].setAttribute('id', 'back')
            cards[i].src = 'img/back.png'
        }
    }

    // 모든 카드를 보여준다.(앞면이 보이게 한다.)
    function showAll() {

        cards = document.querySelectorAll('img');

        for(let i=0; i<cards.length; i++){
            cards[i].setAttribute('id', 'front')
            cards[i].src =  board[i]
        }
    }

</script>
</body>
</html>
```