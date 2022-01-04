---
layout: post
current: post
cover: assets/built/images/background-frontend.jpg
navigation: True
title: let과 const
tags: [javascript]
class: post-template
subclass: 'post tag-javascript'
author: myungeunlee
---

## let과 var의 차이
-var로 선언한 변수는 지역우선으로 참조했다가 없으면, 전역에서도 사용할 수 있다.
-let로 선언한 변수는 지역에서만 사용할 수 있다.

## closure(클로저) 란?
- 함수 밖에서 선언된 변수를 함수 내부에서 사용할 때 클로저 발생.
- 정의한 함수(outFunc)는 함수(inFunc)를 반환하고, 사용은 바깥에서 함.
- 즉, 함수에서 정의한 환경을 기억하고 있다.

## let과 closure

```html
{% raw %}
<html>
<head></head>
<script>
var list = document.querySelectorAll("li");
for(var i=0; i<list.length; i++){
  list[i].addEventListener("click", function(){
    console.log(i+"번째 리스트 입니다");
  });
}
</script>
<body>
  <ul>
    <li>javascript</li>
    <li>java</li>
    <li>c/c++</li>
    <li>node.js</li>
  </ul>
</body>
<html>

{% endraw %}
```

여기서 i 값이 클로저이다.
따라서 i 값은 참조되면서 공유고 있음.

### [해결책]
var -> let 으로 변경.

## const 변수
- 선언된 변수 고정됨. 변경 불가능
- 배열과 object의 값을 변경은 가능함.

### immutable(변경이 불가능 한)
#### (참고) 객체와 문자열
문자열인 경우 변경이 불가능하다. 즉, 별도의 메모리를 사용하고 있다.(값의 의한 복사)
반대로 객체는 mutable 함. 즉, 같은 메모리를 참조하고 있음.
#### immutable array 만들기
- (이유) 뒤로가기, 앞으로가기를 할 때 객체는 현재 저장한 값이 계속 업데이트되고 있기 때문에 이전의 값이 무엇인지 기억하지 못하고 있음.
```html
{% raw %}
const list = ["apple", "orange", "watermelon"];
list2 = [].concat(list, "banana");
console.log(list, list2); //["apple", "orange", "watermelon"], ["apple", "orange", "watermelon", "banana"]
{% endraw %}
```

## String 새로운 메서드
- startsWith : 시작문자 매치 여부
- endsWith : 끝문자 매치 여부
- includes : 문자 포함 여부
```html
{% raw %}
let str = "hello LA ~ ^^&";
let matchstr = "hello";
console.log(str.startsWith(matchstr)); //true
console.log(str.endsWith(matchstr)); //false;
console.log(str.includes(matchstr)); // true;

{% endraw %}
```

## for of
```html
{% raw %}
var data = [1,2,undefined, NaN, null, ""];

//방법1
data.forEach(function(value){
  console.log("valueis", value);
})

//방법2 : for in 문제점 : 해당 객체뿐만아니라 상위객체(proptotype에 추가된 3)까지 나타냄.
Array.prototype.getIndex = function(){};
for(let idx in data){
  console.log(data[idx]); //... function(){}
}

//방법3 : for of : for in의 문제점 해결
for(let idx of data){
  console.log(data[idx]);
}
//문자열 순회 기능
var str = "hello world!!!"
for(let val of str){
  console.log(val); //"h" "e" "l" "l" "o" " " ...
}

{% endraw %}
```


## spread operator
- 값을 펼쳐준다.(예시를 보면 pre 배열객체가 배열로 전체복사되는 게 아님. 값만 복사해서 펼쳐준다고 보면 됨. 따라서 []배열안에 spread operator와 객체를 넣어줌)
- 참조 값은 다름, 서로 다른 데이터
```HTML
{% raw %}
let pre = ["apple", "oragne", 100];
let newData = [...pre];
console.log(pre, newData); // ["apple", "oragne", 100  ["apple", "oragne", 100]
console.log(pre == newData); // false
{% endraw %}
```

배열에 특정 배열을 끼워 넣는 기능.
```HTML
{% raw %}
let pre = [100, 200, "hello", null];
let newData = [0,1,2,3, ...pre, 4];

{% endraw %}
```

배열 값을 함수의 매개변수에 할당.
```html
{% raw %}
function sum(a,b,c){
  return a+b+c;
}
let pre2 = [100, 200, 300];

sum.apply(null, pre2); //600
sum(...pre2);

{% endraw %}
```

## from 매소드로 배열 만들기

```html
{% raw %}
function addMark(){

  //방법 1
  //arguments 내부 지역변수를 이용해서 인자값을 가져옴.
  //가변적인 파라미터가 들어오는 경우 사용됨.
  let newData = [];
  for(let i=0; i<arguments.length; i++){
    newData.push(arguments[i]+"!");
  }
  console.log(newData);


  //방법 2
  let newArray = Array.from(arguments);
  let newData2 = arguments.map(function(value){
    return value + "!";
  });
  console.log(newData);
}

addMark(1,2,3,4,5,6,7);
{% endraw %}
```

# [글 쓰며 참고한 문서]
 - [클로저](https://hyunseob.github.io/2016/08/30/javascript-closure/)
 - [ES6](https://www.inflearn.com/course/es6-강좌-자바스크립트/)
