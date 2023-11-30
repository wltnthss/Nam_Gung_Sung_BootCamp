# 자바스크립트

## 모던 자바스크립트 Deep Dive 책 참고

**데이터타입**

* numer, boolean, string, null, undefined, symbol, function, object 8개의 데이터 타입을 가짐.
* typeof 연산자로 변수나 리터럴 타입 확인 가능.

```javascript
let integer = 10;
let double = 10.12;
let negative = -20;

// 숫자 타입은 모두 실수 처리
console.log(1 == 1.0)   // true
console.log(1 === 1.0)  // true

parseInt("123px")   // 123
parseInt(true)  // NaN
Number(true)    // 1
Number("true")  // NaN
String(123 + "")    // '123'
Boolean("0")    // true
Boolean(0)  // false
Boolean(123)    // true
!!123   // true
```

* 자바스크립트는 모두 숫자 타입임.

**템플릿 리터럴**

```javascript
let first = 'ES';
let two = '5';
console.log('ES5표기 방법 - ' + first + ' ' + two)

let es6First = 'ES'
let es6Two = '6'
console.log(`ES6표기 방법 - ${es6First} ${es6Two}`)
```

**연산자**

```javascript
typeof -'10'    // number
typeof +true    // number
7 + '5'     // 75
7 - '5'     // 2
"abc" - 3   // NaN
1 + true    // 2
1 + false   // 1
1 + null    // 1
10 ** 3     // 1000
0.2 * 10    // 2
102.124.toFixed(1)  // 102.1 (소수점 반올림)
"2" > "12"     // true (String 끼리의 사전 순서)
2 > "12"        // false (숫자로 변환됨)
undefined == null   // true
NaN === NaN     // NaN은 자신과 일치하지 않는 유일한 값
2 % 2 ? '홀수' : '짝수' // 짝수  (0은 false로 변환됨) 
typeof NaN  // number
```

* null 타입 확인 시는 === 사용, typeof 의 결과는 object 이기 때문
* NaN은 자신과 일치하지 않는 유일한 값
* +연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작함.

**배열**

```js
let arr = [1,2,3,4,5];
arr[6] = 100
console.log(arr)    // 1,2,3,4,5,empty,100
console.log(arr[5]) // undefined

// 배열내 요소 찾기, toString
var ages = [10, 20, 30, 40, 50]

function checkAdult(ages){
    return ages >= 18;
}

console.log(ages.find(checkAdult));     // 20
console.log(ages.filter(checkAdult));   // 20,30,40,50
console.log(ages.toString())            // 10,20,30,40,50

// 배열 요소 추가 삭제
var fruits = ["banana", "apple", "grape"]
fruits.push("lemon")
fruits.pop('apple')
console.log(fruits)     // ['banana', 'apple', 'grape']

fruits.splice(0,2)
console.log(fruits)     // ['grape']

delete fruits[0]
console.log(fruits)     // empty

// 배열 정렬, 뒤집기, 채우기, 합치기
var fruits = ["banana", "apple", "grape", 'mango']
console.log(fruits.sort())      // ['apple', 'banana', 'grape', 'mango']
console.log(fruits.reverse())   // ['mango', 'grape', 'banana', 'apple']

var numbers = [40, 100, 1, 5, 20, 50]
console.log(numbers.sort(function(a,b) {return a-b}))   // [1, 5, 20, 40, 50, 100]
console.log(numbers.sort(function(a,b) {return Math.random() - 0.5}))   // [20, 40, 100, 1, 5, 50] (shuffle 기능)

numbers.fill(1)
console.log(numbers)    // [1, 1, 1, 1, 1, 1]

var bigArr = fruits.concat(numbers)
console.log(bigArr)     // ['mango', 'grape', 'banana', 'apple', 1, 1, 1, 1, 1, 1]

// 2차원 배열 안에 담기
var arr = [];
var arr2 = [];

for(var i=0; i<25; i++){
    arr[i] = i+1
}
console.log(arr)

for(var j=0; j<5; j++){
    arr2[j] = arr.splice(0,5)
}
console.log(arr2)

// for문 while문
var person = {fname : 'park', lname : 'jin', age : '29'};
var text = ''

for(var x in person){
    text += person[x] + ' '
}

console.log(text)       // park jin 29 

var car = ["BMW", "Volvo", "Ford"]
var test = ""

for(var i=0; i < car.length; i++){
    test += car[i] + " "
}
console.log(test)       // BMW Volvo Ford 

var test2 = ""
```

**함수**

* 함수는 항상 값을 반환함.

```js
var add = function(a,b) {
            return a+b;
        }
console.log(add(3,5));

// 함수 즉시 호출 표현식 (익명함수이며 일회용임)
var result = (function(a,b) {return a+b})(3,5)
console.log(result)

// ES6 화살표 함수
var add = (a,b) => a + b
console.log(add(3,5))

// arguments 객체
function findMax(a,b){
    var i;
    var max = -Infinity

    console.log(arguments)

    for(i=0; i < arguments.length; i++){
        if(arguments[i] > max){
            max = arguments[i]
        }
    }
    return max;
}

var result = findMax(2,6,4,7,1);
console.log(result)
```

**클로져**

* 렉시컬 스코프란 **함수를 어디에서 호출했는지가 아닌 어디서 정의했는지에 따라 상위 스코프를 결정하는 것**
* 반환된 내부함수가 자신이 선언됐을 때의 환경인 스코프를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 그 환경에 접근할 수있는 함수.
* 함수와 그 함수가 선언됐을 때의 렉시컬 환경과의 조합.
* **자신이 생성될 때의 환경을 기억하는 함수**
* **내부함수를 반환하여, 외부에서 호출할 수 있도록 변경**.
* **외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조**
* **상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하기 위해 사용**. (자바의 접근 제어자 private 라 생각하자.)

```js
function closure(){
    var cnt = 0;

    return function(){
        cnt++;
        console.log(cnt)
    }
}

var f = closure();
f();    // 1
f();    // 2
f();    // 3
```

**객체**

```js

// 객체 생성 방법
// 1. 빈 객체 생성 후 , 멤버 추가
var person = {};
        
person.firstName = "John";
person.lastName = "Doe";
person.age = 50;
person.eyeColor = "blue";
person.sayHello = function(){
    console.log('Hi my name is '+this.firstName)
}

console.log(person) // {firstName: 'John', lastName: 'Doe', age: 50, eyeColor: 'blue'}
console.log(person.firstName)   // John
person.sayHello();

for(var x in person){
    console.log("x : ", x)  // key값
    console.log("person[x] : ", person[x])  // value값
}

// 2. 객체 생성 후 동시 멤버 추가
var myObject = {
    favoriteFruit: "Apple",
    favoriteNum : 5,
    favoriteHobby : "golf",
    introduce: function(){
        return this.favoriteFruit + " " + this.favoriteHobby
    }
}

console.log(myObject.favoriteFruit)     // Apple
console.log(myObject.introduce())   // Apple golf

// 3. 생성자 객체 정의
function Person1(name, age){
    this.name = name;
    this.age = age;
}

var obj = new Person1("Javascript", "100")
obj.toString = function(){
    return "name=" + this.name + ", age=" +this.age
}
console.log(obj)    // Person1 {name: 'Javascript', age: '100', toString: ƒ}
console.log(obj.toString()) //name=Javascript, age=100
```

* 같은 생성자로 생성한 객체라도 서로 다른 함수를 가질 수 있음.

**Prototype (프로토타입)**

* 객체는 자신을 생성한 생성자의 prototype에 대한 참조인 __proto__와 constructor 속성을 자동으로 갖음.
* js는 프로토타입을 기반으로 상속을 구현함.

```js
function Person(name, age){
    this.name = name;
    this.age = age;
}

var obj = new Object();
var p = new Person("David", 10);
var s = new String();

console.log(Object.prototype===obj.__proto__)   // true  
console.log(String.prototype===s.__proto__)    // true
console.log(obj.constructor===Object)   // true
console.log(p.constructor===Person)     // true

var obj = new Object();
var obj2 = new Object();

console.log(obj.__proto__ === obj2.__proto__)   // true
console.log(obj2.__proto__ === Object.prototype)    // true

Object.prototype.getName = function(){
    return this.name
}

obj.name = "aaa"
obj2.name = "bbb"

console.log(obj.getName())  // aaa
console.log(obj2.getName()) // bbb
```