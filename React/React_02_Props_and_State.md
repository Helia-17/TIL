[toc]

# React

## Props

- properties
- 어떠한 값을 컴포넌트에게 전달해줘야 할 때 사용

### props 의 기본 사용법

> 컴포넌트 내부에서 코드를 작성한다.

- App.js
  - App 컴포넌트에서 Hello 컴포넌트를 사용 할 때 `name` 이라는 값을 전달

```javascript
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <Hello name="react" />
  );
}

export default App;
```

>  받는쪽은 props 라는 예약어를 통해 받는다.

- Hello.js
  - Hello 컴포넌트에서 name 값을 사용
  - props 는 객체 형태로 전달된다.
  - `name` 값을 조회하고 싶다면 `props.name` 을 조회

```react
import React from 'react';

function Hello(props) {
    //console.log(props)를 하면 {name: "react"}가 찍힘
  return <div>안녕하세요 {props.name}</div>
}

export default Hello;
```

<br>

### 여러개의 props, 비구조화 할당

> 컴포넌트의 파라미터에서 {}안에 받는 내용을 미리 표기한다.

- App.js
  - `color` 라는 값을 설정

```javascript
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <Hello name="react" color="red"//>
  );
}

export default App;
```

- Hello.js
  - Hello 컴포넌트에서 `color` 값을 조회해서 폰트의 색상으로 설정

```react
import React from 'react';

function Hello(props) {
    //console.log(props)를 하면 {name: "react"}가 찍힘
  return <div style={{ color: props.color }}>안녕하세요 {props.name}</div>
}

export default Hello;
```

- props 내부의 값을 조회 할 때마다 `props.` 를 입력하기 귀찮음

 => 함수의 파라미터에서 [비구조화 할당](https://learnjs.vlpt.us/useful/06-destructuring.html) (=구조 분해) 문법을 사용

```react
import React from 'react';

function Hello({ color, name }) {
  return <div 
         // 바깥쪽의 괄호는 style을 객체형태로 작성한 것, 안쪽의 괄호는 변수명이 아닌 구조분해 객체이므로
         style={{ color }}>안녕하세요 {name}</div>
}

export default Hello;
```

<br>

### defaultProps 로 기본값 설정

- props 를 지정하지 않았을 때 기본적으로 사용 할 값을 설정

- Hello.js

```react
import React from 'react';

function Hello({ color, name }) {
  return <div style={{ color }}>안녕하세요 {name}</div>
}

Hello.defaultProps = {
  name: '이름없음'
}

export default Hello;
```

- App.js
  - name 이 없는 Hello 컴포넌트를 렌더링

```react
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <>
      <Hello name="react" color="red"/> // 안녕하세요 react
      <Hello color="pink"/> // 안녕하세요 이름없음
    </>
  );
}

export default App;
```

<br>

### props.children

> 컴포넌트 태그 사이에 값이 있을때 'children'이란 예약어를 사용한다.

- 컴포넌트 태그 사이에 넣은 값을 조회할 때
- src/Wrapper.js

```react
import React from 'react';

function Wrapper() {
  const style = {
    border: '2px solid black',
    padding: '16px',
  };
  return (
    <div style={style}>
          {/* 비어 있다 */}
    </div>
  )
}

export default Wrapper;
```

- App.js

  - Wrapper 컴포넌트 사용
    - Wrapper 태그 내부에 Hello 컴포넌트 두개
    - 브라우저를 확인하면 Hello 컴포넌트들은 보여지지 않음
    - 내부의 내용이 보여지게 하기 위해서는 Wrapper 에서 `props.children` 을 렌더링해야

  ```javascript
  import React from 'react';
  import Hello from './Hello';
  import Wrapper from './Wrapper';
  
  function App() {
    return (
      <Wrapper>
        <Hello name="react" color="red"/>
        <Hello color="pink"/>
      </Wrapper>
    );
  }
  
  export default App;
  ```

- 다시 src/Wrapper.js

  ```react
  import React from 'react';
  
  function Wrapper() {
    const style = {
      border: '2px solid black',
      padding: '16px',
    };
    return (
      <div style={style}>
            {children}
      </div>
    )
  }
  
  export default Wrapper;
  ```



> 쓰이는 곳(App.js)에서 값을 정한다 = props(부모)
> 쓰임 당하는 곳(Hello.js나 Wrapper.js)에서 값을 정한다 = children

<br>

---

<br>

## 조건부 렌더링

- 특정 조건에 따라 다른 결과물을 렌더링 하는 것

- App.js

  - App 컴포넌트에서 Hello 컴포넌트를 사용 할 때, `isSpecial` 이라는 props 를 설정

  ```react
  import React from 'react';
  import Hello from './Hello';
  import Wrapper from './Wrapper';
  
  
  function App() {
    return (
      <Wrapper>
        <Hello name="react" color="red" isSpecial={true}/>
        <Hello color="pink" />
      </Wrapper>
    )
  }
  
  export default App;
  ```

  - `true` 는 자바스크립트 값이기 때문에 중괄호

- Hello.js

  - Hello 컴포넌트에서는 isSpecial 이 `true` 이냐 `false` 이냐에 따라서 컴포넌트의 좌측에 * 표시
  - 가장 기본적인 방법인 삼항연산자를 사용
    - `isSpecial` 값이 `true` 라면 `<b>*</b>` 를, 그렇지 않다면 `null` 
    -  JSX 에서 null, false, undefined 를 렌더링하게 된다면 아무것도 나타나지 않음

  ```react
  import React from 'react';
  
  function Hello({ color, name, isSpecial }) {
    return (
      <div style={{ color }}>
        { isSpecial ? <b>*</b> : null }
        안녕하세요 {name}
      </div>
    );
  }
  
  Hello.defaultProps = {
    name: '이름없음'
  }
  
  export default Hello;
  ```

<br>

#### 삼항연산자를 사용한 조건부 렌더링

- 특정 조건에 따라 보여줘야 하는 내용이 다를 때 사용

- 단순히 특정 조건이 `true` 이면 보여주고, 그렇지 않다면 숨겨주는 경우에는 `&&` 연산자를 사용해서 처리하는 것이 더 간편

  - &&를 사용하면 첫번째로 나오는 false값을 반환하며 없다면 마지막 값을 반환한다.
  - [단축 평가 논리 계산법](https://learnjs.vlpt.us/useful/03-short-circuiting.html) 

- Hello.js

  ```react
  import React from 'react';
  
  function Hello({ color, name, isSpecial }) {
    return (
      <div style={{ color }}>
        {isSpecial && <b>*</b>}
        안녕하세요 {name}
      </div>
    );
  }
  
  Hello.defaultProps = {
    name: '이름없음'
  }
  
  export default Hello;
  ```

  - `isSpecial && <b>*</b>` 의 결과는 
    `isSpecial` 이 `false` 일땐 `false` 이고,
     `isSpecial`이 `true` 일 땐 `<b>*</b>` 
    (`<b>*</b>` 는 값이 있으니 `true`로 취급됨)

<br>

#### props 값 설정을 생략하면 ={true}

- 컴포넌트의 props 값을 설정하게 될 때 만약 props 이름만 작성하고 값 설정을 생략한다면, 
  이를 `true` 로 설정한 것으로 간주

- App.js

  - 이렇게 `isSpecial` 이름만 넣어주면 `isSpecial={true}` 와 동일한 의미

  ```react
  function App() {
    return (
      <Wrapper>
        <Hello name="react" color="red" isSpecial />
        <Hello color="pink"/>
      </Wrapper>
    );
  }
  ```

<br>

---

<br>

## useState를 통한 동적 상태 관리

- Counter.js

  - 버튼을 누르면 숫자가 바뀌는 Counter 컴포넌트

  ```react
  import React from 'react';
  
  function Counter() {
    return (
      <div>
        <h1>0</h1>
        <button>+1</button>
        <button>-1</button>
      </div>
    );
  }
  
  export default Counter;
  ```

- App.js

  - App 에서 Counter 를 렌더링

  ```react
  import React from 'react';
  import Counter from './Counter';
  
  function App() {
    return (
      <Counter />
    );
  }
  
  export default App;
  ```

### 이벤트 설정 

- `on이벤트이름={실행하고싶은함수}`
- 이벤트를 설정할때에는 함수타입의 값을 넣어주어야 한다

- Counter.js

  - 버튼이 클릭되는 이벤트가 발생 했을 때, 특정 함수가 호출되도록 설정
  - `onIncrease` 와 `onDecrease` 는 화살표 함수를 사용하여 구현
    - 화살표 함수에 대해서 잘 모른다면 이 [링크](https://learnjs.vlpt.us/basics/05-function.html#화살표-함수)
  - 함수를 만들고, button 의 `onClick` 으로 각 함수를 연결
    - 이벤트는 camelCase이며 on으로 시작(자동완성 목록에서 고를 수 있음)
  - 주의: 함수형태를 넣어주어야 하지, 함수를 `onClick={onIncrease()}`과 같이 실행하면 안됨
    - 이렇게 하면 렌더링되는 시점에서 함수가 호출

  ```react
  import React from 'react';
  
  function Counter() {
    const onIncrease = () => {
      console.log('+1')
    }
    const onDecrease = () => {
      console.log('-1');
    }
    return (
      <div>
        <h1>0</h1>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    );
  }
  
  export default Counter;
  ```

### 동적인 값 끼얹기, useState

- 상태(state)

  - 컴포넌트에서 동적인 값

- `useState` 라는 함수

  - 컴포넌트에서 상태를 관리
  - `useState` 를 사용 할 때에는 상태의 기본값을 파라미터로 넣어서 호출
  - 이 함수를 호출해주면 배열이 반환
  - 

- counter.js

  ```react
  import React, { useState } from 'react'; // 수정
  
  function Counter() {
      // number라는 state를 작성했고, 이 값은 0이며, 이를 변경하는 함수는 setNumber
    const [number, setNumber] = useState(0); // 수정
    <!-- 구조분해 할당 전 구조
  	numberState는 개발자가 임의로 지정한 변수(구조분해할당하면 필요없음)
  	const numberState = useState(0);
  	const number = numberState[0];
  	const setNumber = numberState[1];
      -->
  
    const onIncrease = () => {
      setNumber(number + 1); // 수정
    }
  
    const onDecrease = () => {
      setNumber(number - 1); // 수정
    }
  
    return (
      <div>
        <h1>{number}</h1> // 수정
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    );
  }
  
  export default Counter;
  ```

### 함수형 업데이트

- Setter 함수를 사용 할 때, 새로운 값을 파라미터로 넣어주는 대신,
  대신에 기존 값을 어떻게 업데이트 할 지에 대한 함수를 등록

- 주로 나중에 컴포넌트를 최적화를 하게 될 때 사용

- Counter.js

  ```react
  import React, { useState } from 'react';
  
  function Counter() {
    const [number, setNumber] = useState(0);
  
    const onIncrease = () => {
      setNumber(prevNumber => prevNumber + 1);
      // setNumber(n => n + 1);의 형태도 가능. 상관없음
    }
  
    const onDecrease = () => {
      setNumber(prevNumber => prevNumber - 1);
    }
  
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    );
  }
  
  export default Counter;
  ```

<br>

---

<br>

## input

### 상태 관리하기

- src/InputSample.js

  ```javascript
  import React from 'react';
  
  function InputSample() {
    return (
      <div>
        <input />
        <button>초기화</button>
        <div>
          <b>값: </b>
        </div>
      </div>
    );
  }
  
  export default InputSample;
  ```

- App.js

  ```javascript
  import React from 'react';
  import InputSample from './InputSample';
  
  function App() {
    return (
      <InputSample />
    );
  }
  
  export default App;
  ```

- InputSample.js

  - input 에 입력하는 값이 하단에 나타나게 하고, 초기화 버튼을 누르면 input 이 값이 비워지도록 구현
  - `useState` 를 사용
  -  input의 onChange를 사용하면 이벤트 객체 e를 파라미터로 받아올 수 있다.
  - 이 객체의 e.target은 이벤트가 발생한 DOM을 가리킨다.
  - e.target.value를 조회하면 현재 input의 value값을 알 수 있다.
    - 이 값을 `useState` 를 통해서 관리
  - input 태그의 `value` 값도 설정
    - 초기화버튼클릭과 같이 state의 값이 바뀌었을때 input 의 내용도 업데이트

  ```javascript
  import React, { useState } from 'react';
  
  function InputSample() {
    const [text, setText] = useState('');
  
    const onChange = (e) => {
      setText(e.target.value);
    };
  
    const onReset = () => {
      setText('');
    };
  
    return (
      <div>
        <input onChange={onChange} value={text}  />
        <button onClick={onReset}>초기화</button>
        <div>
          <b>값: {text}</b>
        </div>
      </div>
    );
  }
  
  export default InputSample;
  ```

### 여러개의 input 상태 관리하기

- 단순히 `useState` 를 여러번 사용하고 `onChange` 도 여러개 만들어서 구현 할 수 있지만 비추
- 더 좋은 방법은, input 에 `name` 을 설정하고 이벤트가 발생했을 때 이 값을 참조하는 것
- `useState` 에서는 문자열이 아니라 객체 형태의 상태를 관리

- InputSample.js

  - 기존 상태 지움, `onChange` 와 `onReset` 함수 비움.

  ```javascript
  import React, { useState } from 'react';
  
  function InputSample() {
    const [inputs, setInputs] = useState({
      name: '',
      nickname: ''
    });
  
    const { name, nickname } = inputs; // 비구조화 할당을 통해 값 추출
  
    const onChange = (e) => {
      // console.log(e.target.name);
      // console.log(e.target.value);
      const { value, name } = e.target; // 우선 e.target 에서 name 과 value 를 추출
        
        
       /* 개선 전 구조
       const nextInputs = {
       	... inputs,
       };
       
       nextInputs[name] = value;
       
       setInputs(value)
       */
        
      // 개선 후 구조
      setInputs({
        ...inputs, // 기존의 input 객체를 복사한 뒤
        [name]: value // name 키를 가진 값을 value 로 설정
      });
    };
  
    const onReset = () => {
      setInputs({
        name: '',
        nickname: '',
      })
    };
  
  
    return (
      <div>
        {/* 길어졌을 땐 이렇게 가능 */}
        <input
        	name="name"
  		placeholder="이름"
  		onChange={onChange}
  		value={name}
         />
        <input name="nickname" placeholder="닉네임" onChange={onChange} value={nickname}/>
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

  - name: state의 어떤 프로퍼티(키) 인지 (=key)
    value:값이 무엇인지 

#### State에서 객체를 수정할 때

- 직접 수정하면 안된다.

  - 기존 상태를 직접 수정하게 되면, 값을 바꿔도 리렌더링이 되지 않음

  ```javascript
  inputs[name] = value;
  ```

- "불변성을 지킨다"

  - 불변성을 지켜주어야만 리액트 컴포넌트에서 상태가 업데이트가 됐음을 감지 할 수 있고 이에 따라 필요한 리렌더링이 진행
  - 불변성을 지켜주어야만 컴포넌트 업데이트 성능 최적화가 가능

- 직접 수정 대신, 새로운 객체를 만들어서 새로운 객체에 변화를 주고, 이를 상태로 사용

  -  `...` 문법은 spread 문법 [링크](https://learnjs.vlpt.us/useful/07-spread-and-rest.html)
    - 객체의 내용을 모두 "펼쳐서" 기존 객체를 복사  

  ```javascript
  setInputs({
    ...inputs,
    [name]: value
  });
  ```

- - 



##### onChange

- 변할때마다 실행된다.
- 주로 input 태그의 이벤트값을 받아와서 name과 value를 비구조화 할당을 통해 추출한다.

##### onClick

- 클릭되면 실행된다.

#### 헷갈리는 부분 정리

- 비구조화 할당 : 객체를 추출하는 방법
- 구조분해 할당 : 객체나 배열을 변수로 '분해’할 수 있게 해주는 특별한 문법



> #### 최적화에 대하여
>
> - setState는 shouldComponentUpdate(nextProps, nextState)를 트리거하는데 이 메소드의 boolean 반환값에 따라 render 호출 여부가 결정
>
> - 이 메소드를 재정의하지 않으면 setState 호출 시마다 render가 호출
>
> -  '최적화'는 여러분이 shouldComponentUpdate 재정의를 통해 render 호출 여부를 결정하는 것
>
> - 예시
>
>   ```javascript
>   shouldComponentUpdate(nextProps: Props, nextState: State) {
>     for (const [key, value] of Object.entries(nextState)) {
>       if (typeof value != "object") {
>         if (this.state.isLoading != nextState.isLoading) {
>           return true;
>         }
>       }
>       else {
>         // codes for deep comparison here depending on your case
>       }
>     }
>     return false;
>   }
>   ```
>
> <br>
>
> #### state는 왜 immutable하게 다뤄야 하는가
>
> -  React는 개발자가 호출한 setState로
>   특정 state의 값이 실제로 변경되기 전에
>   shouldComponentUpdate를 호출시켜
>   개발자로 하여금 해당 state의 기존 값과 새로운 값을 비교하여
>   render 호출 여부를 결정하도록 기회를 준다
>
> - 다음과 같은 state set이 있고 shouldComponentUpdate를 통해 incremental의 변경에 대해 최적화하는 경우
>
>   ```
>   state = {
>     incremental: 0,
>     ...
>   };
>   ```
>
> - incremental를 다음과 같은 방식으로 변경한다면
>
>   ```
>   this.setState({
>     incremental: ++incremental
>   });
>   ```
>
>   위의 setState 호출 후 바로 호출될 앞서 정의한 shouldComponentUpdate에서 현재 incremental값이 변경될 값과 동일하므로 변경점을 찾지 못할 것이고 결국 false를 반환하게 될 것
>
> - 결론적으로
>   위의 예시와 같이 
>   <u>"다른 lifecycle 메소드들에서 여러분이 값을 직접 지정한 state에 대해 참조가 일어날 때 컴포넌트 전체 로직이 깨질 여지가 있기 때문에"</u> state를 immutable하게 취급하라
> - React가 해당 state를 변경하기 전까지 여러분이 현재 state 값을 지정하지 않기를 권장
>
> <br>
>
> #### 그럼에도 현재 state에 직접 변경을 가하여 최적화하고 싶다면
>
> - 대부분 Array 타입의 state를 변경하는 경우일 것
>
> - 해당 state에 데이터를 추가 혹은 삭제 시 shouldComponentUpdate에서 검사할 필요도 없이 render는 반드시 호출돼야
>
>   - 아래와 같은 배열 복사는 무의미
>
>   ```
>   const newItems = Array.from(this.state.items);
>   ... // data insertion into newItems
>   this.setState({
>     items: newItems
>   });
>   ```
>
> - 다른 메소드에서
>    `this.state.items`의 어떤 원소들의 특정 값 혹은 그 원소 자체를 바꾸고
>   이를shouldComponentUpdate에서 최적화 시키고 싶은 경우,
>   해당 변경을 알리는 **변수**를 따로 두면 쉽게 구현할 수 있음
>
>   ```
>   private onInputChange(ev: React.FormEvent<HTMLInputElement>) {
>     const input = ((ev.target as HTMLInputElement).value).toLocaleLowerCase();
>     for (const item of this.state.items) {
>       const preDisplay = item.display
>       item.display = item.nameForFiltering.includes(input); // display, nameForFiltering은 각각 items[i]의 boolean, string property
>       this.hasDataModified = preDisplay != item.display;
>     }
>     this.setState({
>       items: this.state.items
>     });
>   }
>   
>   shouldComponentUpdate(nextProps: Props, nextState: State) {
>     ...
>     if (this.hasDataModified) {
>       this.hasDataModified = false;
>       return true;
>     }
>   }
>   ```
>
> - **useState hook과 spread 연산자**
>   함수형 컴포넌트에서 state 관리를 위한 hook `useState(...)`는 class형 컴포넌트 state의 특정 키/값 쌍에 대응합니다. 풀어서 설명하자면
>   `class형 컴포넌트의 this.state.<키> == 함수형 컴포넌트의 useState(...)[0]`
>   `class형 컴포넌트의 this.setState({키: 값}) == 함수형 컴포넌트의 useState(...)[1](값)`
>   본문에서 state setter에서 spread 연산자를 사용한 이유는 저 값이 object타입이기 때문입니다. 함수형 컴포넌트에서 useState로 관리하는 어떤 state 값이 object 타입이 아니거나, class형 컴포넌트일 경우 spread 연산자를 사용할 필요가 없습니다.