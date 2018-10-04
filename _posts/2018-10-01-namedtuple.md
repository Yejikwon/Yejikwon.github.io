---
title: "collections 모듈 - namedtuple"
date: 2018-10-01 10:32:00 -0400
categories: python
tags: python
---

> <b> Excelsior-JH</b> 님 사이트를 참고하였습니다. <br>
  http://excelsior-cjh.tistory.com/97?category=966334

## <span style="color:#36999F"> namedtuple 이란? </span>
- 일반 튜플(basic tuple)은 위치에 의존한다. <br> (그러나 키워드(키)로 접근이 불가능하다. :neutral_face: )
- 키워드 인수로 접근할 수 있는 방법에 대해 찾다가 <br> <b> namedtuple 인스턴스 </b>를 알게되었다.
- <mark> collections.namedtuple(typename, field_names, verbose=False, rename=False) </mark>

## <span style="color:#36999F"> tuple() vs namedtuple() </span>
- 자세한 예시는 [python docs](https://docs.python.org/)에서 확인할 수 있다.
- tuple() 예시
    ```python
    # 리스트 안에 (score, weight) 튜플 사용
    grades = []
    grades.append((95, 0.45, 'Great job'))
    grades.append((85, 0.55, 'Better next time'))
    total = sum(score * weight for score, weight, _ in grades)
    total_weight = sum(weight for _, weight, _ in grades)
  
    average_grade = total / total_weight
    print(average_grade)
    ```
<br>    
- namedtuple()은 <mark> csv나 DB에서 테이블을 가져올 때 </mark> 유용하게 사용할 수 있다. :thumbsup:
- 요구 사항이 변해서 단순 데이터 컨테이너에 동작을 추가해야할 때 쉽게 바꿀 수 있게 해준다.
- namedtuple() 예시
    ```python
    import collections
    
    # namedtuple()은 field_names를 이용해 값을 지정할 수 있다.
    Grade = collections.namedtuple('Grade', ('score', 'weight'))
    
    class Subject(object):
    def __init__(self):
        self._grades = []

    def report_grade(self,score, weight):
        self._grades.append(Grade(score, weight))

    def average_grade(self):
        total, total_weight = 0, 0
        for grade in self._grades:
            total += grade.score * grade.weight
            total_weight += grade.weight
        return total / total_weight
    ```
    
    ```python
    Person = collections.namedtuple("Person", 'name age gender')
    
    P1 = Person(name='Jhon', age=28, gender='남')
    P2 = Person(name='Sally', age=28, gender='여')
    for n in [P1, P2]:
    print('%s는(은) %d세의 %s성 입니다.' %n)
    
    결과
    Jhon는(은) 28세의 남성 입니다.
    Sally는(은) 28세의 여성 입니다.
    
    print(P1.name, P1.age, P1.gender)
    print(P2.name, P2.age, P2.gender) 
    
    결과
    Jhon 28 남
    Sally 28 여
    
    출처: http://excelsior-cjh.tistory.com/97?category=966334 [EXCELSIOR]
    ```
    
## <span style="color:#36999F"> namedtuple의 제약 </span>
- namedtuple이 여러 상황에서 유용하긴 하지만, namedtuple로 만들 클래스에 기본 인수 값을 설정할 수 없다. <br>
   <span style="color:#0975C2"> 그래서 데이터에 선택적인 속성이 많으면 다루기 힘들어진다.  :disappointed_relieved: </span>
- namedtuple 인스턴스의 속성 값을 여전히 숫자로 된 인덱스와 순회 방법으로 접근할 수 있다.
- <mark> namedtuple 인스턴스를 사용하는 방식을 모두 제어할 수 없다면, <br> :star: 클래스 :star: 를 직접 정의하는 게 낫다. </mark>