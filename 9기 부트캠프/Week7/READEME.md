# 7째 주

## js 과제

```html

// Q1 입력시 li요소 클릭시 삭제 기능

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input type="text" id="textId">
    <input type="button" value="입력" onclick="btnClick()">

    <ul id="navi">

    </ul>

    <script>
        function btnClick(){
            //1. input 태그창 값 가져오기
            let values = document.getElementById('textId').value;
            console.log(values);

            //2. li Element 생성후 값 넣어주기
            let li = document.createElement('li');
            let text = document.createTextNode(values)
            li.append(text)

            // 3. ul 태그안에 li 넣기
            let ul = document.getElementById('navi')
            ul.append(li)

            // 4. li 태그 클릭시 삭제 
            li.onclick = function(){
                li.remove();
            }
        }
    </script>
</body>
</html>

// Q2 선택하는 라디오버튼 textarea 영역에 추가

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    #nav {
        float: left;
        margin-right: 20px;
    }

</style>
<body>
    
    <div id="nav">
        <input type="checkbox" id="sportsAll" value="전체" onclick="checkedAll()">전체<br>
        <input type="checkbox" name="sports" value="야구" onclick="check()">야구<br>
        <input type="checkbox" name="sports" value="농구" onclick="check()">농구<br>
        <input type="checkbox" name="sports" value="배구" onclick="check()">배구<br>
        <input type="checkbox" name="sports" value="축구" onclick="check()">축구
    </div>

    <div id="section">
        <textarea name="" id="text" cols="30" rows="10">
    
        </textarea>
    </div>

    <script>
        // 체크박스 전체
        function checkedAll() {
            // 1. checkbox 버튼 클릭 시 값 가져오기
            // 전체값
            let allSelect = document.getElementById('sportsAll')
            // 전체 제외 4개 값
            let selected = document.getElementsByName('sports')
            // 전체값 체크 boolean 여부
            let allSelectChecked = allSelect.checked
            // check된 값 배열
            let checkedAll = [];

            // 1.1 체크박스 전체 선택할 시 true이면 배열에 push 후 textarea 에 넣기
            // 1.2 false이면 checked false 처리.
            if(allSelectChecked){
                for(let select of selected){
                    select.checked = true;
                    checkedAll.push(select.value)
                }
                document.getElementById('text').innerHTML = checkedAll;
            }else{
                for(let select of selected){
                    select.checked = false;
                    checkedAll.pop(select.value)
                }
                document.getElementById('text').innerHTML = ''
            }
        }

        // 체크박스 개별요소 체크
        function check(){
            let selected = document.getElementsByName('sports')
            let checkedAll = []

            for(let i=0; i<selected.length; i++){
                if(selected[i].checked){
                    console.log(selected[i])
                    checkedAll.push(selected[i].value)
                }
            }
            document.getElementById('text').innerHTML = checkedAll;
        }
    </script>
</body>
</html>
```