# Python



### 기초 문법(Syntax)

- 주석(Comment => `#`, `''' '''`)은 실행되지 않습니다.
- 문장(statement)은 파이썬이 실행 가능(executable)한 최소한의 코드 단위
  - 1줄에 1문장(statment)'이 원칙

```python
print('hello');'print('world') # X

print('hello')
print('world') # O
```



> #### 할당 연산자(Assignment Operator): `=`

- 변수는 `=`을 통해 할당(assignment) 된다.
- 같은 / 다른 값을 동시에 할당 가능, 변수 값 교환 가능

```python
# 같은 값
x = y = 10
print(x, y)

# 다른 값
x, y = (1, 10) # 좌변과 우변의 개수가 일치해야 함
print(x, y)

# 변수의 값 SWAP
x = 10
y = 100
x, y = y, x
print(x, y)

## 임시 변수를 활용하여 변수의 값 SWAP
temp = x # temp : temporary, 임시 상자의 개념
x = y 
y = temp
print(x, y)
```

 

> #### 식별자(Identifiers)

- 변수, 함수, 모듈, 클래스 등을 식별하는데 사용되는 이름(name)

  - 영문알파벳(대문자와 소문자), 밑줄(_), 숫자로 구성

  - 첫 글자에 숫자가 올 수 없다.

  - 길이에 제한 없음, 대소문자(case) 구별

  - 사용할 수 없는 키워드( + 내장함수, 모듈)

    ```python
    import keyword
    print(keyword.kwlist)
    ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
    ```

    

### 데이터 타입(Data Type)

> ####  **숫자**(Number) 타입

##### `int` (정수, ingteger)

- 8진수 : `0o` / 2진수 : `0b` / 16진수: `0x` 로도 표현 가능

##### `float`(부동소수점, 실수, floating point number)

- floating point rounding error
- 실수의 연산

##### `complex`(복소수, complex number)

- 실수로 표현되는 실수부와 허수부(`j`)



> ####  **문자**(String) 타입



> #### **참/거짓**(Boolean) 타입







> ### 주의사항

-  List 표기 방식

```python
## PEP-8 가이드에 따르면 여러 줄의 생성자의 닫히는 괄호(소, 중, 대)는
## (1) 첫번째 문자(요소) 위치에 오거나 (2) 마지막 줄에서 생성자가 시작되는 첫번째 열에 위치합니다.
## 저희는 (1) 방식으로 사용할 것입니다.

food = [
    '샐러드'
    '까르보붉닭'
    '제육볶음'
    '허니버터칩'
    '꿔바로우'
    '짜파게티'
    '일본가정식'
]
```



> ### 관련 함수

| 내장 함수<br />(Built-in function) |                            |                                                              |
| ---------------------------------- | -------------------------- | ------------------------------------------------------------ |
| type()                             | 해당 데이터 타입 확인      | `print(variables, type(variables))`<br />`<class 'int'>`<br />int, str, float, tuple... |
| id()                               | 해당 값의 메모리 주소 확인 | 할당 !== 메모리 기록                                         |
| round()                            | 반올림                     | 0~4는 내림, 5는 동일하게 작동하지 않고 반올림 방식에 따라 다름<br/>짝수에서 5는 내림 / 홀수에서 5는 올림 (?) |

| 모듈    |                                                              | 외장함수                                    | import 함수명                                                |
| ------- | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------ |
| keyword | 식별자가 될 수 없는 목록                                     | `keyword.kwlist`                            |                                                              |
| sys     | 1. 파이썬에서 가장 큰 숫자를 활용하기 위해 불러온 모듈<br />2. `epsilon` 은 부동소수점 연산에서 반올림을 함으로써 발생하는 오차 상환 | `sys.maxsize`<br />`sys.float_info.epsilon` | `sys.maxsize` 의 값은 2**63 - 1 <br />=> 64비트에서 부호비트를 뺀 63개의 최대치 <br />= 9223372036854775807 85070591730234615847396907784232501249<br /> |
|         |                                                              |                                             |                                                              |

round()

round 처리 : 2진수 처리방식에 의해, 부동소수점을 활용해 계산



부동소수점 방식

- 많은 언어가 사용하는 방식



> ### 알아두기

**Syntax) 여러 줄 작성**

- 기본적으로 파이썬에서는 `;`을 작성하지 않으나, 한 줄로 표기할때는 `;`을 작성하여 표기(지양)

```python
print('hello');print('world')
```

- 줄을 여러줄 작성할 때는 역슬래시`\`를 사용할 수 있다

```python
print('hello\
world')
```

**Syntax) 여러줄 문자열의 관례(convention)**

```python
print("""hello
world""")
```

---

**Identifiers) 내장함수의 이름을 식별자로 사용한다면 일어나는 일**

- 내장함수가 새로운 값으로 인식되어 이전의 기능을 수행하지 못함
- `del 함수명`으로 새로 생성한 식별자를 삭제해야

---

**Int) 파이썬에서 표현할 수 있는 가장 큰 수**

- 파이썬에서 가장 큰 숫자를 활용하기 위해 sys 모듈을 불러온다.
- 파이썬은 기존 C 계열 프로그래밍 언어와 다르게 정수 자료형(integer)에서 오버플로우가 없다.
- 임의 정밀도 산술(arbitrary-precision arithmetic)을 사용하기 때문이다.

> **오버플로우(overflow)**

- 데이터 타입 별로 사용할 수 있는 메모리의 크기가 제한되어 있다.
- 표현할 수 있는 수의 범위를 넘어가는 연산을 하게 되면, 기대했던 값이 출력되지 않는 현상, 즉 메모리가 차고 넘쳐 흐르는 현상

> **임의 정밀도 산술(arbitrary-precision arithmetic)**

- 사용할 수 있는 메모리양이 정해져 있는 기존의 방식과 달리, 현재 남아있는 만큼의 가용 메모리를 모두 수 표현에 끌어다 쓸 수 있는 형태
- 특정 값을 나타내는데 4바이트가 부족하다면 5바이트, 더 부족하면 6바이트까지 사용할 수 있게 유동적으로 운용



**int) n진수 만들기**

```python
binary_number = 0b10 
octal_number = 0o10
decimal_number = 10
hexadecimal_number = 0x10
print(f"""
2진수 : {binary_number} # 2
8진수 : {octal_number} # 8
10진수 : {decimal_number} # 10
16진수 : {hexadecimal_number} # 16
""")
```

---

**float) 컴퓨터식 지수 표현 방식**

- e와 E 둘 중 어느 것을 사용해도 무방

```python
pi = 314e-2
print(pi, type(pi))
# 3.14 <class 'float'>
```



**float) floating point rounding error**

- 실수를 컴퓨터가 표현하는 과정에서 부동소수점을 사용하며, 항상 같은 값으로 일치되지 않습니다. 
- 컴퓨터가 2진수(비트)를 통해 숫자를 표현하는 과정에서 생기는 오류이며, 대부분의 경우는 중요하지 않으나 값을 같은지 비교하는 과정에서 문제가 발생

```python
3.5 - 3.12 # A
```

```python
0.3799999999999999 # 결과
```

```python
round(3.5 - 3.12, 2)
```

```python
0.38 # 결과 # B 
```

```python
3.5 - 3.12 == 0.38 # A = B
```

```python
False # 결과
```

=> 처리방법

```python
# 1.
a = 3.5 - 3.12
b = 0.38

abs(a - b) <= 1e-10
```

```python
True # 결과
```

```python
# 2. sys 모듈을 통해 처리
import sys
abs(a - b) <= sys.float_info.epsilon
```

```python
True # 결과
```

```python
# 3. python 3.5부터 활용 가능한 math 모듈
import math
math.isclose(a, b)
```

```python
True # 결과
```

---



```python

```

```python

```

```python

```

```python

```

```python

```



