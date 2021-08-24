[toc]

# React

## useRef 로 특정 DOM 선택하기

- javascript에서 특정 Dom을 선택하는 역할 ex) getElementById, querySelector
- 특정 DOM에 접근할 때 사용한다.
- 외부 라이브러리 사용할때 유용하다. (특정 DOM에다 적용)
  - Video.js, JWPlayer 같은 HTML5 Video 관련 라이브러리
  - D3, chart.js 같은 그래프 관련 라이브러리
- 원하는 위치에 ref={} 의 형태로 작성하면 된다.
- 포커스를 잡으려면 nameInput.current.focus() 형태로 작성하면 된다.



- 함수형 컴포넌트에서 `ref` 를 사용 할 때에는 `useRef` 라는 Hook 함수

- 클래스형 컴포넌트에서는 콜백 함수를 사용하거나 `React.createRef` 라는 함수

- inputSample.js

  - 초기화 버튼을 클릭했을 때 이름 input 에 포커스가 잡히도록 `useRef` 를 사용

  ```javascript
  import React, { useState, useRef } from 'react';
  
  function InputSample() {
    const [inputs, setInputs] = useState({
      name: '',
      nickname: ''
    });
    // useRef() 를 사용하여 Ref 객체를 만들고, 이 객체를 우리가 선택하고 싶은 DOM 에 ref 값으로 설정
    const nameInput = useRef();
  
    const { name, nickname } = inputs; // 비구조화 할당을 통해 값 추출
  
    const onChange = e => {
      const { value, name } = e.target; // 우선 e.target 에서 name 과 value 를 추출
      setInputs({
        ...inputs, // 기존의 input 객체를 복사한 뒤
        [name]: value // name 키를 가진 값을 value 로 설정
      });
    };
  
    const onReset = () => {
      setInputs({
        name: '',
        nickname: ''
      });
      // Ref 객체의 .current 값은 우리가 원하는 DOM을 가리킴
      // onReset 함수에서 input 에 포커스를 하는 focus() DOM API 를 호출
      nameInput.current.focus();
    };
  
    return (
      <div>
        <input
          name="name"
          placeholder="이름"
          onChange={onChange}
          value={name}
          ref={nameInput}
        />
        <input
          name="nickname"
          placeholder="닉네임"
          onChange={onChange}
          value={nickname}
        />
        <button onClick={onReset}>초기화</button>
        <div>
          <b>값: </b>
          {name} ({nickname})
        </div>
      </div>
    );
  }
  
  export default InputSample;
  ```

<br>

---

<br>

## 배열 렌더링하기

```javascript
const users = [
  {
    id: 1,
    username: 'velopert',
    email: 'public.velopert@gmail.com'
  },
  {
    id: 2,
    username: 'tester',
    email: 'tester@example.com'
  },
  {
    id: 3,
    username: 'liz',
    email: 'liz@example.com'
  }
];
```

이 내용을 컴포넌트로 렌더링한다면?

1. 그냥 그대로 코드를 작성하는 것

   - 가장 기본적인 방법이지만 비효율적인 방법

   - src/UserList.js

   ```javascript
   import React from 'react';
   
   function UserList() {
     const users = [
       {
         id: 1,
         username: 'velopert',
         email: 'public.velopert@gmail.com'
       },
       {
         id: 2,
         username: 'tester',
         email: 'tester@example.com'
       },
       {
         id: 3,
         username: 'liz',
         email: 'liz@example.com'
       }
     ];
     return (
       <div>
         <div>
           <b>{users[0].username}</b> <span>({users[0].email})</span>
         </div>
         <div>
           <b>{users[1].username}</b> <span>({users[1].email})</span>
         </div>
         <div>
           <b>{users[2].username}</b> <span>({users[1].email})</span>
         </div>
       </div>
     );
   }
   
   export default UserList;
   ```

   - 재사용되는 코드를 일일히 넣는게 별로 좋지 않음

2. 컴포넌트를 재사용

   - 한 파일에 여러개의 컴포넌트를 선언해도 괜찮음

   - src/UserList.js

   ```javascript
   import React from 'react';
   
   // 재사용하기 위한 컴포넌트
   function User({ user }) {
     return (
       <div>
         <b>{user.username}</b> <span>({user.email})</span>
       </div>
     );
   }
   
   function UserList() {
     const users = [
       {
         id: 1,
         username: 'velopert',
         email: 'public.velopert@gmail.com'
       },
       {
         id: 2,
         username: 'tester',
         email: 'tester@example.com'
       },
       {
         id: 3,
         username: 'liz',
         email: 'liz@example.com'
       }
     ];
   
     return (
       <div>
         <User user={users[0]} />
         <User user={users[1]} />
         <User user={users[2]} />
       </div>
     );
   }
   
   export default UserList;
   ```

   - 배열의 인덱스를 하나하나 조회해가면서 렌더링하는 방법은 동적인 배열을 렌더링하지 못함

### 동적인 배열을 렌더링

- 자바스크립트 배열의 내장함수 `map()` 을 사용

  - 배열안에 있는 각 원소를 변환하여 새로운 배열을 만들어줌

- 이 함수를 사용하여 일반 데이터 배열을 리액트 엘리먼트로 이루어진 배열로 변환

- UserList.js

  ```javascript
  import React from 'react';
  
  function User({ user }) {
    return (
      <div>
        <b>{user.username}</b> <span>({user.email})</span>
      </div>
    );
  }
  
  function UserList() {
    const users = [
      {
        id: 1,
        username: 'velopert',
        email: 'public.velopert@gmail.com'
      },
      {
        id: 2,
        username: 'tester',
        email: 'tester@example.com'
      },
      {
        id: 3,
        username: 'liz',
        email: 'liz@example.com'
      }
    ];
  
    return (
      <div>
        {users.map(user => (
          <User user={user} /> // 여기가 수정될 예정
        ))}
      </div>
    );
  }
  
  export default UserList;
  ```

  - 하지만 이렇게하면 에러가 뜸
  - 리액트에서 배열을 렌더링 할 때에는 `key` 라는 props 를 설정해야 함
    - `key` 값은 각 원소들마다 가지고 있는 고유값
    - 이 경우엔 `id`값

  ```jsx
      <div>
        {users.map(user => (
          <User user={user} key={user.id} />
        ))}
      </div>
  ```

  - 만약 배열 안의 원소가 가지고 있는 고유한 값이 없다면 `map()` 함수를 사용 할 때 설정하는 콜백함수의 두번째 파라미터 `index` 를 `key` 로 사용

  ```jsx
      <div>
        {users.map((user, index) => (
          <User user={user} key={index} />
        ))}
      </div>
  ```

### Map에서 Key가 필요한 이유

> Map에 key 값이없다면 중간의 값이 바뀌었을때 그 하위 값들이 전부 변하기 때문인다. key값을 사용한다면 key를 이용해 중간의 값을 추가하게 된다.

- key가 없는 배열

  이 배열을

  ```javascript
  const array = ['a', 'b', 'c', 'd'];
  ```

  이와 같이 렌더링한다면

  ```react
  array.map(item => <div>{item}</div>);
  ```

  위 배열의 b 와 c 사이에 z 를 삽입하여 리렌더링할 때

  - 기존의 c 가 z 로바뀌고, d 는 c 로 바뀌고, 맨 마지막에 d 가 새로 삽입

  a 를 제거한다면

  - 기존의 a 가 b 로 바뀌고, b 는 z 로 바뀌고, z는 c로 바뀌고, c는 d 로바뀌고, 맨 마지막에 있는 d 가 제거\

  => 매우 비효율적이므로 `key`가 필요

- key가 있는 배열

  ```javascript
  [
    {
      id: 0,
      text: 'a'
    },
    {
      id: 1,
      text: 'b'
    },
    {
      id: 2,
      text: 'c'
    },
    {
      id: 3,
      text: 'd'
    }
  ];
  ```

  렌더링

  ```jsx
  array.map(item => <div key={item.id}>{item.text}</div>);
  ```

  => 수정되지 않는 기존의 값은 그대로 두고 원하는 곳에 내용을 삽입하거나 삭제

<br>

---

<br>

## useRef 로 컴포넌트 안의 변수 만들기

#### useRef의 또 다른 역할

- 컴포넌트 안에서 조회 및 수정 할 수 있는 변수 관리
- useRef로 관리되는 변수는 <u>값이 바뀌어도 컴포넌트가 리렌더링 되지 않는다</u>

#### 상태 VS useRef로 관리하는 변수

- 상태는 상태를 바꾸는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 된 상태를 조회 
- `useRef` 로 관리하고 있는 변수는 설정 후 바로 조회

#### useRef로 관리하는 변수의 예시

- `setTimeout`, `setInterval` 을 통해서 만들어진 `id`
- 외부 라이브러리를 사용하여 생성된 인스턴스
- scroll 위치

#### 관리해보기

- App.js
  - App 컴포넌트에서 `useRef` 를 사용하여 변수를 관리
  - 배열에 새 항목을 추가할 때, 새 항목에서 사용 할 고유 id 를 관리하는 용도
  - 필요한 사전 작업
    - UserList 에서 배열을 직접 선언해서 사용하는 대신에, 이 배열을 App 에서 선언하고 UserList 에게 props 로 전달
  
  ```javascript
  import React from 'react';
  
  import UserList from './UserList';
  
  function App() {
    const users = [
      {
        id: 1,
        username: 'velopert',
        email: 'public.velopert@gmail.com'
      },
      {
        id: 2,
        username: 'tester',
        email: 'tester@example.com'
      },
      {
        id: 3,
        username: 'liz',
        email: 'liz@example.com'
      }
    ];
    return <UserList users={users} />;
  }
  
  export default App;
  ```

- UserList.js

  ```javascript
  import React from 'react';
  
  function User({ user }) {
    return (
      <div>
        <b>{user.username}</b> <span>({user.email})</span>
      </div>
    );
  }
  
  function UserList({ users }) {
    return (
      <div>
        {users.map(user => (
          <User user={user} key={user.id} />
        ))}
      </div>
    );
  }
  
  export default UserList;
  ```

- App.js

  - 이제 App 에서 `useRef()` 를 사용하여 nextId 라는 변수 생성

  ```javascript
  import React, { useRef } from 'react';
  import UserList from './UserList';
  
  function App() {
    const users = [
      {
        id: 1,
        username: 'velopert',
        email: 'public.velopert@gmail.com'
      },
      {
        id: 2,
        username: 'tester',
        email: 'tester@example.com'
      },
      {
        id: 3,
        username: 'liz',
        email: 'liz@example.com'
      }
    ];
  
    // 변수 생성
    const nextId = useRef(4);
    const onCreate = () => {
      // 나중에 구현 할 배열에 항목 추가하는 로직
      // ...
  	// console.log(nextId.current); // 4
      nextId.current += 1; // 기존 값에 1을 더할 것
    };
    return <UserList users={users} />;
  }
  
  export default App;
  ```

  - `useRef()` 를 사용 할 때 파라미터를 넣어주면, 이 값이 `.current` 값의 기본값
  - 그리고 이 값을 수정 할때에는 `.current` 값을 수정하면 되고 조회 할 때에는 `.current` 를 조회
  - 값을 수정하거나 조회해도 리렌더링 되지않는다는걸 기억하기!

<br>

---

<br>

## 배열에 항목 추가하기

- src/CreateUser.js

  - input 두개와 button 하나로 이루어진 컴포넌트

  ```javascript
  import React from 'react';
  
  // 4개의 props를 받아옴
  function CreateUser({ username, email, onChange, onCreate }) {
    return (
      <div>
        <input
          name="username"
          placeholder="계정명"
          onChange={onChange}
          value={username}
        />
        <input
          name="email"
          placeholder="이메일"
          onChange={onChange}
          value={email}
        />
        <button onClick={onCreate}>등록</button>
      </div>
    );
  }
  
  export default CreateUser;
  ```

- App.js

  - 상태관리를 CreateUser 에서 하지 않고 부모 컴포넌트인 App 에서 하게 하고, input 의 값 및 이벤트로 등록할 함수들을 props 로 넘겨받아서 사용

  ```javascript
  import React, { useRef, useState } from 'react';
  import UserList from './UserList';
  import CreateUser from './CreateUser';
  
  function App() {
    const [inputs, setInputs] = useState({
      username: '',
      email: ''
    });
    const { username, email } = inputs;
    const onChange = e => {
      const { name, value } = e.target;
      setInputs({
        ...inputs,
        [name]: value
      });
    };
      
    // 상태로서 관리할때 useState로 감싸줌
    const [users, setUsers] = useState([
      {
        id: 1,
        username: 'velopert',
        email: 'public.velopert@gmail.com'
      },
      {
        id: 2,
        username: 'tester',
        email: 'tester@example.com'
      },
      {
        id: 3,
        username: 'liz',
        email: 'liz@example.com'
      }
    ]);
  
    const nextId = useRef(4);
    const onCreate = () => {
      // 나중에 구현 할 배열에 항목 추가하는 로직
      // ...
  	// 값 지우기
      setInputs({
        username: '',
        email: ''
      });
      nextId.current += 1;
    };
    return (
      <>
        <CreateUser
        {/* 네가지 props*/}
          username={username}
          email={email}
          onChange={onChange}
          onCreate={onCreate}
        />
        <UserList users={users} />
      </>
    );
  }
  
  export default App;
  ```

  - 배열에 변화 주기
    - 객체와 마찬가지로, 불변성을 지켜주어야
    - 배열의 `push`, `splice`, `sort` 등의 함수를 사용하면 안된다
      - 만약에 사용해야 한다면, 기존의 배열을 한번 복사하고 나서 사용

#### 불변성을 지키면서 배열에 새 항목을 추가하는 방법

##### spread 연산자 사용

- setUsers([...users, user]);

- App.js

  ```javascript
    const onCreate = () => {
      // 새로운 유저 객체 생성
      const user = {
        id: nextId.current,
        // ...inputs 해도 됨
        username,
        email
      };
      // 기존의 배열을 복사해서 만들고, 항목을 추가
      setUsers([...users, user]);
  
      setInputs({
        username: '',
        email: ''
      });
      nextId.current += 1;
    };
  ```

##### concat 함수 사용

- `concat` 함수는 기존의 배열을 수정하지 않고, 새로운 원소가 추가된 새로운 배열을 만들어줌
  - 여러개의 배열을 하나의 배열로 합쳐줌
  - 배열이 아닌 것도 배열에 합쳐줌 

- setUsers(users.concat(user));

- App.js

  

#### 1-13 구조에서 알아두면 좋은 점

- 부모 컴포넌트에서 state값(input 등등)과 함수를 작성하고 자식 컴포넌트에게 전달하는 구조를 기억하자

<br>

---

<br>

## 배열에 항목 제거하기

<br>

---

<br>

## 배열에 항목 수정하기

<br>

---

<br>

## useEffect를 사용하여 마운트/언마운트/업데이트시 할 작업 설정하기

<br>

---

<br>

## useMemo 를 사용하여 연산한 값 재사용하기

<br>

---

<br>

## useCallback 를 사용하여 함수 재사용하기

<br>

---

<br>

## React.memo 를 사용한 컴포넌트 리렌더링 방지

<br>

---

<br>

## useReducer 를 사용하여 상태 업데이트 로직 분리하기

<br>

---

<br>

