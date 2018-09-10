---
title: "이터레이터와 제너레이터의 개념"
date: 2018-08-30 16:00:00 -0400
categories: python
tags: concepts
---
> 앞으로 작성할 내용은 아래 블로그 글을 참고하여 작성한 글이다. <br>
    - [이터레이터와 제너레이터](https://mingrammer.com/translation-iterators-vs-generators/)

## <span style="color:#36999F"> 1. 컨테이너(Container) </span>
- 원소들을 가지고 있는 데이터 구조
- 메모리에 상주하는 데이터 구조로, 보통 모든 원소값을 메모리에 가지고 있다.
- 기술적으로, 어떤 객체가 특정한 원소를 포함하고 있는지 아닌지를 판단할 수 있으면 컨테이너라고 한다.
-  대부분의 컨테이너는 또한 이터레이블(iterable)하다.
- Membership Test[^1]가 가능하다. <br>
   [^1]: list, set, dict, tuple, str과 같이 데이터 구조(Membership)에 따라 각 값들을 테스트 하는 것.
- 컨테이너의 종류
    - list, set, dict, tuple, str, deque, counter, namedtuple, ....
    
    <br>

## <span style="color:#36999F"> 2. 이터레이블 (Iterable) </span>
-  의미: member를 하나씩 차례로 반환 가능한 object
-  예시: <br>
    - sequence type: list, str, tuple <br>
    - non-sequence type: dict 나 file <br>
        <br>
        
-  일례로 파일 열기, 소켓 열기 등도 있다.

- ### <b>이터레이블과 이터레이터 사이에는 중요한 차이점이 있다.</b>

```python
x = [1, 2, 3]
y = iter(x)
z = iter(x)

print(next(y))
print(next(y))
print(next(z))

print("================================")
print(type(x))
print(type(y))

- 결과

1
2
1
================================
<class 'list'>
<class 'list_iterator'>
```

-  <b>이터레이블(iterable)</b> : x = [1, 2, 3]과 같은 데이터구조(리스트) 혹은 member를 하나씩 차례로 반환 가능한 object <br>
-  <b>이터레이터(iterator)</b> : 이터레이블로부터 값을 생성해내는 이터레이터의 인스턴스 <br>
<br>

- 파이썬 코드 디스어셈블링(어셈블리 수준으로 코드 해부)

```python
import dis

x = [1, 2, 3]

print("================================")
dis.dis('for _ in x: pass')

================================
  1           0 SETUP_LOOP              12 (to 14)
              2 LOAD_NAME                0 (x)
              4 GET_ITER
        >>    6 FOR_ITER                 4 (to 12)
              8 STORE_NAME               1 (_)
             10 JUMP_ABSOLUTE            6
        >>   12 POP_BLOCK
        >>   14 LOAD_CONST               0 (None)
             16 RETURN_VALUE
```
- 파이썬 코드를 디스어셈블링(어셈블리 수준으로 코드를 해부함) 해보면 <br>
 iter(x)를 실행시키는데 필요한 GET_ITER를 호출하고 있음을 볼 수 있다. <br>
 FOR_ITER는 모든 원소를 반복적으로 가져오기 위해 next()를 호출하는것과 동일한 일을 수행하는 명령어지만, <br>
 인터프리터에서 속도에 최적화 되어있기 때문에 바이트 코드 명령어에서는 보이지 않는다. <br>

    <br>

## <span style="color:#36999F"> 3. 이터레이터 (Iterator) </span>
-  next()를 호출할 때 다음값을 생성해내는 상태를 가진 헬퍼 객체
-  예시: <br>
    - sequence type: list, str, tuple <br>
    - non-sequence type: dict 나 file <br>
        <br>
        