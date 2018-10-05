---
title: "python3 - 비트연산자"
date: 2018-09-10 17:00:00 -0400
categories: python
tags: python
---

## <span style="color:#36999F"> 비트 연산자 (Bitwise Operators) </span>

| Operator | Description | Example |
| :------------: |:---------------------------:| :-------------------:|
| &    | AND 연산. 둘다 참일때만 만족 | (a & b) = 12 → 0000 1100 |
| \/   | OR 연산. 둘 중 하나만 참이여도 만족 | (a \| b) = 61 → 0011 1101 |
| ^    | XOR 연산. 둘 중 하나만 참일 때 만족 | (a ^ b) = 49 → 0011 0001|
| ~    | 보수 연산 | (~a) = -61 → 1100 0011 |
| <<   | 왼쪽 시프트 연산자. 변수의 값을 <br> 왼쪽으로 지정된 비트 수 만큼 이동 | a << 2 = 240 → 1111 0000|
| >>   | 오른쪽 시프트 연산자. 변수의 값을 <br> 오른쪽으로 지정된 비트 수 만큼 이동 | a >> 2 = 15 → 0000 1111 |

- 이 중 오늘 알아볼 내용은 <mark> <b>XOR 연산(^)</b></mark>이다.
- python3에서는 xor 연산을 ^ 기호로 표기한다.
- xor은 <mark> 다른 값</mark>을 찾을 때 유용하다. :kissing:
    - (예) A xor A = 0   # 0은 같음을 의미
    - (예) A xor A xor B = (A xor A = 0) xor B = 0 xor B = B
 
## <span style="color:#36999F"> XOR 연산 예시 </span> 
 ```python
def solution(v):
    answer = []
    x_list, y_list = [], []

    for list_v in v:
        x_list.append(list_v[0])
        y_list.append(list_v[1])

    answer = [x_list[0] ^ x_list[1] ^ x_list[2], y_list[0] ^ y_list[1] ^ y_list[2]]

    return answer

print(solution([[1, 1], [2, 2], [1, 2]]))
```

 ```python
실행결과: [2, 1]
```

- xor을 이용하여 3가지 값 중 다른 값을 찾아 낼 수 있었다.