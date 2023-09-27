

# Python 기초
### 기본 문법
##### Collection
- list  :   순서를 가지는 값의 목록

  ```python list = [2,4,5]```
  
- tuple :   list와 마찬가지로 순서를 가지는 값의 목록이지만 구성요소간 변경은 불가하다.

  ```python list = (2,4,5)```
- dictionary : 키와 쌍을 가지는 자료형으로 {}로 감싸서 표현한다. 

  ```python list = {"name":"홍길동,"age" : 20}```
- set : 집합 자료형으로 {}감싸서 표현하며 순서를 가지지 않고 값이 중복 될 수 없다. 

  ```python list = {"name":"홍길동,"age" : 20}```

#### if 문
- if <조건>
   
  elif <조건2>

  elif <조건3>

  else :

#### Func 함수
``` python
    def printPerson(name, age, major = '전산학과'):
        print(f"이름:{name}, 연령:{age}, 전공:{major}")
    printPerson("규히", 22);
```
#### 가변 인자 파라미터
``` python
  def personPrint(*args):
    for value in args:
        print(*person)
```
``` python
  def printPersons(name, age, major):
     print(name, age, major)

person = {'name' : '홍길동', 'age' : 20, 'major' : '전산'}
printPersons(**person)
```

- 가변 인자(말 그대로 별할 수 있는 파라미터)를 가지는 함수의 경우에 튜플 언패킹을 사용하여 인자 전달한다.
- 언패킹을 사용하여 함수를 호출할 때, 데이터의 구분은 데이터의 순서에 의존해야한다.
- 두번째 예시와같이 딕셔녀리를 인자로 넘길 경우, **을 써서 타고 들어가도록 한다. 
  
### 모듈
##### 모듈 정의
- 변수나 함수 또는 클래스를 모아넣은 파일 
- 모듈은 다른 프로젝트나, 프로그램에서 재사옹 가능하도록 해준다

##### 모듈 생성
- 하나의 모듈에는 재사용하고자 하는 변수나, 함수 ,클래스 등을 별도의 파일로 작성한 것인다. 
- 파이썬 소스 파일의 이름은 모듈명이 된다.
- 모듈을 사용하기 위해서는 반드 시 사용할 모듈을 import 해야한다. 
- 모듈은 from 구문을 사용하여 선택적 요소를 할 수 있따. 

