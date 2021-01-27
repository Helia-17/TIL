# 데이터 구조(Data Structure) II

> ####  알고리즘에 빈번히 활용되는 순서가 없는(unordered) 데이터 구조

<br>

### 세트(Set)

> 변경 가능하고(mutable), 순서가 없고(unordered), 순회 가능한(iterable)

데이터 구조로서의 세트(set)와 조작법(method)

- https://docs.python.org/ko/3/library/stdtypes.html#set-types-set-frozenset

<br>

#### 1. 추가 및 삭제

### `.add(elem)`

elem을 세트에 추가합니다

```python
a = {'사과', '바나나', '수박'}
a.add('파인애플')
print(a) # {'수박', '파인애플', '사과', '바나나'}
```

### `.update(*others)`

여러가지의 값을 추가합니다.
인자로는 반드시 iterable 데이터 구조를 전달해야합니다.

```python
a = {'사과', '바나나', '수박'}
a.update(('파인애플', '애플'))
print(a) # {'수박', '애플', '사과', '바나나', '파인애플'}
```

### `.remove(elem)`

elem을 세트에서 삭제하고, 없으면 KeyError가 발생합니다.

```python
a = {'사과', '바나나', '수박'}
a.remove('사과')
print(a) # {'수박', '바나나'}
a.remove('파인애플') # KeyError
```

### `.discard(elem)`

elem을 세트에서 삭제하고 없어도 에러가 발생하지 않습니다.

```python
a = {'사과', '바나나', '수박'}
a.remove('사과')
a.remove('파인애플') # KeyError
print(a) # {'수박', '바나나'}
```

### `.pop()`

**임의의 원소**를 제거해 반환합니다.
**리스트와 다르게 랜덤**

```python
a = {'사과', '바나나', '수박', '아보카도'}
b = a.pop()
print(a) # {'수박', '바나나', '아보카도'}
print(b) # 사과
```

<br>

### 딕셔너리(Dictionary)

> 변경 가능하고(mutable), 순서가 없고(unordered), 순회 가능한(iterable)
> `Key: Value` 페어(pair)의 자료구조

데이터 구조로서의 딕셔너리(dictionary)와 조작법(method)

- https://docs.python.org/ko/3/library/stdtypes.html#mapping-types-dict

<br>

#### 1. 조회

### `.get(key[, default])`

> key를 통해 value를 가져옵니다.
> 절대로 KeyError가 발생하지 않습니다. default는 기본적으로 None입니다.

```python
my_dict = {'apple': '사과', 'banana': '바나나', 'melon': '멜론'}
my_dict.get('pineapple') # None return
my_dict.get('pineapple', 0) # 0를 return
```



#### 2. 추가 및 삭제

### `.pop(key[, default])`

key가 딕셔너리에 있으면 제거하고 그 값을 돌려줍니다. 그렇지 않으면 default를 반환합니다.
default가 없는 상태에서 딕셔너리에 없으면 KeyError가 발생합니다.

```python
my_dict = {'apple': '사과', 'banana': '바나나'}
print(my_dict.pop('apple')){'banana': '바나나'} # '사과'
print(my_dict) {'banana': '바나나'}
# 딕셔너리에 없으면 에러 발생
my_dict.pop('pine') # Error
# 두번째 인자로 default를 설정할 수 있음
my_dict.pop('pine', 0) # 0
```

### `.update()`

값을 제공하는 key, value로 덮어씁니다.

```python
my_dict = {'apple': '사과', 'banana': '바나나', 'melon': '멜론'}
my_dict.update({'banana': '빠나나'})
my_dict.update(melon='메론')
print(my_dict) # {'apple': '사과', 'banana': '빠나나', 'melon': '메론'}
```

<br>

#### 3. 딕셔너리 순회(반복문 활용)

기본 동작은 key 출력

```python
grades = {'john':  80, 'eric': 90, 'justin': 90}
for student in grades:
    print(student)
# john
# eric
# justin 
```

딕셔너리의 value를 출력

```python
print(grades.keys()) # dict_keys(['john', 'eric', 'justin'])
print(grades.values()) # dict_values([80, 90, 90])
print(grades.items()) # dict_items([('john', 80), ('eric', 90), ('justin', 90)])
```

- dictionary에서 `for`를 활용하는 4가지 방법

```python
# 0. dictionary 순회 (key 활용)
for key in dict:
    print(key)
    print(dict[key])


# 1. `.keys()` 활용
for key in dict.keys():
    print(key)
    print(dict[key])


# 2. `.values()` 활용    
for val in dict.values():
    print(val)


# 3. `.items()` 활용
for key, val in dict.items():
    print(key, val)
```

- 예시 : 혈액형 검사 결과
  혈액형 검사한 결과가 담긴 `blood_types`이 주어졌을때, 해당 딕셔너리를 순회하며, `key`와 `value`를 출력해보세요.

  ```python
  # 1.
  for blood_type in blood_types:
      print(f'{blood_type}형은 {blood_types[blood_type]}명입니다.')
  # 2.
  for blood_type in blood_types.keys():
      print(f'{blood_type}형은 {blood_types[blood_type]}명입니다.')
  # 3.
  for blood_type, number in blood_types.items():
      print(f'{blood_type}형은 {number}명입니다.')
  ```

- 리스트가 주어졌을 때 딕셔너리 구축하기
  리스트가 주어질 때, 각각의 요소의 개수를 value 값으로 갖는 딕셔너리를 만드세요.

```python
# 1
book_title =  ['great', 'expectations', 'the', 'adventures', 'of', 'sherlock', 'holmes', 'the', 'great', 'gasby', 'hamlet', 'adventures', 'of', 'huckleberry', 'fin']
# 문제 발생!! key 있을 때랑 없을때를 나누자!
count = {}
# 단어들을 반복하면서
for word in book_title:
    # 만약에 키가 있으면,
    if word in count.keys():
        # count 딕셔너리에 해당하는 key의 value를 증가시킨다.
        count[word] = count[word] + 1
    # 없으면,
    else:
        count[word] = 1
print(count)
# {'great': 2, 'expectations': 1, 'the': 2, 'adventures': 2, 'of': 2, 'sherlock': 1, 'holmes': 1, 'gasby': 1, 'hamlet': 1, 'huckleberry': 1, 'fin': 1}
```

```python
# 2. get과 default값 사용
book_title =  ['great', 'expectations', 'the', 'adventures', 'of', 'sherlock', 'holmes', 'the', 'great', 'gasby', 'hamlet', 'adventures', 'of', 'huckleberry', 'fin']
# 문제 발생!! key 있을 때랑 없을때를 나누자!
count = {}
# 단어들을 반복하면서
for word in book_title:
    # 가지고 오는데 없으면 0..
    count[word] = count.get(word, 0) + 1
count
```

<br>

### Dictionary comprehension

`iterable`에서 `dict`를 생성할 수 있습니다.

```python
{키: 값 for 요소 in iterable}

dict({키: 값 for 요소 in iterable})
```

- 예시

  ```python
  a = [1, 2, 3]
  {str(n): n for n in a} # {'1': 1, '2': 2, '3': 3}
  ```

  ```python
  cubic = {x: x ** 3 for x in range(1, 8)}
  print(cubic) # {1: 1, 2: 8, 3: 27, 4: 64, 5: 125, 6: 216, 7: 343}
  ```

  ```python
  blood_types = {'A': 40, 'B': 11, 'AB': 4, 'O': 45}
  negative_blood_types = {'-' + key: value for key, value in blood_types.items()}
  # negative_blood_types = {'-' + key: blood_types[key] for key in blood_types}
  print(negative_blood_types) # {'-A': 40, '-B': 11, '-AB': 4, '-O': 45}
  ```

<br>

### Dictionary comprehension + 조건

```python
{키: 값 for 요소 in iterable if 조건식}

{키: 값 if 조건식 else 값 for 요소 in iterable}
```

- 예시

  ```python
  dusts = {'서울': 72, '대전': 82, '구미': 29, '광주': 45, '중국': 200}
  # 미세먼지 농도가 80 초과 지역만 뽑아주세요.
  # 예) {'대전': 82, '중국': 200}
  result = {key: value for key, value in dusts.items() if value > 80}
  # 미세먼지 농도가 80초과는 나쁨 80이하는 보통으로 하는 value를 가지도록 바꾸세요.
  result = {key: '나쁨' if value > 80 else '보통' for key, value in dusts.items()}
  # elif 도 사용할 수 있습니다. (if else 열거)
  result = {key: '매우나쁨' if value > 150 else '나쁨' if value > 80 else '보통' if value > 30 else '좋음' for key, value in dusts.items()}
  ```