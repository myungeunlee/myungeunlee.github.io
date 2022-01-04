---
layout: post
current: post
cover: assets/built/images/background-frontend.jpg
navigation: True
title: Array 실습 및 Object 객체
tags: [javascript]
class: post-template
subclass: 'post tag-javascript'
author: myungeunlee
---

## [실습] 특정 문자열이 포함된 배열 만들어서 반환하기
문자열 'e'가 노드로 구성된 배열을 만들어서 반환
```html
{% raw %}
<html>
<head></head>
<script>
function print(){
  let list = document.querySelectorAll("li");
  let listArray = Array.from(list); //Array 변환
  let eArray = listArray.filter(function(v){
    return v.innerText.includes("e");
  })
}
</script>
<body>
  <ul>
    <li>apple</li>
    <li>orange</li>
    <li>banana</li>
    <li>strawberry</li>
  </ul>
</body>
<html>

{% endraw %}
```

## 객체 생성하기
```html
{% raw %}
function getObj(){
  const name = "crong";

  const getName = function(){
    return name;
  }

  const setName = function(newname){
    name = newname;
  }

  const printName = function(){
    console.log(name);
  }

  //방법 1.
  return{
    getName : getName,
    setName : setName
  }

  //방법 2.
  return{getName, setName}

  var obj = getObj();
  console.log(obj.getName());

  //간단한 Object 생성
  const data = {
    let name,
    getName(){

    },
    age
  }
}
{% endraw %}
```

# Destructuring
## Destructuring Array

```html
{% raw %}
let data = ["mong", "lee", "eun", "myung"];
let [jisu,,jung] =data;
console.log(jisu, jung);  //"mong" "eun"
{% endraw %}
```

## Destructuring Object
let obj = {
  name : "myungeun",
  address : "Korea",
  age : 20
}

//할당한 변수명과 Object의 키값이 같은 경우
let {name, age} = obj;
console.log(name, age);         //"myungeun" 20

//할당한 변수명과 Object의 키값이 다른 경우  
let {name:myName, age:myAge} = obj;
console.log(myName, myAge);     //"myungeun" 20

## Destructuring JSON 파싱
```html
{% raw %}
let news = [
  {
    "title" : "LA",
    "imgurl" : "http://skfskdjflksdf"
    "list" : [
        "하이루",
        "이클립스",
        "비주얼스튜디오"
    ]
  }
  {
    "title" : "SC",
    "imgurl" : "http://skfskdjflksdf2312312"
    "list" : [
        "하이루123",
        "이클립스123",
        "비주얼스튜디오123"
    ]
  }
];

// 방법 1.
let [,SC] = news;
let {title, imgurl} = SC;
console.log(title, imgurl);    // "SC" "http://skfskdjflksdf2312312"

//방법 2.
let [, {title, imgurl}] = news;
console.log(title, imgurl);    // "SC" "http://skfskdjflksdf2312312"

//방법 3. function 이용
function getList([,{list}]){  //객체로 구성된 리스트를 받아 마지막 리스트 객체의 "list" value 값
  console.log(list);  
}

getNewsList(news);    //["하이루123","이클립스123","비주얼스튜디오123"]

{% endraw %}
```
# [글 쓰며 참고한 문서]
 - [클로저](https://hyunseob.github.io/2016/08/30/javascript-closure/)
 - [ES6](https://www.inflearn.com/course/es6-강좌-자바스크립트/)
