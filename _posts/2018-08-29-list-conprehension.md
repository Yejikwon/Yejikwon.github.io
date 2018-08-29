---
title: "리스트 컴프리헨션(List Conprehension)"
date: 2018-08-29 17:00:00 -0400
categories: python
tags: list_conprehension
---

> "파이썬 코딩의 기술" 책을 보고 정리한 내용입니다. Pyhon 공부를 <br> 하면서 알게된 점, 공유하고 싶은 점을 추가 작성했습니다.

## <span style="color:#36999F"> 리스트 컴프리헨션(List Conprehension) 이란? </span>
- 파이썬에는 한 리스트에서 다른 리스트를 만들어내는 간결한 문법이 있는데, 이 문법을 사용한 표현식을 **리스트 컴프리헨션**이라고 한다.

## <span style="color:#36999F"> 입력 리스트에 있는 아이템 걸러내기 </span>
- **1. map과 filter를 이용하는 방법** :
    - 일단 이 방법은 리스트 컴프리헨션을 이용하는 방법보다 훨씬 읽기 어려운 방법이다.
        - map, lambda, filter, list 등을 사용해야한다.
<br>

- **관련 코드** :

```python
a = [1,2,3,4,5,6,7,8,9,10]
alt = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, a)))
print(alt)

[result]
[4, 16, 36, 64, 100]
```
<br>

- **2. 리스트 컴프리헨션을 이용하는 방법** :
    - 입력 리스트에 있는 아이템을 간편하게 걸러내서 그에 대응하는 출력을 결과에서 삭제 할 수 있다.
    - 루프 뒤에 조건식을 추가해서 계산을 수행할 수 있다.
    - **[ ]** 로 묶어서 정의한다.
<br>

- **관련 코드** :

```python
a = [1,2,3,4,5,6,7,8,9,10]
even_squares = [x**2 for x in a if x % 2 == 0]
print(even_squares)

[result]
[4, 16, 36, 64, 100]
```
<br>

## <span style="color:#36999F"> 딕셔너리와 세트에서 사용되는 컴프리헨션 표현식 </span>
- 딕셔너리와 세트에도 리스트 컴프리헨션에 해당하는 문법이 있다.
- 컴프리헨션 문법을 쓰면 알고리즘을 작성할 때 파생되는 자료 구조를 쉽게 생성할 수 있다.

> **세트란?** <br>
집합과 동일하며, **{ }** 로 묶어서 정의한다. <br>

```python
num1 = {1,2,3}
num2 = {3,4,5}

print("num1.union(num2) = ", num1.union(num2))
print("num1.intersection(num2) = ", num1.intersection(num2))
print("num1 - num2 = ", num1 - num2)
```

```python
[result]
num1.union(num2) =  {1, 2, 3, 4, 5} # 합집합
num1.intersection(num2) =  {3} # 교집합
num1 - num2 =  {1, 2} # 차집합
```

<br>

- **list conprehension - 딕셔너리와 세트** :

```python
chile_ranks = {'ghost':1, 'habanero':2, 'cayenne':3}
rank_dict = {rank: name for name, rank in chile_ranks.items()}
chile_len_set = {len(name) for name in rank_dict.values()}

print(rank_dict)
print(chile_len_set)

print(type(rank_dict))
print(type(chile_len_set))
```

```ruby
[result]
{1: 'ghost', 2: 'habanero', 3: 'cayenne'}
{8, 5, 7}

<class 'dict'>
<class 'set'>
```
<br>

## <span style="color:#36999F"> list conprehension 장점 </span>
- <span style="color:#0975C2"> **[장점]** </span> 리스트 컴프리헨션은 추가적인 lambda 표현식이 필요 없어서 내장 함수인 map이나 filter를 사용하는 것보다 명확하다.
- <span style="color:#0975C2"> **[장점]** </span> 리스트 컴프리헨션을 사용하면 입력 리스트에서 아이템을 간단히 건너뛸 수 있다.

## <span style="color:#36999F"> list conprehension 단점 </span>
- <span style="color:#E42C51"> **[단점]** </span> 표현식이 두 개가 넘게 들어 있는 리스트 컴프리헨션은 이해하기 매우 어렵다.
- <span style="color:#E42C51"> **[단점]** </span> 입력 시퀀스에 있는 각 값별로 아이템을 하나씩 담은 **새 리스트를 통째로 생성**한다는 점이다.
    - 따라서, 입력이 클 경우 메모리를 많이 소모해서 프로그램을 망가뜨리는 원인이 된다.
    - 그렇다면 이 문제를 해결할 수 있는 방법은? <br>
      => 바로 <span style="color:#36999F"> 제너레이터 표현식(generator expression) </span> 이다! <br>
