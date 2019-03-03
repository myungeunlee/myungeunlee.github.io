---
title:  "[React] Component LifeCycle"
categories: [react]
tags: lifecycle, react
author: myxxxxme
---

# Component LifeCycle
### 첫 컴포넌트 render 시,
1. componentWillMount()
2. render()
3. componentDidMount()

### state, props update 시,
1. componentWillReceiveProps()
2. shouldComponentUpdate()
3. componentWillUpdate()
4. render()
5. componentDidUpdate()


## Dump & Smart Components
Dump component
: stateless functional component
: 앞에 class가 아닌 **functional** 로 선언한 컴포넌트
: state가 존재하지 않음
: render 존재 x, Component 의 function 들을 사용할 수 없음
Smart component
: 일반적인 state 와 props 가 존재하는 컴포넌트
:앞에 class로 선언한 컴포넌트

``` java

//Smart Component
class Movie extends Component{
	render(){
		return(
			<div>~~~</div>
		)
	}
}

//Dump Component
functional Movie(poster){
	return(
		<img src={poster} />
	)
}

```

## AJAX on react
- **fetch('json데이터')** 를 이용해서 json데이터를 가져오는 듯
- ajax 는 비동기 방식으로 데이터를 가져옴, 즉 새로고침없이 데이터를 가져옴

### Promises
- 비동기
- 첫번째라인이 끝나든 말든 두번째라인이 실행되는 거임.

```javascript
componentDidMount(){
	fetch('json url')
	.then(response => respones.json())
	.then(json => console.log(json))
	.catch(error => console.log(error))
}
```


### Review
내기준 메모겸 정리해 두고 싶은 부분만 포스팅했다.
노마드코더 강의는 전체적으로 웃기고 재밌다.
영어로 진행되는데 자막도 재밌고 욕하는건 어쩜 너무 잘들리는지ㅋㅋ

자바스크립트 무료강의도 있길래 그것도 들어볼것이다.
인스타그램 클론코딩 강의 듣고 싶은데 300달러라서 패스ㅎㅎ
혹시 필요하신 분들은 [노마드코더] https://academy.nomadcoders.co/courses/category/KR react나 javascript 강의 들으면 좋을 듯 하다.



#### [글 쓰며 참고한 문서]
 - [react 강의] https://jusungpark.tistory.com/52
