---
title: "try/except/else/finally에서 각 블록의 장점을 이용하자"
date: 2018-09-05 12:00:00 -0400
categories: python
tags: functions
---

> "파이썬 코딩의 기술" 책을 보고 정리한 내용입니다. Pyhon 공부를 <br> 하면서 알게된 점, 공유하고 싶은 점을 추가 작성했습니다.

### 파이썬에는 <span style="color:#36999F">예외 처리 과정</span>에서 동작을 넣을 수 있는 <span style="color:#36999F">네 번</span>의 구분되는 시점이 있다.

## <span style="color:#36999F"> finally 블록 </span>
- 예외를 전달하고 싶지만, 에외가 발생해도 정리 코드를 실행하고 싶을 때 try/finally를 사용
    > 정리 코드: close() 같이 정리해주는 용도의 코드들을 의미

- try/finally 일반적 사용 예시: 파일 핸들러를 종료하는 작업
    - 예시 코드
    
       ```python
       handle = open('/tmp/random_data.txt') # IOError가 일어날 수 있음
       try:
          data = handle.read() # UnicodeDecodeError가 일어날 수 있음
       finally:
          handle.close()      # try: 이후에 계속 실행됨       
      ``` 
      
    - <span style="color:#DA2F67">try</span>: read 메서드에서 발생한 예외는 항상 호출 코드까지 전달됨
    - <span style="color:#DA2F67">finally</span>: handle의 close 메소드는 예외 발생 여부와 상관없이 정리 코드를 실행한다.
      
    - 제너레이터 표현식: 위의 예시를 제너레이터 표현식으로 변형할 경우
       ```python
       it = (len(x) for x in open('/tmp/my_file.txt'))
       print(it)    
      ``` 
     
    - 하지만 제너레이터 표현식은 즉시 이터레이터로 평가되므로 더는 진행되지 않는다. <br>
      <b>(제너레이터 표현식은 모든 출력 시퀀스를 메모리에 로딩하지 않고, 한 번에 한 아이템을 내주는 이터레이터(iterator)로 평가됨.) 
    - 필요할 때 제너레이터 표현식에 다음 출력을 생성하려면 <br>
     <span style="color:#36999F">내장 함수 next</span>로 반환받은 이터레이터를 한 번에 전진시키면 된다. <br>
       ```python
       print(next(it))
       print(next(it))
       
       100
       57
       ```
    - <span style="color:#DA2F67"> 제너레이터 표현식은 이터레이터로 한 번에 한 출력만 만드므로 메모리 문제를 피할 수 있다.</span>
<br>

## <span style="color:#36999F">제너레이터 표현식 + 제너레이터 표현식 </span>
- 제너레이터 표현식의 또 다른 강력한 결과는 다른 제너레이터 표현식과 함께 사용할 수 있다는 점이다.
- 다음은 앞의 제너레이터 표현식이 반환한 이터레이터를 다른 제너레이터 표현식의 입력으로 사용한 예다.

    ```python
       value = [100, 57, 15, 1, 12, 75, 5, 86, 89, 11]
       it = (x for x in value)
       print(it)
       
       print(next(it))
       print(next(it))
       
       roots = ((x, x**0.5) for x in it)
       
       print(next(roots))
       print(next(roots))
       print(next(roots))
     
       <generator object <genexpr> at 0x0000019FD2E199E8>
       100
       57
       (15, 3.872983346207417)
       (1, 1.0)
       (12, 3.4641016151377544)
    ```
  
- 다음은 앞의 제너레이터 표현식이 반환한 이터레이터를 다른 제너레이터 표현식의 입력으로 사용한 예다.    
- 이 이터레이터(roots)를 전진시킬 때마다 루프의 도미노 효과로 내부 이터레이터(it)도 전진시키고,
   조건 표현식을 계산해서 입력과 출력을 처리한다.
- <span style="color:#DA2F67"> 한 제너레이터 표현식에서 나온 이터레이터를 또 다른 제너레이터 표현식의 for 서브 표현식으로 넘기는 방식으로 제너레이터 표현식을 조합할 수 있다. </span>
- <span style="color:#DA2F67"> 큰 입력 스트림에 동작하는 기능을 결합하는 방법을 찾을 때는 제너레이터 표현식이 최선의 도구다.</span>
- 제너레이터 표현식은 서로 연결되어 있을 때 매우 빠르게 실행된다.
- <span style="color:#DA2F67">단, 제너레이터 표현식이 반환한 이터레이터에는 상태가 있으므로 이터레이터를 한 번 넘게 사용하지 않도록 주의한다!! <br> 
   why? 입력 인수가 이터레이터라면 이상하게 동작해서 값을 잃어버릴 수 있으므로(다른 챕터에서 더 자세히 설명)</span>