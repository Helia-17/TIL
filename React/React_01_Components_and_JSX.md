[TOC]

# REACT

> https://ko.reactjs.org/docs/getting-started.html

## 배경

### 리액트는 어쩌다 만들어졌을까?

#### DOM

- 각 HTML 엘리먼트에 대한 정보를 지니고 있는 JS 객체
- DOM 을 변형하려면 브라우저의 DOM ㄴelector API를 사용해서 특정 돔을 선택한 뒤에 특정 이벤트가 발생하면 변화를 주는 것
  - dom을 직접 건드리는 작업은 번거롭다
  - 유지보수가 힘듬

#### Ember, Backbone, AngularJS 등의 프레임워크

- 자바스크립트의 특정 값이 바뀌면 특정 DOM의 속성이 바뀌도록 연결을 해주어서, 업데이트 하는 작업을 간소화해주는 방식으로 웹개발의 어려움을 해결

#### React의 발상

- dom을 전부 날려버리고 다시 만들어서 보여주자
- "업데이트를 어떻게 해야 할 지" 에 대한 고민이 필요 없음

#### Virtual DOM

![img](React_01_Components_and_JSX.assets/u6YnxUS.png)

- 정말로 동적인 UI 를 보여주기 위해서 모든걸 다 날려버리고 모든걸 새로 만들게 된다면, 속도가 굉장히 느릴 것

- Virtual DOM 이라는 것을 사용해서 이를 가능케 함

- Virtual DOM: 가상의 DOM

  - 브라우저에 실제로 보여지는 DOM 이 아니라 그냥 메모리에 가상으로 존재하는 DOM
  - 그냥 JavaScript 객체이기 때문에 작동 성능이 실제로 브라우저에서 DOM 을 보여주는 것 보다 속도가 훨씬 빠름

- 업데이트가 필요한 부분만 가상DOM으로 수정

  - 리액트는 상태가 업데이트 되면,

  1. 업데이트가 필요한 곳의 UI 를 Virtual DOM 을 통해서 렌더링
  2. 알고리즘을 통하여 실제 브라우저에 보여지고 있는 DOM 과 비교
  3. 차이를 실제 DOM 에 패치시켜줌

  - 이를 통하여, "업데이트를 어떻게 할 지" 에 대한 고민을 하지 않으면서, 빠른 성능도 지켜낼 수 있게 되었다.



# 사용해보기

## 온라인 플레이그라운드

- CodePen https://codepen.io/pen?&editors=0010
- CodeSandbox https://codesandbox.io/s/new
- Stackblitz https://stackblitz.com/edit/react-94fyl2



## 설치하기

### node.js

- 브라우저 환경이 아닌 곳에서도 javascript를 실행하게 해주는 javascript런타임
- Webpack 과 Babel 같은 도구들이 자바스크립트 런타임인 Node.js 를 기반으로 만들어져있음. 그렇기에 해당 도구들을 사용하기 위해서 Node.js 를 설치
- macOS / Linux 의 경우엔, [nvm](https://github.com/nvm-sh/nvm) 이라는 도구를 사용하여 Node.js 를 설치

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
$ nvm install --lts
```



### Yarn

- 조금 개선된 버전의 npm 
- npm: Node.js 를 설치하게 될 때 같이 딸려오는 패키지 매니저 도구
  - 프로젝트에서 사용되는 라이브러리를 설치하고 해당 라이브러리들의 버전 관리를 하게 될 때 사용
- 더 나은 속도, 더 나은 캐싱 시스템을 사용하기 위해 Yarn 권장



### 코드 에디터

- VSCode, Atom, WebStorm, Sublime...



## 시작하기

```bash
$ yarn install
```

```bash
$ cd begin-react
$ yarn start
```

- yarn이 없다면 npm start

### 컴포넌트 생성

- 함수형태로 작성 할 수도 있고 클래스형태로도 작성 할 수 있음

- 함수 형태 작성
  - src 디렉터리에 js 파일 작성

```javascript
// Hello.js

// 리액트를 불러와주어야
import React from 'react';

function Hello() {
    // HTML처럼 생긴 JSX를 리턴
  return <div>안녕하세요</div>
}

// Hello를 만들어서 내보내주겠다를 의미
export default Hello;
```

### 컴포넌트 불러오기

##### App.js

- 기본구조

```javascript
// 필요 없음
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    // 이하 div 구조만 남겨둘 것
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

```

```javascript
// 수정 후
import React from 'react'; // react 불러오기
// 태그 입력시 자동완성을 통해 자동으로 입력되도록 할 수 있다.
import Hello from './Hello'; // 필요한 컴포넌트 불러오기.

function App() {
  return (
    <div>
      <Hello /> //띄어쓰기 필요!
    </div>
  );
}

export default App;
```



### 컴포넌트 재사용

> `<Hello />` 3번 입력하면 3번 사용하는 것.

- 보통은 하나의 웹페이지에 여러 React 컴포넌트를 설치

- 다음 예제는 “좋아요” 버튼 3개를 만들고 그 컴포넌트들에 데이터를 넘겨주는 코드

  [예제 전체 소스 코드 보기](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda)

- 이 방법은 대개 페이지에서 React로 만들어진 부분들이 서로 격리 되어있을 때 유용

- React 코드 내에서는 [컴포넌트 합성](https://ko.reactjs.org/docs/components-and-props.html#composing-components)을 사용하는 편이 더 쉬움



##### index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
// 아이디가 root인 것을 찾아서 리액트 App을 넣겠다

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

- ReactDOM.render 의 역할
  - 브라우저에 있는 실제 DOM 내부에 리액트 컴포넌트를 렌더링하겠다는 것을 의미

##### public/index.html

- 아이디가 `root`인 div가 위치
- 리액트 컴포넌트가 렌더링 될 때에는, 렌더링된 결과물이 이 div 내부에 렌더링되는 것

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!--
      manifest.json provides metadata used when your web app is installed on a
      user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <!-- 여기!!!! -->
    <div id="root"></div> 
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
</html>

```



> ### 웹사이트에 React 추가
>
> - React는 처음부터 점진적으로 도입할 수 있게 설계되었음
>
> #### 1분 내로 React 추가하기
>
> ##### 1단계: HTML 파일에 DOM 컨테이너 설치
>
> - `<div>` 태그: React를 통해 원하는 내용을 표시할 수 있는 위치
>   - 보통 이 태그는 비어있다. React가 DOM 컨테이너 안에 내용을 추가해준다.
>
> -  `id`를 부여: JavaScript가 태그를 찾고 찾은 태그 안에 React 컴포넌트를 표시할 수 있게
>
> ##### 2단계: 스크립트 태그 추가하기
>
> - `<script>` 태그 3개를 닫는 태그인 `</body>` 앞에 추가
>
>   - 처음 두 태그는 React를 실행시키고 3번 째 코드는 만든 컴포넌트를 실행
>
>   ```html
>   <!-- ... 다른 HTML ... -->
>   
>     <!-- React를 실행. -->
>     <!-- 주의: 사이트를 배포할 때는 "development.js"를 "production.min.js"로 대체하세요. -->
>     <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
>     <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
>   
>     <!-- 만든 React 컴포넌트를 실행. -->
>     <script src="like_button.js"></script>
>   
>   </body>
>   ```
>
> ##### 3단계: React 컴포넌트 만들기
>
> - `like_button.js` 라는 이름으로 HTML 페이지 옆에 새 파일을 만듬
>
> - **[스타터 코드](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)** 를 열고 코드를 방금 만든 파일에 복사
>
>   - 이 코드는 `LikeButton` 이라는 React 컴포넌트를 정의해준다
>
> - `like_button.js`의 맨 뒷 줄에 다음 코드 두 줄을 추가
>
>   - 이 두줄의 코드는 첫 단계에서 HTML 페이지에 추가했던 `<div>` 태그를 찾아주고 그 안에 “좋아요” 버튼이라는 React 컴포넌트를 추가
>
>   ```javascript
>   // ... 복사했던 스타터 코드 ...
>   
>   const domContainer = document.querySelector('#like_button_container');
>   ReactDOM.render(e(LikeButton), domContainer);
>   ```
>
> **[예제 전체 소스 코드 보기](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605)**

<br>

- 

<br>

---

<br>

##### [팁]프로덕션을 위한 JavaScript의 압축

- 프로덕션을 위해 웹사이트를 배포하기 전에 JavaScript 파일을 압축하지 않는다면 웹사이트를 사용할 때 눈에 띄는 성능 저하가 일어날 것
- 애플리케이션 스크립트를 이미 압축했을 경우 배포된 HTML 파일이 `production.min.js`로 끝나는 React 파일을 확실히 실행하기만 하면 **사이트는 프로덕션 준비가 완료**

```html
<script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>

  <!-- 만든 React 컴포넌트를 실행. -->
  <script src="like_button.min.js"></script>
```

- 스크립트를 압축하는 절차가 따로 없다면 [이 사이트를 참고해서 설정](https://gist.github.com/gaearon/42a2ffa41b8319948f9be4076286e1f3)



> React를 사용하는 이유는 컴포넌트들을 만들고 그것들을 재사용하기 위함입니다. 개인적으로는 React와 같은 라이브러리들이 '컴포넌트'라고 부르는 것의 핵심 아이디어는 component보다 template이라는 단어가 더 잘 표현한다고 생각합니다. React를 사용한다는 것은 곧 재사용 가능한 틀(template)을 만들고, 틀로 찍어낼 instance를 커스터마이징 가능하도록 해당 틀에 구멍들(slots)을 뚫고, 인스턴스에 전달되는 props나 인스턴스 내부의 state로 그 구멍들을 채우는 일입니다.
>
> 사실 재사용 가능한 컴포넌트를 정의하는 것 따위는 js로도 가능하기에 위 설명은 반쪽짜리도 안 됩니다. React와 같은 라이브러리들의 컴포넌트는 선언적이기에 선호됩니다. 예를 들어 어떤 컴포넌트가 렌더링 값으로 반환하는 html template을 document.createElement("...")나 엘리먼트.innerHTML = "..."이 아닌 html 문법 그대로 사용할 수 있을 뿐만 아니라, template에 삽입할 state/prop값들을 위한 구멍들을 그 template에 선언적으로(`<div>{this.state.msg}</div>`) 정의할 수 있습니다.
>
> React와 같은 라이브러리들이 자랑하는 Virtual DOM은 사실 **선언적인 컴포넌트에서 데이터 업데이트 시 절차적 코드와 가까운 성능을 내기 위한 장치**이지, 그것이 절차적 코드보다 빠른 속도를 내도록 하는 것은 아닙니다. React는 class형 컴포넌트의 render함수나 함수형 컴포넌트에서 **반환되는 DOM을 렌더링된 DOM과 비교한 후, 변경점이 존재할 시 Native DOM에 적용**합니다.
>
> [출처](https://react.vlpt.us/basic/12-variable-with-useRef.html)



## JSX

- 리액트에서 생김새를 정의할 때, 사용하는 문법
  
  - `return <div>안녕하세요</div>;`
- 컴포넌트 를 여러가지 파일로 분리해서 저장 할 때 일반 자바스크립트가 아닌 JSX 라는 문법으로 작성
  
  - 얼핏보면 HTML 같이 생겼지만 실제로는 JavaScript
- 리액트 컴포넌트에서 XML 형식의 값을 반환
- XML 형태로 코드를 작성하면 babel 이 JSX 를 JavaScript 로 변환을 해줌

- 기존

  ```react
  const e = React.createElement;
  
  // "좋아요" <button>을 표시
  return e(
    'button',
    { onClick: () => this.setState({ liked: true }) },
    'Like'
  );
  ```

  

- JSX

  ```react
  //  "좋아요" <button>을 표시
  return (
    <button onClick={() => this.setState({ liked: true })}>
      Like
    </button>
  );
  ```

- **JSX는 [필수가 아닌 선택사항](https://ko.reactjs.org/docs/react-without-jsx.html)**

- UI 코드를 짤 때 JSX를 쓰는 것이 더 편리



### JSX 규칙

#### 1. 태그는 꼭 닫혀있어야 한다.

- HTML 에서는 `input` 또는 `br` 태그를 사용 할 때 닫지 않고 사용하기도 하지만, 리액트에서는 그렇게 하면 안됨
  - `<br><br>` (O), `<br />` (O), `<br>` (x) 

- 태그와 태그 사이에 내용이 들어가지 않을 때에는, **Self Closing 태그** 라는 것을 사용
  - `<Hello />`
  - 열리고, 바로 닫히는 태그를 의미

#### 2. 두개 이상의 태그는 무조건 하나의 태그로 감싸져있어야 한다.

- 잘못된 예

```react
function App() {
  return (
    <Hello />
    <div>안녕히계세요.</div>
  );
}
```

- 바른 예

```react
function App() {
  return (
   {/* 하나의 태그로 감싸서 처리 */}
    <div> 
      <Hello />
      <div>안녕히계세요</div>
    </div>
  );
}
```

- 불필요하게 div로 감싸야 하는 상황이 있을 것 (table 관련 태그를 작성 할 때에도 내용을 div 같은걸로 감싸기엔 애매)

  - 리액트의 **Fragment** 라는 것을 사용

    ```react
    function App() {
      return (
       {/* 이름이 없는 fragment태그, 개발자도구의 HTML Elements에 나타나지 않음 */}
        <> 
          <Hello />
          <div>안녕히계세요</div>
        </>
      );
    }
    ```

  - 괄호`()`가 없어도 작동하나 가독성을 위해  괄호 사용 

#### 3. JSX 안에서 Javascript 값 사용할 때에는 {}를 사용한다

- JSX 내부에 자바스크립트 변수를 보여줘야 할 때에는 `{}` 으로 감싸기

```react
function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      {/* 없이하면 문자열 name이 되겠지! */}
      <div>{name}</div> 
    </>
  );
}
```

#### 4. style 과 className

##### 인라인스타일의 경우 style의 네이밍은 camelCase로 사용해야한다

```react
function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24, // 기본 단위 px
    padding: '1rem' // 다른 단위 사용 시 문자열을 사용 ex)'10px'
  }

  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
    </>
  );
}
```

- HTML과 `style` 과 CSS class 를 설정 방법이 다름
- 인라인 스타일은 객체 형태로 작성
  - `<div style={style}>{name}</div>`
-  `-` 로 구분되어 있는 이름들은 camelCase 형태로 네이밍
  - `background-color` -> `backgroundColor`

##### css파일에서 불러올때는 'className=' 으로 설정해야한다.

- App.css

```css
.gray-box {
  background: gray;
  width: 64px;
  height: 64px;
}
```

- App.js
  - `class=` 가 아닌 `className=` 으로 설정 (camleCase!)
    - `class=`여도 작동은 하지만 경고가 뜸. 권장하지 않음

```javascript
import React from 'react';
import Hello from './Hello';
import './App.css'; // 불러오는 방법

function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      <div className="gray-box"></div>
    </>
  );
}
```

#### 5. 주석

- JSX 내부의 주석은 `{/* 이런 형태로 */}` 작성

```react
import React from 'react';
import Hello from './Hello';

function App() {
  return (
      {/* 주석은 화면에 보이지 않습니다 */}
      /* 중괄호로 감싸지 않으면 화면에 보입니다 */
      <Hello 
      />
  );
}
```

- 태그와 클로징 태그에서의 주석 작성

```react
import React from 'react';
import Hello from './Hello';
import './App.css'; // 불러오는 방법

function App() {
  const name = 'react';
  return (
      <Hello 
      	// 이런식으로 작성하는 주석은 화면에 나타나지 않습니다
      />
      <div 
      	// 여기에도 주석 작성이 가능합니다
      style={style}>{name}</div>
  );
}
```



## Babel

> Babel is a JavaScript compiler.
>
> https://bit.ly/2wMpkk2
>
> babel이 브라우저가 이해할 수 있는 문법으로 변환해준다. ES6, ES7 등의 최신 문법을 사용해서 코딩을 할 수 있기 때문에 생산성이 향상된다.

JSX 를 비롯한 새로운 자바스크립트 문법들을 사용하기 위해 Babel이라는 도구를 사용

- JSX

```xml
(
<div>
  <b>Hello, </b> <span>React</span>  
</div>
)
```

- javascript

```javascript
"use strict";

/*#__PURE__*/
React.createElement("div", null, /*#__PURE__*/React.createElement("b", null, "Hello, "), " ", /*#__PURE__*/React.createElement("span", null, "React"));
```

`자바스크립트 컴파일러`

- 왜 인터프리터 언어에 컴파일러가 필요하지?
  -  javascript 로 결과물을 만들어주는 컴파일러
  -  `소스 대 소스 컴파일러 (transpiler)`
- 왜 javascript 로 변환하는 과정이 필요할까?
  - ESNext and Legacy… Legacy…
    - 새로운 ESNext 문법을 기존의 브라우져에 사용하기 위해서 babel 은 필수적
  - New Language
    -  typescript 든 coffeescript 든 javascript 로의 compile 이 필수가 되어야 하며,
       이를 담당하는게 babel
- [create-react-app](https://github.com/facebookincubator/create-react-app)에도 기본으로 들어있음



> #### babel-polyfill?
>
> > polyfill은 프로그램이 처음에 시작될 때 현재 브라우저에서 지원하지 않는 함수를 검사해서 각 object의 prototype에 붙여주는 역할을 한다.
>
> - 폴리필(polyfill) 은 개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인을 의미
>
> - 브라우저에서 지원하지 않는 기능들에 대한 호환성 작업을 채워 넣는다고 해서 polyfill
> - babel 은 이러한 polyfill 을 손쉽게 지원하기 위해 babel-polyfill 기능을 지원
> - 이미 문법을 컴파일 해서 javascript 로 compile 한다고 했는데… 왜 polyfill 이 필요할까?
>   - babel 을 사용한다고 최신 함수를 사용할 수 있는 건 아님
>   - babel 은 문법을 변환하여 javascript 로 변환하는 transpiler 역할만 할 뿐
>   - polyfill 은 프로그램이 처음에 시작될 때 지원하지 않는 기능들을 추가하는 것
>   - babel 은 컴파일시에 실행되고 babel-polyfill 은 런타임에 실행되는 것
>
> - babel-polyfill을 사용하고 싶다면 별도로 [설정](http://babeljs.io/docs/usage/polyfill/)해줘야
>
> #### .babelrc
>
> >  [.babelrc](http://babeljs.io/docs/usage/babelrc/) 파일을 프로젝트 root 폴더에 생성하자. plugins와 presets 속성이 중요하다. 위에서 설명했던 각 문법이 하나의 plugin이라고 생각하면 된다. 그리고 preset은 plugin 여러 개가 묶여있는 개념이다. 대표적으로 ES6 문법을 모아놓은 es2015 preset과 react 문법을 모아놓은 react preset이 있다. 사용할 preset을 presets에 추가하고 presets에 속해있는 plugin 외에 추가로 사용하고 싶은 plugin은 plugins에 넣자.





### 실습

#### JSX 빠르게 시도해보기

- `<script>` 태그를 집어넣기

  ```html
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  ```

- 이제 어떤 `<script>` 태그에서든 `type="text/babel"`성질을 추가하면 JSX를 사용할 수 있음

  ```html
      <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    </head>
    <body>
      <div id="root"></div>
      <script type="text/babel">
  
        ReactDOM.render(
          <h1>Hello, world!</h1>,
          document.getElementById('root')
        );
  
      </script>
    </body>
  ```

#### 프로젝트에 JSX 추가하기

- **1단계:** `npm init -y`

> If you get an "Invalid name" error when you run `npm init -y`, rename the project folder to only contain lowercase ASCII letters or hyphens (e.g. `my-project`), and try again.

- **2단계:** `npm install babel-cli@6 babel-preset-react-app@3`를 실행

#### JSX 전처리기 실행하기

- `src` 폴더를 만들고 다음 터미널 명령어를 실행
  - 이 명령어는 자동화 된 JSX 감시기를 실행

```bash
npx babel --watch src --out-dir . --presets react-app/prod
```

-  `src/like_button.js`라는 파일을 만들어주면, 감시기가 전처리 되어 브라우저와 호환되는 순수 JavaScript로 구성된 `like_button.js`를 생성 (.min.js도 생성)
- 덤으로 구형 브라우저와의 호환성 문제를 걱정할 필요 없이 클래스와 같은 모던 JavaScript 문법을 쓸 수 있게 함
-  npx와 npm의 차이
   -  npx는 필요한 앱을 다운받아 한번만 쓰고 삭제함
      - 불필요한 메모리 낭비가 없음
      - 항상 새로 다운받으므로 최신 버전(최신 버전 사용을 유도)

<br>

## Webpack

"여러가지의 파일을 한개로 결합하기 위해서 Webpack 이라는 도구를 사용"





## 툴체인: 새로운 React 앱 만들기

- 도움이 되는 몇 가지 인기 있는 React 툴체인
  - 많은 파일과 컴포넌트 스케일링
  - 서드파티 npm 라이브러리 사용
  - 일반적인 실수를 조기에 발견
  - CSS와 JS를 실시간으로 편집
  - 프로덕션 코드 최적화
- 이러한 문제를 경험하지 못했거나 아직 JavaScript 도구를 사용하는 것이 편하지 않다면, 

### 추천 툴체인

- 시작하는데, 별도의 환경설정이 필요 없는 툴체인들
- 툴체인이 필요하지 않을 수 있습니다

#### Create React App

- **React를 배우고 있거나** 아니면 **새로운 [싱글 페이지](https://ko.reactjs.org/docs/glossary.html#single-page-application) 앱**을 만들고 싶다면 [Create React App](https://ko.reactjs.org/docs/create-a-new-react-app.html#create-react-app).



- **서버 렌더링 Node.js 웹사이트를 만들고 있다면** [Next.js](https://ko.reactjs.org/docs/create-a-new-react-app.html#nextjs)을 시도해보세요..



- **고정적인 콘텐츠 지향적 웹사이트를 만들고 있다면** [Gatsby](https://ko.reactjs.org/docs/create-a-new-react-app.html#gatsby)를 시도해보세요..



- **컴포넌트 라이브러리** 혹은 **이미 있는 코드 베이스에 통합을 한다**면 [더 유연한 툴체인](https://ko.reactjs.org/docs/create-a-new-react-app.html#more-flexible-toolchains).

### 