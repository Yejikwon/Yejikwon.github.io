---
title: "리스트 컴프리헨션(List Conprehension)"
date: 2018-08-29 15:00:00 -0400
categories: python
tags: List_conprehension
---

> "파이썬 코딩의 기술" 책을 보고 정리한 내용입니다. Pyhon 공부를 <br> 하면서 알게된 점, 공유하고 싶은 점을 추가 작성했습니다.

## <span style="color:#36999F"> PEP 8 스타일 가이드 </span>
- PEP란 Python Enhancement Proposal의 약자로 파이썬 개선 제안서를 의미한다.
- 가이드 url :
    - [PEP 8 스타일 가이드](https://www.python.org/dev/peps/pep-0008/)
    - [파이썬 코딩 스타일](http://pythonstudy.xyz/python/article/511-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%BD%94%EB%94%A9-%EC%8A%A4%ED%83%80%EC%9D%BC)
- PEP8과 같은 스타일 가이드를 따라야하는 이유는 다른 사람과 원활하게 협업하려면 공통된 스타일을 공유하는 것이 편하기 때문이다.
- 또한, 일관성 있는 스타일로 작성하면 나중에 본인의 코드를 수정할 때 더 쉽게 수정이 가능해서의 이유도 있다.

## <span style="color:#36999F"> 유니코드 문자, 바이너리 데이터 </span>
- **인코딩** :
    - 유니코드 문자 -> 바이너리 데이터로의 변환 (encode 메서드 사용)
    - 일반적인 인코딩은 UTF-8 이며, 한글의 경우 euc-kr을 사용하기도 한다.
    - 유니코드 문자열은 단순히 "문자셋의 규칙"일 뿐이다. <br>
    - 따라서, 다른 시스템으로 네트워크 전송을 하거나 파일에 적기위해선 바이트로 변환해야한다. <br>
<br>

- **인코딩 종류** :
    > **UTF (Unicode Transformation Format):** <br>
    UTF는 유니코드 형태의 문자를 변환하기 위한 공식이다. <br>
    유니코드는 4byte 구성되어 있기 때문에 사용하는 코드 <br> 범위에 따라서 1~4byte로 변환이 가능하게 된다. <br>
    <small> - http://nuli.navercorp.com/sharing/blog/post/1079940 </small>

    > **EUC (extend unix code):** <br>
    euc는 extend unix code의 약자로 유닉스에서 영어를 <br> 제외한 문자를 표시하기 위한 확장 부호를 의미한다. <br>
    그 중 euc-kr은 한글 표현을 위한 문자 인코딩인데, <br>
    영문은 KSC5636(ASCII와 동일하나 역슬래쉬를 원표시로 대체)으로 처리하고 한글은 KSC5601로 처리한다. <br>
    과거 euc-kr은 KSC5601-87의 완성형 한글이었으나 현재의 euc-kr은 KSC5601-92로 조합형 한글까지 사용 가능하다. <br>
    <small> - http://nuli.navercorp.com/sharing/blog/post/1079940 </small>
<br>

- **디코딩** :
    - 바이너리 데이터 -> 유니코드 문자로의 변환 (decode 메서드 사용) <br>
<br>

- **관련 코드** :

```ruby
a = "Hello world"
print(type(a))
>> <class 'str'>

b = a.encode('utf-8')
print(type(b))
>> <class 'bytes'>
```

## <span style="color:#36999F"> str(단순한 문자열, 유니코드), bytes(바이너리 데이터): <br> 문자타입 분리 해결을 위한 헬퍼함수 </span>
- **디코딩 헬퍼함수: 유니코드 문자로 변환** :

```python
def to_str(str):
    if isinstance(str, bytes):
        value = str.decode('utf-8')
        print("decoding success")
    else:
        value = str
    return value # str 인스턴스

print(to_str(b"Hello world!"))

[result]
decoding success
Hello world!
```

<br>

- **인코딩 헬퍼함수: bytes(바이너리 데이터)로 변환** :

```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        value = bytes_or_str.encode('utf-8')
        print("encoding success")
    else:
        value = bytes_or_str
    return value # str 인스턴스

print(to_bytes("Hello world!"))

[result]
encoding success
b'Hello world!'
```
<br>

- **정상적인 한글 인코딩, 디코딩** :

```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        value = bytes_or_str.encode('utf-8')
        print("utf-8 encoding success")
    else:
        value = bytes_or_str
    return value # str 인스턴스

def to_str(str):
    if isinstance(str, bytes):
        value = str.decode('utf-8')
        print("decoding success")
    else:
        value = str
    return value # str 인스턴스

print(to_bytes("한글 인코딩"))
print(to_str(b'\xed\x95\x9c\xea\xb8\x80 \xec\x9d\xb8\xec\xbd\x94\xeb\x94\xa9'))
```

```ruby
[result]
utf-8 encoding success
b'\xed\x95\x9c\xea\xb8\x80 \xec\x9d\xb8\xec\xbd\x94\xeb\x94\xa9'

decoding success
한글 인코딩
```
<br>

- **서로 다른 인코딩 종류에 따른 디코딩 error** :

```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        value = bytes_or_str.encode('euc-kr')
        print("euc-kr encoding success")
    else:
        value = bytes_or_str
    return value # str 인스턴스

def to_str(str):
    if isinstance(str, bytes):
        value = str.decode('utf-8')
        print("decoding success")
    else:
        value = str
    return value # str 인스턴스

print(to_bytes("한글 인코딩"))
print(to_str(b'\xc7\xd1\xb1\xdb \xc0\xce\xc4\xda\xb5\xf9'))
```

```ruby
[result]
euc-kr encoding success
b'\xc7\xd1\xb1\xdb \xc0\xce\xc4\xda\xb5\xf9'
Traceback (most recent call last):
  File "get_first_int.py", line 35, in <module>
    print(to_str(b'\xc7\xd1\xb1\xdb \xc0\xce\xc4\xda\xb5\xf9'))
  File "get_first_int.py", line 28, in to_str
    value = str.decode('utf-8')
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc7 in position 0: invalid continuation byte
```
