---
title: "리스트 중복제거"
date: 2018-10-02 10:42:00 -0400
categories: python
tags: python
---

## <span style="color:#36999F"> 리스트 중복제거 </span>
- 원본 리스트에서 값 중복제거를 하고 싶을 때 사용할 수 있는 방법 2가지가 있다.
- 원본 리스트
    ```python
    host, group  = [], []
        for multi_info in multiple_info:
            host.append(multi_info.split(' ')[0])
            group.append(multi_info.split(' ')[2])
    ```
     ```python
    print(group)
    ['1', '1', '1', '1', '1', '1', '1', '2', '2', '2', '2', '2', '2', '2', '3', '3', '3', '3', '3', '3']
    ```

## <span style="color:#36999F"> set 함수를 활용한 중복제거 </span> 
 ```python
ex_group = list(set(group))
print(ex_group)
['3', '2', '1']
```
- set함수는 중복제거는 되지만, `'순서와 상관없이'` 중복만 제거하는 
  것을 볼 수 있다. <br>
- 그렇다면, 순서를 유지하면서 중복을 제거하고 싶다면? <br>  

## <span style="color:#36999F"> OrderedDict 라이브러리를 활용한 중복제거 </span> 
 ```python
from collections import OrderedDict

ex_group = list(OrderedDict.fromkeys(group))
print(ex_group)
['1', '2', '3']
```
- OrderedDict 라이브러리를 사용하면 원본 리스트가 가진 값을 순서대로 정렬 및 중복 제거 수행 <br>