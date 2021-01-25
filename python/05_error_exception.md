# 에러 & 예외 처리

<br>

### 문법 에러(Syntax Error)

- 에러 발생 시 `SyntaxError`라는 키워드와 함께, 에러의 상세 내용을 보여준다.

- `파일이름`과 `줄번호`, `^` 문자를 통해 파이썬이 코드를 읽어 들일 때(`parser`) 문제가 발생한 위치를 표현한다.

- `parser` 는 줄에서 에러가 감지된 가장 앞의 위치를 가리키는 작은 '화살표(`^`)'를 표시한다.

```python
# : 빼먹기

if True:
    print('참')
else
    print('거짓')
#   File "<ipython-input-1-04c4e0453d50>", line 3
#     else
#         ^
# SyntaxError: invalid syntax
```

```python
# EOL 에러 (괄호 닫기 오류)
# str ' 제대로 안닫기

print('hi)
#         File "<ipython-input-2-8878a92e9096>", line 1
#     print('hi)
#               ^
# SyntaxError: EOL while scanning string literal
```

<br>

### 예외(Exception)

- 실행 도중 예상하지 못한 상황(exception)을 맞이하면, 프로그램 실행을 멈춘다.

- 문법적으로는 옳지만, 실행시 발생하는 에러

아래 제시된 모든 에러는 `Exception`을 상속받아 이뤄진다.

```python
# ZeroDivisionError
10 * (1/0)
# ZeroDivisionError: division by zero
```

```python
# NameError
# 지역 혹은 전역 이름 공간내에서 유효하지 않는 이름
# 즉 정의되지 않은 변수를 호출 하였을 경우
print(abc)
# NameError: name 'abc' is not defined
```

```python
# TypeError
# 자료형에 대한 타입 자체가 잘못 되었을 경우
# 지원하지 않는 연산..
1 + '1'
# TypeError: unsupported operand type(s) for +: 'int' and 'str
```

```python
# 함수 호출과정에서 TypeError
# 문자열은 반올림을 할 수 없습니다..
round('3.5')
# TypeError: type str doesn't define __round__ method
```

```python
# 함수호출 과정에서의 오류 (1) 필수 argument 누락
# 'k' 위치인자 하나가 없다.
# random.sample([1, 2, 3], 1)
import random
random.sample([1, 2, 3])
# TypeError: sample() missing 1 required positional argument: 'k'
```

```python
# 함수호출 과정에서의 오류 (2) argument 개수 초과
random.choice([1, 2, 3], 6)
# TypeError: choice() takes 2 positional arguments but 3 were given
```

```python
# ValueError

# 자료형에 대한 타입은 올바르나 값이 적절하지 않는 경우
int('3.5')
# ValueError: invalid literal for int() with base 10: '3.5'

# 존재하지 않는 값을 찾고자 할 경우
#(find()로 해결 가능<-존재하지 않는 값의 경우 -1 반환)
numbers = [1, 2]
numbers.index(3)
# ValueError: 3 is not in list
```

```python
# IndexError
# 존재하지 않는 index로 조회할 경우
empty_list = []
empty_list[1]
# IndexError: list index out of range
```

```python
# KeyError
# 딕셔너리에서 Key가 없는 경우 
songs = {'sia': 'candy cane lane'}
songs['queen']
# KeyError: 'queen'
```

```python
# ModuleNotFoundError
# 모듈을 찾을 수 없는 경우
import reque
# ModuleNotFoundError: No module named 'reque'
```

```python
# ImportError
# 모듈을 찾았으나 가져오는 과정에서 실패하는 경우 (존재하지 않는 클래스/함수 호출)
from random import sampl
# ImportError: cannot import name 'sampl' from 'random'
```

```python
# KeyboardInterrupt
# 사용자가 의도적으로 멈췄을 때
while True:
    continue
# 정지 버튼이나 ctrl + c를 눌렀을 때
```

<br>

### 예외 처리(Exception Handling)

> #### `try` & `except`

```python
try:
    <코드 블럭 1>
except (예외):
    <코드 블럭 2>
```

- `try` 아래의 코드블락(code block)이 실행된다.
- 예외가 발생되지 않으면, **`except`없이 실행이 종료 된다.**
- 예외가 발생하면, **남은 부분을 수행하지 않고**, `except`가 실행된다.

```python
try: 
    num = input('값을 입력하시오 : ')
    print(int(num))
except ValueError:
    print('숫자를 입력하라니까!!')
```

<br>

**에러 메시지 처리 `as`**

- `as` 키워드를 활용하여 에러 메시지를 보여줄 수도 있다.

```python
try:
    <코드 블럭 1>
except 예외 as err:
    <코드 블럭 2>
```

```python
try:
    empty_list = []
    print(empty_list[-1])
except IndexError as err:
    print(f'{err}, 오류가 발생했습니다.')
```

<br>

**복수의 예외 처리**

- 하나 이상의 예외를 모두 처리할 수 있다.
- 괄호가 있는 튜플로 여러 개의 예외를 지정한다.
- 여기서 중요한 내용은 **에러가 순차적으로 수행됨**으로, 가장 작은 범주부터 시작해야 한다.
   ex) int를 입력받아야 하는데 문자열일때와 0일때 -> 0일때, 문자열일때 순

```python
try:
    <코드 블럭 1>
except (예외1, 예외2):
    <코드 블럭 2>


try:
    <코드 블럭 1>
except 예외1:
    <코드 블럭 2>
except 예외2:
    <코드 블럭 3>
```

<br>

**else**

- 에러가 발생하지 않는 경우 수행되는 문장은 `else`를 이용한다.
- 모든 except 절 뒤에와야 한다.
- try 절이 예외를 일으키지 않을 때 실행되어야만 하는 코드에 적절하다.

```python
try:
    <코드 블럭 1>
except 예외:
    <코드 블럭 2>
else:
    <코드 블럭 3>
```



**finally**

- 반드시 수행해야하는 문장은 `finally`를 활용한다.
- 즉, 모든 상황에 실행되어야만 하는 코드를 정의하는데 활용한다.
- 예외의 발생 여부과 관계없이 try 문을 떠날 때 항상 실행한다.

```python
try:
    <코드 블럭 1>
except 예외:
    <코드 블럭 2>
finally:
    <코드 블럭 3>
```

```python
try:
    print('성적 파일을 읽어옵니다.')
    data = {'python': 'A+'}
    data['java']
except KeyError as err:
    print(f'{err}는 딕셔너리에 없는 키입니다.')
finally:
    print('성적 파일을 종료합니다.')
```

<br>

### 예외 발생 시키기(Exception Raising)

##### 1. `raise`를 통해 예외를 강제로 발생시킬 수 있다

```python
raise <에러>('메시지')
```

```python
raise ZeroDivisionError('0으로 감히 나눠?')
# ----> 1 raise ZeroDivisionError('0으로 감히 나눠?')
# ZeroDivisionError: 0으로 감히 나눠?
```

- 예외 발생 명세 예시

  리스트를 받아 평균을 반환하는 def avg(scores)를 작성하세요.
  scores의 길이가 0인 경우 Exception과 메시지를 발생시키세요.

  예) Exception: 학생이 없습니다.
  정상적인 경우에는 결과를 return합니다. 

<br>

##### 2. `assert`로 예외를 발생시킬 수 있다. 

##### 보통 **상태를 검증하는데 사용**되며 무조건 `AssertionError`가 발생한다.

```python
assert Boolean expression, error message

assert len([1, 2]) == 1, '길이가 1이 아닙니다.'
```

- 위의 검증식이 거짓일 경우를 발생한다. 일반적으로 디버깅용도로 사용된다.
- https://docs.python.org/ko/3/reference/simple_stmts.html#the-assert-statement