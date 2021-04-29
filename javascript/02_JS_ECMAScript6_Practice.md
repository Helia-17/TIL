[TOC]

# 연습 - 변수

확인은 개발자도구 - Console에서 가능

<br>

```javascript
/*
  [let 키워드 연습]
  
  1. let 키워드를 이용하여 city 변수를 작성하세요.
  2. city 변수에 '제주도'를 할당하세요.
  3. city 변수의 값을 현재 여러분의 지역으로 재할당하세요.
*/
let city = '제주도'
city = '서울'
```

```javascript
/*
  [const 키워드 연습]
  
  1. const 키워드를 이용하여 phone 변수를 작성하세요.
  2. phone 변수에 'Galaxy S2'을 할당하세요.
  3. phone 변수의 값을 현재 여러분의 핸드폰 기종을 재할당하세요.
  4. 재할당 에러를 확인하세요.
*/
const phone = 'Galaxy S2'
phone = 'Galaxy Note 10'

// const로 작성된 변수는 재할당이 불가능하지만
// Object, list 등의 데이터의 내부를 수정하는 것은 가능하다
const userInfo = {
  'name': 'Helia'
}
userInfo.name = 'Tony'
```

```javascript
/*
  [블록 스코프 - let 예시]
  
  아래 코드 실행 후 결과를 확인해보세요.
*/

let fullName = 'Brendan Eich'

if (fullName === 'Brendan Eich') {
  let fullName = 'Guido Van Rossum'
  console.log('블록 스코프:', fullName)
}

console.log('전역 스코프:', fullName)
```

- if문 안은 안의 fullName을 참조, 바깥은  바깥의 상단에 있는 fullName을 참조

```javascript
/*
  [블록 스코프 - const 예시]
  
  아래 코드 실행 후 결과를 확인해보세요.
*/

let fullName = 'Brendan Eich'

if (fullName === 'Brendan Eich') {
  let fullName = 'Guido Van Rossum'
  const language = 'Python'
}

console.log(language) // 안에 있는 language을 밖에서 참조할 수없음
```

```javascript
/*
  [var 키워드 연습]
  
  1. var 키워드를 이용하여 framework 변수를 작성하세요.
  2. framework 변수에 'Bootstrap'를 할당하세요.
  3. framework 변수에 'Django'를 재할당하세요.
  4. framework 변수를 재선언하고 'Vue'를 할당하세요.
*/
var framework
framework = 'Bootstrap'
framework = 'Django' // 문제 없이 동작
var framework = 'Vue' // 문제 없이 동작
```

```javascript
/*
  [함수 스코프 - var 키워드 예시]
  
  아래 코드 실행 후 결과를 확인해보세요.
*/

function f1() {
  var message = 'You are doing great!'
}
console.log(message)
// => Uncaught ReferenceError: message is not defined
```

- 함수 내에 있는 var을 참조 불가

```javascript
/*
  [블록 스코프 - var 키워드 예시]

  Tip.
    if문은 블록 스코프를 생성합니다.
  
  아래 코드 실행 후 결과를 확인해보세요.
*/

const codeEditor = 'vscode'

if (codeEditor === 'vscode') {
  var theme = 'dark+'
}
console.log(theme) // 문제 없이 동작
```

- 함수 안이 아니라면 var은 어디든 참조 가능

```javascript
/*
  [블록 스코프 - const, let 키워드 예시]
  
  Tip. 
    const와 let은 블록 스코프입니다.
    함수의 중괄호도 블록에 해당됩니다.
  
  아래 코드 실행 후 결과를 확인해보세요.
*/

function f2() {
  const stack = 'Last In, First Out'
}
console.log(stack)

function f3() {
  let queue = 'First In, First Out'
}
console.log(queue)
// => Uncaught ReferenceError: stack is not defined
```

```javascript
/*
  [호이스팅(hoisting)]
  
  아래 코드 실행 후 결과를 확인해보세요.
  그리고 const와 let의 경우와 비교해보세요.
*/

console.log(hoisted)
var hoisted = 'can you see me?'

console.log(lunch)
const lunch = '초밥'
// => Uncaught ReferenceError: Cannot access 'lunch' before initialization

console.log(dinner)
let dinner = '스테이크' 
// => Uncaught ReferenceError: dinner is not defined
```

<br>

---

<br>

# 연습 - 타입과 연산자

```javascript
/*
  [Number 타입 연습]

  - hour 변수에 현재 시간의 "시(hour)를 초(second)로 바꿔서" 저장하세요.
  - minute 변수에 현재 시간의 "분(minute)을 초(second)로 바꿔서" 저장하세요. 
  - curTime 변수에 hour와 minute의 합을 저장 후 출력해보세요.
*/
let hour = 10 * 60 * 60
let minute = 29 * 60
let curTime = hour + minute
console.log(curTime)
```

```javascript
/*
  [String 타입 연습]

  - username 변수에 여러분의 이름을 입력하세요.
  - message 변수에 인사말을 작성하세요.
  - username 변수에 greeting을 할당 연산자로 이어붙인 후 출력해보세요. 
*/
let username = 'Helia'
let message = 'hello'
console.log(username + message)
// console.log(`${username} ${message}`)
```

```javascript
/*
  [String 타입 연습]

  템플릿 리터럴(Template Literal) 활용

  - viewCnt 변수를 활용하여 예시와 같은 문장을 만들어보세요.
  - 예시) 조회수 500회
*/

const viewCnt = 500
console.log(`조회수 ${viewCnt}회`)
```

```javascript
/*
  [undefined vs. null]

  Tip.
    - undefined는 변수 선언 시 값을 할당하지 않을 때 할당되는 값입니다.
    - null은 개발자가 의도적으로 값이 없음을 표현할 때 할당하는 값입니다. 

  아래 코드 실행 후 결과를 확인해보세요.
*/

let unknown
console.log(unknown) // undefined

const nullValue = null 
console.log(nullValue) // null
console.log(typeof nullValue) // object
```

```javascript
/*
  [Boolean 타입 연습]

  Tip.
    파이썬과 다르게 자바스크립트의 Boolean 타입은 
    첫 단어가 소문자임에 주의하세요.

  - isLoggedIn 변수에 false를 할당하세요.
  - isLoggedIn 변수의 값을 true로 바꾸고 출력해보세요.
*/
let isLoggedIn = false
isLoggedIn = true
console.log(isLoggedIn)
```

```javascript
/*
  [삼항(Ternary) 연산자 연습]
  
  Tip.
    condition ? expression if true : expression if false

  아래의 조건을 만족하는 삼항 연산자를 작성해보세요.
  - 조건문에서 subscribed 변수의 참/거짓 여부를 판별합니다.
  - 조건이 참이면 '구독취소'를 반환합니다.
  - 조건이 거짓이면 '구독중'을 반환합니다.
  - 삼항 연산자의 반환값을 message 변수에 할당 후 출력합니다.
*/

const subscribed = false

let message = subscribed ? '구독취소' : '구독중'
console.log(message) // 구독중
```

<br>

---

<br>

# 연습 - 조건문과 반복문

```javascript
/*
  [if문 연습]
  
  username 변수의 값에 따라 다른 메세지를 출력하세요.
  - 관리자(admin)일 경우 "관리자님 환영합니다."
  - 매니저(manager)일 경우 "매니저님 환영합니다."
  - 그 외 모든 경우 "{username}님 환영합니다"
*/

const username = 'admin'
if (username === 'admin') {
  console.log("관리자님 환영합니다")
} else if (username === 'manager') {
  console.log("매니저님 환영합니다")
} else {
  console.log(`${username}님 환영합니다`)
}
```

```javascript
/*
  [switch문 연습]

  operator 변수의 값에 따라 다른 계산을 하는 조건을 작성하세요.
  - '+'는 두 숫자의 합을 출력합니다.
  - '-'는 두 숫자의 차이를 출력합니다.
  - '*'는 두 숫자의 곲을 출력합니다.
  - '/'는 두 숫자의 나눗셈 결과를 출력합니다.
  - 만약 위 4가지 경우에 해당하지 않는 operator라면,
    "유효하지 않은 연산자입니다."라는 메세지를 출력하세요.
*/

const numOne = 10
const numTwo = 100
const operator = '+'

switch (operator) {
  case '+': {
    console.log(numOne + numTwo)
    break
  }
  case '-' {
    console.log(numOne - numTwo)
    break
  }
}
```

```javascript
/*
  [while문 연습]
  
  아래의 조건을 만족하는 while문을 작성하세요.
  - 주어진 변수 evenNumber를 2씩 증가시키고, 해당 값을 출력합니다.
  - evenNumber가 6이 되면 반복문을 종료합니다.
*/

let evenNumber = 0

while (evenNumber < 6) {
  console.log(evenNumber)
  evenNumber += 2
}
```

```javascript
/*
  [for문 연습]
  
  아래의 조건을 만족하는 for문을 작성하세요.
  - oddNumber라는 이름의 변수를 선언 및 1로 초기화합니다.
  - 매 시행마다 oddNumber를 2씩 증가시키고, 해당 값을 출력합니다.
  - oddNumber가 5가 되면 반복문을 종료합니다.
*/

for (let oddNumber = 1; oddNumber < 5; oddNumber + =2) {
  console.log(oddNumber) // 1, 3
}
```

```javascript
/*
  [for... in 연습]

  Tip.
    JS 객체의 value는 점(.) 또는 대괄호 표기법을 이용하여 
    key값을 통해 접근 가능합니다. ex) obj.key, obj[key]
  
  - 주어진 객체를 순회하면서 예시와 같이 출력합니다.
  - 예시) title: '벤자민 버튼의 시간은 거꾸로 간다'
*/

const bestMovie = {
  title: '벤자민 버튼의 시간은 거꾸로 간다',
  releaseYear: 2008,
  actors: ['브래드 피트', '케이트 블란쳇'],
  genres: ['romance', 'fantasy'],
}

for (let value in bestMovie) {
 console.log(`${value}`)
} // key값만 뜸

for (let key in bestMovie) {
  console.log(`${key} ${bestMovie[key]}`)
} // key-value
```

```javascript
/*
  [for... of 연습]
  
  Tip.
    JS 객체의 value는 점(.) 또는 대괄호 표기법을 이용하여
    key값을 통해 접근 가능합니다. ex) obj.key, obj[key]

  - 주어진 배열을 순회하면서 예시와 같이 출력합니다.
  - 예시) title: '어바웃 타임'
*/

const movies = [
  {title: '어바웃 타임'},
  {title: '굿 윌 헌팅'},
  {title: '인턴'},
]

for (let movie in movies) {
  console.log(movie)
}
```



<br>

---

<br>

# 연습 - 함수

```javascript
/*
	[함수 선언식 연습]
	
	인자의 길이에 따라 true 혹은 false를 반환하는 함수 `isValid`를 작성하세요.
	- `password` 인자의 값의 길이가 8 미만이면 false를 반환합니다.
	- `password` 인자의 값의 길이가 8 이상이면 true를 반환합니다.
	- 함수는 선언식으로 작성합니다.
	- 예시) isValid('abcd')  // false
*/
function isValid(password) {
	if(password.length >= 8){
		 return true 
	}
	else{
		 return false
	}
}

function isValid(password) {
	return password.length >= 8 ? true : false
}

let isValid(password) {
	return password.length >= 8
}

function isValid(password) {
	return password.length >= 8
}
let isValid = function (password) {
	return password.length >= 8
}
let isValid = password => password.length >= 8 // 생략 가능
```

```javascript
/*
	[함수 표현식 연습]
	
	문자열로 구성된 배열을 특정 문자를 기준으로 하나의 문자열로 합치는 함수 `join`을 작성하세요.
	- 첫번째 인자 `array`는 문자열로 구성된 배열입니다.
	- 두번째 인자 `separator`는 문자열입니다.
	- 함수는 표현식으로 작성합니다.
	- 예시) join(['010', '1234', '5678'], '-')  // '010-1234-5678'
*/

// 함수 표현식
const join = function (numbers, seperator) {
	let result = ''

	for (let i = 0; i < numbers.length; i++) { // for _ in range(len(A))
		const number = numbers[i]
		result += number

		if (i < numbers.length-1) {result += seperator}
	}
	return result
}

// 화살표 함수
const join = (numbers, seperator) => {
	let result = ''

	for (let i = 0; i < numbers.length; i++ ) {
		const number = numbers[i]
		result += number

		if (i<numbers.length-1) {result += seperator}
	}
	return result
}
```

```javascript
/*
	[함수 기본인자 연습]
	
	주문을 받아서 주문서를 반환하는 함수 `makeOrder`를 작성하세요.
	- 첫번째 인자 `menu`는 문자열입니다.
	- 두번째 인자 `size`는 문자열이며, 기본인자는 'regular'입니다.
	- 함수는 각 인자를 속성으로 갖는 객체를 반환합니다.
	
	예시) makeOrder('mocha') // { menu: 'mocha', size: 'regular' }
*/
const makeOrder = function (menu, size=regular) {
	return { menu: menu, size: size }
}

const makeOrder = (menu, size='regular') => ({ menu: menu, size: size })
```

```javascript
/*
	[화살표 함수 연습]
	
	- 아래 celsiusToFahrenheit 함수는 섭씨 온도를 화씨 온도로 바꾸는 함수입니다. 
  - 선언식으로 작성된 함수를 "화살표 함수"로 다시 작성해보세요.

  function celsiusToFahrenheit (celsius) {
		const fahrenheit = celsius * 9/5 + 32
		return fahrenheit
	}

*/
const celsiusToFahrenheit = (celsius) => {return (celsius * 9/5 + 32)}
const celsiusToFahrenheit = celsius => (celsius * 9/5 + 32)
// celsiusToFahrenheit(20)
```

<br>

---

<br>

# 연습 - 배열(arrays)

```javascript
/*
	[배열 관련 주요 메서드 연습 1]
	
	주어진 배열의 요소 중 null 값을 제거한 새로운 배열을 만드세요.
*/

const homeworks = ['david.zip', null, 'maria.zip', 'tom.zip', null]
const result = []
for (let homework of homworks) {
	if (homework) { // True라면 push
		result.push(homework)
	}
}
console.log(result)
```

```javascript
/*
	[배열 관련 주요 메서드 연습 2]
	
	주어진 배열을 사용하여 아래 문자열을 완성하세요.

	'www.samsung.com/sec/buds/galaxy-buds-pro'

*/

const arr1 = ['www', 'samsung', 'com']
const arr2 = ['galaxy', 'buds', 'pro']
const arr3 = ['sec', 'buds']

const url = arr1.join('.') + '/' + arr3.join('/') + arr2.join('-')
console.log(url)

const url = arr.join('.')
const product = arr2.join('-')
arr3.unshift(url)
arr.push(product)
console.log(arr3.join('/'))
```

```javascript
/*
	[배열 관련 주요 메서드 연습 3]

	주어진 배열의 요소 중 모든 'rainy' 요소를 'sunny'로 교체하세요
	- indexOf 메서드를 사용합니다.
*/

const weather = ['sunny', 'sunny', 'sunny', 'sunny', 'rainy', 'rainy', 'sunny']

while (weather.indexOf('rainy') > 0) { // 있으면 그 인덱스가 나와서 True, 없으면 -1이 나와서 False. 
	const index = weather.indexOf('rainy')
	weather[index] = 'sunny'
}
console.log(weather)
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 1]
 
 속력(distance/time)을 저장하는 배열 speeds를 만드세요.
*/

const trips = [
  { distance: 34, time: 10 },
  { distance: 90, time: 50 },
  { distance: 59, time: 25 },
]

const speeds = trips.map((trip) => trip.distance / trip.time)
console.log(speeds)
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 2]
 
 주어진 배열의 요소 중 특정 문자(query)가 포함되는 요소만 모아서 새로운 배열을 반환하세요.
*/

const languages = ['python', 'javascript', 'html', 'java']
const query = 'java'

// 애매한 풀이
const javas = languages.filter((language) => {
  if (language.includes(query)) {
    return language
  }
})
console.log(javas)

// 명쾌한 풀이
const result = languages.filter(function(lang){
  return lang.includes(query)
})
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 3]
 
 주어진 배열을 사용하여 다음과 같은 객체를 만드세요.
 {
   smith: 90,
   peter: 80,
   anna: 85,
 }
*/

const scores = [
  { name: 'smith', score: 90 },
  { name: 'peter', score: 80 },
  { name: 'anna', score: 85 },
]

const result = scores.reduce((acc, score)=>{
  acc[score.name] = score.score // 다 기록후
  return acc // 반환된 acc를 result 변수에 저장
}, {})
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 4]
 
 주어진 accounts 배열에서 balance가 24,000인 사람을 찾으세요.
*/

const accounts = [
	{ name: 'justin', balance: 1200 },
	{ name: 'harry', balance: 50000 },
	{ name: 'jason', balance: 24000 },
]

const person = accounts.find((account) => account.balance === 24000) // 같은게 있다면 첫번째 요소 반환
console.log(person)
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 5]
 
 주어진 requests 배열에서 status가 pending인 요청이 있는지 확인하세요.
*/

const requests = [
  { url: '/photos', status: 'complete' },
  { url: '/albums', status: 'pending' },
  { url: '/users', status: 'failed' },
]

const check = requests.some((request) => request.status === 'pending')
console.log(check)
```

```javascript
/*
 [배열 관련 주요 메서드 연습 심화 6]
 
 주어진 users 배열을 통해 모든 유저의 상태가 submmited인지 여부를 확인하세요.
*/

const users = [
  { name: 'Harry', submitted: true },
  { name: 'Eric', submitted: true },
  { name: 'Tony', submitted: false },
]

const check = users.some((user) => user.submitted === 'true')
console.log(check)
```

<br>

---

<br>

# 객체(object)

```javascript
// object 만들기
const userInfo = {
  name: 'Helia',
  location: 'Seoul',
  device: ['phone', 'watch', 'pad'], // 배열 가능
  language: {
    python: 1,
    js: 2,
    java: 3,
  }, // object 가능
  hello: function(){ console.log('hello')}, //함수도 가능. 함수를 보려면 hello, 실행시키려면 hello()
  hi(){console.log('hi')}
}

userInfo.name = 'asdf' // 값 변경 가능
```

```javascript
/*
  [Object 요소 접근 연습]
  
	주어진 객체에서 items의 첫번째 아이템의 name을 result 변수에 할당하세요.
*/

const data = {
  id: 42,
  items: [
    {
      id: 1,
      name: 'foo',
    },
    {
      id: 2,
      name: 'bar',
    },
  ],
}

const result = data.items[0].name
```

```javascript
/*
[Object 축약 문법]

아래 변수들을 속성으로 가지는 Object를 축약문법을 활용하여 작성하세요.
*/

const username = 'hailey'
const contact = '010-1234-5678'

const user = {
  username, // username: username
  contact// contact: contact
}
```

```javascript
/*
[Object Destructuring]

주어진 함수를 Object 축약 문법과, destructuring을 사용하여 재작성하세요.
*/

const users = [
  {
    name: 'hailey',
    contact: '010-1234-5678',
  },
  {
    name: 'paul',
    contact: '010-5678-1234',
  },
]

function saveUserData (users) {
  const userData = users.map((user, index) => {
    return { id: index, name: user.name, contact: user.contact }
  })

  return userData
}

function saveUserData(users) {
  return users.map(({name, contact}, index)=>{
    return {
      id: index,
      name,
      contact
    }
  })
}
```

- 두개의 인자를 각각 {name, contact} 이런식으로 묶을 수 있다. 풀어서 가져와준다.