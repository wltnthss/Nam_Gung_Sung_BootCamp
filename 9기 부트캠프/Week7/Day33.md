# Day32 요약

## js

**배열**

```javascript
// 2차원 배열에 담기
arr2[i/5][i%5] =arr[i]
// 2차원 배열 -> 1차원 배열로 바꾸기
arr[i*5+j] = arr2[i][j]
```

**클로져**

* 외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조함 이러한 중첩 함수가 클로저.
* 상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하기 위해 사용함.

**프로토타입**

```js
obj.__proto__ === obj2.__proto__    // true
obj.__proto__ === Object.prototype  // true

// 생성자의 prototype에 함수 getName() 을 추가
Object.prototype.getName = function(){
    return this.name
}

obj.name = "aaa"
obj2.name = "bbb"

console.log(obj.getName())
console.log(obj2.getName())
```

**빙고판**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
            font-size: 20px;
            
        }


    </style>
</head>
<body>
    
    <div id="bingo">
        
    </div>

    <script>
        // 1. 1~25가 담긴 배열을 만든다.


            let arr = [];

            for(let i=0; i<25; i++){
                arr[i] = i+1;
            }

            console.log(arr)
            
        // 2. 배열을 섞는다.

            arr.sort((a,b) => Math.random() - 0.5)

            console.log('sort 배열 : ', arr)

        // 3. 배열을 2차원 배열에 담는다.

            let twoArr = [];

            const hang = 5;

            for(let y=0; y< hang; y++){
                twoArr[y] = arr.splice(0, 5)
            }

            console.log('twoArr : ' , twoArr)

        // 4. 2차원 배열을 <table>에 담는다.

            let result = `<table border="1px solid" >`
                for(i=0; i<5; i++){
                result += `<tr>`
                    for(j=0; j<5; j++){
                        result += `<td> ${twoArr[i][j]} </td>`
                    }
                result += `<tr>`    
                }
            
            document.getElementById('bingo').innerHTML = result

    </script>
</body>
</html>
```

## html

```html
<h1> ~ <h6>
<p>
<br>
<img>
<table>
<li>
<ul>
<ol>
<form>
<input>
<select>
<option>
<div>
<span>
```