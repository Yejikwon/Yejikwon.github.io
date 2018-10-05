---
title: "자바스크립트 공부 1"
date: 2018-09-04 17:00:00 -0400
categories: javascript
tags: javascript
---

## <span style="color:#36999F"> 실습환경 </span>
- 작업 환경: [sublimetext editor](http://www.sublimetext.com/3)
 
## <span style="color:#36999F"> Developer console 활용 잘하기 </span> 
- console tab에서 내가 사용해보고자 하는 js 명령어를 쓸 수 있다.

## <span style="color:#36999F"> 변수 선언 및 초기화 </span> 

```ruby
var a=10, b=20, c=30;
```

## <span style="color:#36999F"> 변수의 활용 </span> 
- 값 입력 받기: prompt 명령 사용

```js
lecture03.js

var name=prompt("이름을 입력해 주세요.");
console.log(name, "님 환영합니다.");
```

```html
index.html

<html>
	<head>
		<meta charset="utf-8">
		<script src="lecture03.js"></script>
	</head>
	<body>
		This is a basic HTML page
	</body>
</html>
```

## <span style="color:#36999F"> 기본자료형 </span> 
- typeof() : 변수의 타입 확인 가능
- 자료형 number: 정수, 실수를 구분하지 않고 number라고 쓴다
- <mark> parseInt, parseFloat </mark> : 자료형 변환 시 사용

```js
lecture05.js

var height=prompt("키를 입력해주세요.");
console.log(height, typeof(height));

var height_int = parseInt(height);
console.log(height_int, typeof(height_int));

var height_float = parseFloat(height);
console.log(height_float, typeof(height_float));
```

```html
index.html

<html>
	<head>
		<meta charset="utf-8">
		<script src="lecture05.js"></script>
	</head>
	<body>
		This is a basic HTML page
	</body>
</html>
```

```ruby
실행결과:
183.6 입니다. string
183 "number"
183.6 "number"
```