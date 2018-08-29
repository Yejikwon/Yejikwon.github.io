---
title: "markdown 기초"
date: 2018-08-23 19:30:00 -0400
categories: markdown
tags: jekyll markdown
---

포스팅 시, 유용한 기초 markdown 내용을 작성하였습니다.

## 지킬(Jekyll)과 마크다운(Markdown)

Jekyll 은 마크다운 문법을 통해 작성된다. 따라서 자주 쓰는 문법을 계속 정리해보려고 한다.

### 내용 정리 시, > 를 사용하여 작성을 시작하면 아래와 같이 표현할 수 있다.

> ## 글자 크기는 '#'문자의 수로 제어가능하다.

### " * " 을 쓰면 순서없는 목록표시, "1."을 쓰면 순서가 있도록 목록을 작성할 수 있다.

>* 예시 1
* 예시 2
* 예시 3<br>
1. 예시 1
2. 예시 2
3. 예시 3

<br>

### - 3개(---)를 넣으면 글 간을 구분 짓는 선이다.

---

<br>


### 링크는 다음과 같이 표시된다 [화면에노출하고싶은 표시] (실제 링크 url)

> [네이버](www.naver.com)
<br>

### 글씨를 굵게 변화시키려면 ** ** 안에 글자를 넣고, 기울이기를 사용하려면 * * 안에 글을 넣는다.

> **굵게** *기울임*
<br>

### 인용, 코드 블럭을 나타내고자 할 때는 >을 시작으로 설명을 쓴다.

> import Firebase <br>
import UI Kit <br>
class UIControllerview { <br>
} <br>

<br>

### 그외 일반 html 의 적용도 가능하다.

> <center> 중앙 정렬 </center>


### 표 삽입

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

<br>

그 외 참고자료: [markdown](https://namu.wiki/w/마크다운) 참고

<br>
