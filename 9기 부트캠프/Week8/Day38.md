# Day38 요약 

## https://www.w3schools.com/howto/default.asp 참고해서 하루에 하나 html, css, js 가볍게 연습하기

## 웹사이트 구성

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    *{
        margin: 0; padding: 0;
        body{font-family: sans-serif;}
        li{list-style: none;}
        img{border: 0;}
    }
    /* Header */

    #mainHeader{
        margin: auto;
        width: 960px;

        height: 160px;
        position: relative;
    }
    #title{
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
    }
    #mainHeader > #title{
        position: absolute;
        left: 20px; top: 30px;
    }
    #mainHeader > #mainNav{
        position: absolute;
        right: 0;
        top: 0;
    }
    #mainHeader > #localNav{
        position: absolute;
        right: 0;
        bottom: 10px;
    }
    li{
        list-style: none;
    }
    /* 메뉴 1 */

    #mainNav > ul {
        overflow: hidden;
    }
    #mainNav > ul > li {
        float: left;
    }
    #mainNav > ul > li > a{
        display: block;
        padding: 2px 10px;
        border: 1px solid black;
    }
    #mainNav > ul > li > a:hover{
        background-color: black;
        color: white;
    }
    #mainNav > ul > li:first-child > a{
        border-radius: 10px 0 0 10px;
    }
    #mainNav > ul > li:last-child > a{
        border-radius: 0 10px 10px 0;
    }
    /* 메뉴 2 */

    #localNav > ul{
        overflow: hidden;
    } 
    #localNav > ul > li{
        float: left;
    }
    #localNav > ul > li > a{
        display: block;
        padding: 10px 20px;
        border: 1px solid black;
    }
    #localNav > ul > li > a:hover{
        background-color: black;
        color: white;
    }
    #localNav > ul > li:first-child > a{
        border-radius: 10px 0 0 10px;
    }
    #localNav > ul > li:last-child > a{
        border-radius: 0 10px 10px 0;
    }
    /* Content 영역 */

    #content{
        margin: auto;
        width: 960px;

        /* overflow: hidden; */
    }
    #content > #mainSection{
        width: 750px;
        float: left;
    }
    #content > #mainAside{
        width: 200px;
        float: right;
    }
    #mainSection > article.mainArticle{
        margin-bottom: 10px;
        padding: 10px;
        border: 1px solid black;
    }
    /* Aside 영역 */

    #mainAside > div:nth-child(4) > ul{
        padding: 0;
    }
    #mainAside > div:nth-child(5) > ul{
        padding: 0;
    }

    /* 첫번째 탭 */

    input:nth-of-type(1) {
        display: none;
    }
    input:nth-of-type(1) ~ div:nth-of-type(1){
        display: none;
    }
    input:nth-of-type(1):checked ~ div:nth-of-type(1) {
        display: block;
    }
    /* 두번째 탭 */

    input:nth-of-type(2) {
        display: none;
    }
    input:nth-of-type(2) ~ div:nth-of-type(2){
        display: none;
    }
    input:nth-of-type(2):checked ~ div:nth-of-type(2) {
        display: block;
    }
    /* 탭 모양 구성 */
    section.buttons {
        overflow: hidden;
    }
    section.buttons > label{
        /* 수평 정렬 */
        display: block;
        float: left;

        /* 크기 및 글자 위치 지정 */
        width: 100px; height: 30px;
        line-height: 30px;
        text-align: center;

        /* 테두리 */
        border: 1px solid black;
        box-sizing: border-box;

        /* 색상 지정 */
        background-color: black;
        color: white;

    }
    input:nth-of-type(1):checked ~ section.buttons > label:nth-of-type(1){
        background-color: white;
        color: black;
    }
    input:nth-of-type(2):checked ~ section.buttons > label:nth-of-type(2){
        background-color: white;
        color: black;
    }
    /* 목록 */
    .item{
        overflow: hidden;
        padding: 2px;
        border: 1px solid black;
    }
    .thumbnail{
        float: left;
    }
    .description{
        float: left;
        margin-left: 8px;
    }
    .description > strong {
        display: block;
        width: 120px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    #mainAside p{
        margin-bottom: 11px;
    }
    /* Footer */
    #mainFooter{
        margin: 0 auto;
        width: 960px;

        /* 테두리 */
        box-sizing: border-box;
        padding: 10px;
        text-align: center;
    }
</style>
<body>
    <header id="mainHeader">
        <div id="title">
            <h1>Web Page</h1>
            <h2>HTML + CSS</h2>
        </div>
        <nav id="mainNav">
            <ul>
                <li><a href="#">Web</a></li>
                <li><a href="#">Mobile</a></li>
                <li><a href="#">Game</a></li>
                <li><a href="#">Simulation</a></li>
                <li><a href="#">Data</a></li>
            </ul>
        </nav>
        <nav id="localNav">
            <ul>
                <li><a href="#">HTML5</a></li>
                <li><a href="#">CSS3</a></li>
                <li><a href="#">JavaScript</a></li>
                <li><a href="#">jQuery</a></li>
                <li><a href="#">Node.js</a></li>
            </ul>
        </nav>
    </header>

    <!-- Content 영역  -->

    <div id="content">
        <section id="mainSection">
            <article class="mainArticle">
                <h1>MainSection</h1>
                <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente maiores dolorem a alias harum at sequi, placeat eveniet, fugiat voluptates illo ullam adipisci consectetur totam corporis iste eum nisi delectus.</p>
            </article>
            <article class="mainArticle">
                <h1>MainSection</h1>
                <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente maiores dolorem a alias harum at sequi, placeat eveniet, fugiat voluptates illo ullam adipisci consectetur totam corporis iste eum nisi delectus.</p>
            </article>
            <article class="mainArticle">
                <h1>MainSection</h1>
                <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente maiores dolorem a alias harum at sequi, placeat eveniet, fugiat voluptates illo ullam adipisci consectetur totam corporis iste eum nisi delectus.</p>
            </article>
            <article class="mainArticle">
                <h1>MainSection</h1>
                <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente maiores dolorem a alias harum at sequi, placeat eveniet, fugiat voluptates illo ullam adipisci consectetur totam corporis iste eum nisi delectus.</p>
            </article>
            <article class="mainArticle">
                <h1>MainSection</h1>
                <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente maiores dolorem a alias harum at sequi, placeat eveniet, fugiat voluptates illo ullam adipisci consectetur totam corporis iste eum nisi delectus.</p>
            </article>
        </section>
        <aside id="mainAside">
            <input type="radio" name="tab" id="first" checked="checked">
            <input type="radio" name="tab" id="second">
            <section class="buttons">
                <label for="first">First</label>
                <label for="second">Second</label>
            </section>
            <div class="tabItem">
                <ul>
                    <li class="item">
                        <a href="#">
                            <div class="thumbnail">
                                <img src="cat.jpg" alt="" width="110px" height="80px">
                            </div>
                            <div class="description">
                                <strong>HTML5 Canvas</strong>
                                <p>2023-12-07</p>
                            </div>
                        </a>
                    </li>
                    <li class="item">
                        <a href="#">
                            <div class="thumbnail">
                                <img src="cat.jpg" alt="" width="110px" height="80px">
                            </div>
                            <div class="description">
                                <strong>HTML5 Audio</strong>
                                <p>2023-12-07</p>
                            </div>
                        </a>
                    </li>
                    <li class="item">
                        <a href="#">
                            <div class="thumbnail">
                                <img src="cat.jpg" alt="" width="110px" height="80px">
                            </div>
                            <div class="description">
                                <strong>HTML5 Video</strong>
                                <p>2023-12-07</p>
                            </div>
                        </a>
                    </li>
                    <li class="item">
                        <a href="#">
                            <div class="thumbnail">
                                <img src="cat.jpg" alt="" width="110px" height="80px">
                            </div>
                            <div class="description">
                                <strong>HTML5 Semantic Web</strong>
                                <p>2023-12-07</p>
                            </div>
                        </a>
                    </li>
                </ul>
            </div>
            <div class="tabItem">
                <ul>
                    <li><a href="#">CSS3 Transition</a></li>
                    <li><a href="#">CSS3 Animation</a></li>
                    <li><a href="#">CSS3 Border</a></li>
                    <li><a href="#">CSS3 Box</a></li>
                </ul>
            </div>
        </aside>
    </div>
    <footer id="mainFooter">
        <h3>HTML + CSS3 BASIC </h3>
        <address>Website Layout Basic</address>
    </footer>
</body>
</html>
```