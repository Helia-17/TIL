# 컨테이너**(Container)**

:여러 개의 값을 저장할 수 있는 객체



파이썬 자료형의 구분 : 숫자형 (Int, float, complex) / 시퀀스형



## 구분 1. 

## 시퀀스(Sequence)형 vs 비시퀀스(Non-sequence)형

> 시퀀스(Sequence)형: 순서가 있는(ordered) 데이터
> 비 시퀀스(Non-sequence)형: 순서가 없는(unordered) 데이터



> #### 시퀀스(Sequence)형: 순서가 있는(ordered) 데이터
>
> 1. 순서를 가질 수 있다.
> 2. **특정 위치의 데이터를 가리킬 수 있다.**(index)
>
> - **리스트(list), 튜플(tuple), 레인지(range), *문자형(string)*,** *바이너리(binary)*



### list [a, b]

- `[value1, value2, value3]`
- 생성 : 대괄호`[]` 및 `list()`
- 값에 대한 접근 : `list[i]`
- 값 변경 : `list[0] = '변경하고 싶은 값'`

- mutable(변경 가능한) 값의 시퀀스

- TIP✨

  - list로 `a += b`의 형태를 만들고 싶다면

    ```python
    list_a = [] # 빈 리스트 변수 선언
    list_b = ['variable elements']
    list_a += list_b # [] += list_b -> X, 0 += list_b -> X
    ```



### Tuple (a, b)

- `(value1, value2)`

- immutable(변경 불가능한) 값의 시퀀스 : 읽을 수 밖에 없음
- 생성 : `my_tuple = (1, 2)` or `another_tuple = 1, 2`(괄호 생략 가능)

🐣**하나의 원소만 넣어서 그냥 생성할 수 없음 -> 값 뒤에 쉼표 필요**

- ```python
  tuple1 = ('hello')
  type(tuple1) # str
  single_tuple = ('hello',)
  print(type(single_tuple)) # tuple
  ```

- TIP✨

  - 활용

    ```python
    x, y = 1, 2
    print(x, y)
    # 결과
    1 2 # <- 실제로는 tuple로 처리됨
    ```

    SWAP

    ```python
    x = 1
    y = 100
    x, y = y, x
    ```

    빈 튜플 : `empty = ()`



### range

- 숫자의 시퀀스

  - `print(range(n)) -> range(0,n)`이라 list, for문의 조합과 함께 쓰임

- 생성
  기본형 : `range(n)`

  > 0부터 n-1까지 값을 가짐

  범위 지정 : `range(n, m)`

  > n부터 m-1까지 값을 가짐

  범위 및 스텝 지정 : `range(n, m, s)`

  > n부터 m-1까지 +s만큼 증가한다



**시퀀스에서 활용할 수 있는 연산자/함수 **

|       operation |                             설명 |
| --------------: | -------------------------------: |
|        x `in` s |      containment test(들어있니?) |
|    x `not in` s | containment test(들어있지 않니?) |
|       s1 `+` s2 |        concatenation(연결, 연쇄) |
|         s `*` n |          n번만큼 반복하여 더하기 |
| operation`s[i]` |                     설명indexing |
|        `s[i:j]` |          slicing : i 초과 j 미만 |
|      `s[i:j:k`] |                k간격으로 slicing |
|          len(s) |                             길이 |
|          min(s) |                           최솟값 |
|          max(s) |                           최댓값 |
|      s.count(x) |                         x의 개수 |

```python
# x in s
## 문자열
s = 'string'
print('a' in s) # False
## 숫자열
l = [1, 2, 3, 5, 1]
print(3 in l) # True
```

```python
# concatenation
print('안녕,' + '하세요') # 안녕,하세요
print((1, 2) + (5, 6)) # (1, 2, 5, 6)
print([1, 2] + [5, 6]) # [1, 2, 5, 6]
```

```python
# *
[0] * 7 # [0, 0, 0, 0, 0, 0]
['쀼'] * 17 
# ['쀼',
# ...
# '쀼'] # 자동 줄바꿈
```

```python
# slicing
list[1:3] # []의 형태로 출력
string[1:3] # tr
tuple[1:3] # ()의 형태로 출력
```

```python
# 간격 slicing
sample_list = list(range(0, 31))
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30]

# 0(첫번째 값)이상 전체길이만큼 / 
# 3씩 증가시켜서 slicing
sample_list[0:len(sample_list):3]
```



> ####  비 시퀀스(Non-sequence)형: 순서가 없는(unordered) 데이터

### set

- 서로 다른(distinct) 값의 집합(collection)

### dict

- key/value의 집함(collection)



> ### 생각해 볼 수 있는 조합

```python
# list에 range를 이용해 숫자 넣기
list(range(3)) # [0, 1, 2]
```

```python
# list에 range원소 넣기
[range(3)] = [range(0, 3)]
```





> ### 알아두기

**List)ordered !== soreted**

- ordered : 순서대로 나열되었다
  sorted : 정렬되었다
  - 시퀀스형 컨테이너 :  데이터가 순서대로 `나열된(ordered) 것`이지 `정렬되었다(sorted)`라는 뜻은 아니다.

**Range)에 음수를 넣기**

```python
list(range(0, -10)) # []
list(range(0, -10, -1)) # [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
```



