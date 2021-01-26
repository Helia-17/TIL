# 데이터 구조(Data Structure) I

데이터 구조(Data Structure)란 데이터에 편리하게 접근하고, 변경하기 위해서 데이터를 저장하거나 조작하는 방법을 말한다.

**Program = Data Structure + Algorithm**

<br>

> ####  알고리즘에 빈번히 활용되는 순서가 있는(ordered) 데이터 구조. 

<br>

### 문자열(String)

> 변경할 수 없고(immutable), 순서가 있고(ordered), 순회 가능한(iterable)

<br>

#### 1. 조회/탐색

###  `.find(x)`

x의 **첫 번째 위치**를 반환합니다. 없으면, `-1`을 반환합니다.

```python
# .find(x) 구현
a = 'apple'
try:
    b = a.index('f')
except:
    b = -1
print(b) # -1
```

### `.index(x)`

x의 **첫번째 위치**를 반환합니다. 없으면, 오류가 발생합니다.

<br>

#### 2. 값 변경

### `.replace(old, new[, count])`

바꿀 대상 글자를 새로운 글자로 바꿔서 반환합니다.
count를 지정하면 해당 갯수만큼만 시행합니다.

```python
'banana'.replace('a', '', 2) #'bnna'
```

### `.strip([chars])`

특정한 문자들을 지정하면, 양쪽을 제거하거나 왼쪽을 제거하거나(lstrip), 오른쪽을 제거합니다(rstrip).
지정하지 않으면 공백을 제거합니다.

- 불필요한 공백을 제거하고 결과를 출력할 때 유용

### `.split()`

문자열을 특정한 단위로 나누어 리스트로 반환합니다.
기본은 공백을 기준으로 반환합니다.

```python
csv = '1,홍길동,01012344567'
# 구분자 지정
csv.split(',') # ['1', '홍길동', '01012344567']

```

### `'separator'.join(iterable)`

특정한 문자열로 만들어 반환합니다.
반복가능한(iterable) 컨테이너의 요소들을 separator를 구분자로 합쳐(`join()`) 문자열로 반환합니다.

- 리스트의 여러 원소를 형식에 맞춰 출력할 때 유용

```python
word = '배고파'
'!'.join(word) # '배!고!파'

words = ['안녕', 'hello']
','.join(words) # '안녕,hello'
```

<br>

#### 3. 문자 변형

### `.capitalize()`, `.title()`, `.upper()`

- `.capitalize()` : 앞글자를 대문자로 만들어 반환한다.
- `.title()` : 어포스트로피나 공백 이후를 대문자로 만들어 반환한다.
- `.upper()` : 모두 대문자로 만들어 반환한다.

### `.lower()`, `.swapcase()`

- `lower()` : 모두 소문자로 만들어 반환한다.
- `swapcase()` : 대 <-> 소문자로 변경하여 반환한다.

<br>

#### 4. 기타 문자열 관련 검증 메소드 : 참/거짓 반환

```py
.isalpha(), .isdecimal(), .isdigit(), .isnumeric(), .isspace(), .isupper(), .istitle(), .islower()
```

<br>

### 리스트(List)

> 변경 가능하고(mutable), 순서가 있고(ordered), 순회 가능한(iterable)

<br>

#### 1. 값 추가 및 삭제

### `.append(x)`

리스트에 값을 추가할 수 있습니다.

### `.extend(iterable)`

리스트에 iterable(list, range, tuple, string**[주의]**) 값을 붙일 수가 있습니다.

### `.insert(i, x)`

정해진 위치 `i`에 값을 추가합니다.

```python
# 가장 맨 앞 넣기
cafe.insert(0, 'hi')
# 가장 맨 뒤 넣기
cafe.insert(-1, 'bye')
# 리스트의 길이를 넘어서는 인덱스는 마지막에 아이템이 추가됩니다.
cafe.insert(len(cafe), '진짜안녕')
```

### `.remove(x)`

리스트에서 값이 x인 것을 삭제합니다.
정해진 위치 `i`에 값을 추가합니다.
값이 없으면 오류가 발생합니다.

### `.pop(i)`

정해진 위치 `i`에 있는 값을 삭제하며, 그 항목을 반환합니다.
`i`가 지정되지 않으면 마지막 항목을 삭제하고 되돌려줍니다.

- 값이 return이 된다는 것은 별도의 변수에 저장할 수 있다는 것. 

### `.clear()`

리스트의 모든 항목을 삭제합니다.

#### 탐색 및 정렬

### `.index(x)`

x 값을 찾아 해당 index 값을 반환합니다.
`.find(x)`와 달리 없을 시 오류가 발생합니다.

### `.count(x)`

원하는 값의 개수를 확인할 수 있습니다.

### `.sort()`

정렬을 합니다.
내장함수 `sorted()` 와는 다르게 **원본 list를 변형**시키고, **`None`**을 리턴합니다.

- **sorted()** 

```python
# 원본 X! 정렬된 값을 반환
sorted(random.sample(range(1, 46), 6))
```

### `.reverse()`

반대로 뒤집습니다. **(정렬 아님)**

```python
classroom = ['Tom', 'David', 'Justin']
classroom.reverse()
print(classroom) # ['Justin', 'David', 'Tom']
```

<br>

#### 리스트 복사

- 문제의식 : 단순 복사로는 id가 같음. 즉 같은 주소를 참조함

  ```python
  original_list = [1, 2, 3]
  copy_list = original_list
  print(copy_list) # [1, 2, 3]
  # 하나에 수정을 가해도 둘 다 변한다
  copy_list[0] = 'A!!'
  print(copy_list, original_list) # ['A!!', 2, 3] ['A!!', 2, 3]
  # id 값 확인해도 같다.
  print(id(copy_list)) # 2757652573760
  print(id(original_list)) # 2757652573760
  ```

##### 일부 상황에만 서로 다른 `얕은 복사(shallow copy)`

##### 1. slice 연산자 사용 `[:]`

```python
a = [1, 2, 3, 4]
# 전체를 똑같이 잘라냄
b = a[:]
```

##### 2. `list()` 활용

```python
a = [1, 2, 3, 4]
# list를 새로운 list로 형변환
b = list(a)
```

- 얕은 복사가 가져오는 잘못된 상황

  ```python
  a = [[1, 2, 3], 2, 3]
  b = list(a) # list() 활용으로 복사
  print(a, b)
  b[0][0] = 100 # b만 변경해도 같이 변경됨
  print(a, b)
  b[1] = '원소' # b만 변경됨
  print(a, b)
  ```

##### 만일 중첩된 상황에서 복사를 하고 싶다면, `깊은 복사(deep copy)`

내부에 있는 모든 객체까지 새롭게 값이 변경된다.

```python
import copy
a = [[1, 2, 3], 2, 3]
b = copy.deepcopy(a)
print(a, b)
b[0][0] = 100
print(a, b)
```

<br>

### List Comprehension

List Comprehension은 표현식과 제어문을 통해 리스트를 생성한다. 
여러 줄의 코드를 한 줄로 줄일 수 있다.

```python
[expression for 변수 in iterable]

list(expression for 변수 in iterable)
```

<br>

- 예시 : 세제곱 리스트
  1~10까지의 숫자로 만든 세제곱 담긴 리스트 `cubic_list`

  ```python
  # 일반 작성
  numbers = range(1, 11)
  cubic_list = []
  for number in numbers:
      cubic_list.append(number ** 3)
  print(cubic_list) # [1, 8, 27, 64, 125, 216, 343, 512, 729, 1000]
  ```

  ```python
  # List comprehension을 활용하여 작성
  [number**3 for number in numbers]
  # [1, 8, 27, 64, 125, 216, 343, 512, 729, 1000]
  ```

<br>

#### List Comprehension + 조건문

조건문에 참인 식으로 리스트를 생성한다.

```python
[expression for 변수 in iterable if 조건식]
[expression if 조건식 else 식 for 변수 in iterable]
```

<br>

- 예시 : 짝수리스트
  1~10까지의 숫자중 짝수만 담긴 리스트 `even_list`
  여러개의 `for` 혹은 `if`문을 중첩적으로 사용 가능한다.

  ```python
  # 일반 작성
  even_list = []
  for i in range(1, 11):
      if i % 2 == 0:
          even_list.append(i)
  print(even_list) # [2, 4, 6, 8, 10]
  ```

  ```python
  # List comprehension을 활용하여 작성
  print([i for i in range(1, 11) if i % 2 == 0])
  # [2, 4, 6, 8, 10]
  ```

- 예시 : 홀짝

  ```python
  # 홀수는 음수, 짝수는 양수
  n = 3
  '홀수' if n % 2 == 1 else '짝수'  # 조건표현식
  # '홀수'
  ```

  ```python
  # 조건 표현식
  ['홀수' if i % 2 == 1 else '짝수' for i in range(1, 11)]
  # i 순서 : 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
  # ['홀수', '짝수', '홀수', '짝수', '홀수', '짝수', '홀수', '짝수', '홀수', '짝수']
  ```

  ```python
  # 뒤에 조건식에는 else 사용 불가
  ['홀수' for i in range(1, 11) if i % 2 == 1 else '짝수'] # Error
  #    File "<ipython-input-128-ebc603da097f>", line 2
  #     ['홀수' for i in range(1, 11) if i % 2 == 1 else '짝수']
  #                                              ^
  # SyntaxError: invalid syntax
  ```

- 예시 : 곱집합
  주어진 두 list의 가능한 모든 조합을 담은 `pair` 리스트를 작성하세요.

  ```python
  # 입력 예시
  girls = ['jane', 'ashley', 'mary']
  boys = ['justin', 'eric', 'david']
  # 출력 예시
  [('justin', 'jane'), ('justin', 'ashley'), ('justin', 'mary'), ('eric', 'jane'), ('eric', 'ashley'), ('eric', 'mary'), ('david', 'jane'), ('david', 'ashley'), ('david', 'mary')]
  ```

  ```python
  # 일반 작성
  pair = []
  for boy in boys:
      for girl in girls:
          pair.append((boy, girl))
  ```

  ```python
  # List comprehension
  pair = [(boy, girl) for boy in boys for girl in girls]
  ```

- 예시 : 피타고라스 정리
  주어진 조건(x < y < z < 50) 내에서 피타고라스 방정식의 해를 찾으세요.

  ```python
  # 출력 예시
  [(3, 4, 5), (5, 12, 13), (6, 8, 10), (7, 24, 25), (8, 15, 17), (9, 12, 15), (9, 40, 41), (10, 24, 26), (12, 16, 20), (12, 35, 37), (15, 20, 25), (15, 36, 39), (16, 30, 34), (18, 24, 30), (20, 21, 29), (21, 28, 35), (24, 32, 40), (27, 36, 45)]
  ```

  ```python
  # 일반 작성
  result = []
  for x in range(1, 50):
      for y in range(x, 50):
          for z in range(y, 50):
              if x**2 + y**2 == z**2:
                  result.append((x, y, z))
  ```

  ```python
  # List comprehension
  result = [(x, y, z) for x in range(1, 50) for y in range(x, 50) for z in range(y, 50) if x**2 + y**2 == z**2]
  ```

  <br>

> ####  데이터 구조에 적용 가능한 Built-in Function
>
> 순회 가능한(iterable) 데이터 구조에 적용가능한 Built-in Function
> iterable 타입 - `list`, `dict`, `set`, `str`, `bytes`, `tuple`, `range`

### `map(function, iterable)`

순회가능한 데이터 구조(iterable)의 모든 요소에 function을 적용한 후 그 결과를 돌려준다.
return은 `map_object` 형태이다.

- `map()` 함수는 입력값을 처리할 때 자주 활용

### `filter(function, iterable)`

iterable에서 function의 반환된 결과가 `True` 인 것들만 구성하여 반환한다.
`filter object` 를 반환한다.

```python
# 특정 list에서 홀수만을 걸러내는 코드
def odd(n):
    return n % 2
numbers = [1, 2, 3]
new_numbers = list(filter(odd, numbers))
```

### `zip(*iterables)`

복수의 iterable 객체를 모아(`zip()`)준다.
결과는 튜플의 모음으로 구성된 `zip object` 를 반환한다

```python
girls = ['jane', 'ashley', 'mary']
boys = ['justin', 'eric', 'david']
# zip() 활용하여 짝을 맞추어 본다.
pair = list(zip(girls, boys))
print(pair)
# [('jane', 'justin'), ('ashley', 'eric'), ('mary', 'david')]
```

<br>

*****

- **Niklaus Wirth**