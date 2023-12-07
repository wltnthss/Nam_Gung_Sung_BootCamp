# HTML, CSS

## HTML, CSS 는 양이 많으니 중요한 것, 잘모르는 것 위주로 정리

**CSS 선택자**

```
* : 모든 태그
h1 : 모든 <h1> 태그
h1, p : 모든 <h1>과, <p> 태그
div p : <div> 태그의 모든 자손 <p> 태그
div > p : <div> 태그의 직계 자손
div ~ p : <div> 태그의 모든 형제
div + p : <div> 의 옆형제
#main : <div id="main">
.even : <div class="even">
input[type=text] : 속성선택자
a:link
a:visited
a:hover
a:active
::selection - 드래그한 글자
:checked
:enabled
:disabled
:selected - 요소가 클 떄 처리위함 ( https://developer.mozilla.org/ko/docs/Web/CSS/overflow )
overflow - 레이아웃 깨지는 부분을 overflow 사용 (자주 사용되니 이것정도는 외우자)
ul>(li>a{menu$})*5
```

**CSS 속성**

* visibility - (visible, hidden)
* display - (none, block, inline, inline-block)
* position - (static, fixed, relative, absoulte)
    * 자식의 position 속성에 absolute 를 적용하면 부모의 position 속성에 relative 키워드를 적용함.
* border, outline - border는 영역이 있지만, outline은 영역이 없음. (border 밖에 생성됨 )
* float - (left, right)
    * 자식에 float 속성을 적용하면 부모의 overflow 속성에 hidden 키워드를 적용함.

**긴 글자 생략**

```css
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```