## React Native 소개 및 개발 환경 구축



### Intro

리액트 네이티브는

- 페이스북에서 만든 오픈소스 모바일 응용 프로그램
- 네이티브 앱 개발을 위한 자바스크립트 프레임워크
- 단 하나의 코드 개발로 iOS 와 안드로이드에서 동일하게 동작 시킬 수 있는 API

리액트 네이티브는 자바스크립트를 기본 언어로 쓰기 때문에
Java나 Kotlin 언어에 의존하는 안드로이드 네이티브 앱, 
혹은 Swift 언어에 의존하는 iOS 네이티브 앱 개발 보다
진입 장벽이 낮고 훨씬 쉽다는 장점을 가짐

### React Native 기본 원리

React Native는 모바일 웹앱, 하이브리드 앱이 아닌 네이티브 앱을 개발하기 위한 오픈 소스 프레임워크

IOS 네이티브 앱은 Object C 혹은 Swift 코드를 IOS 플랫폼에 타겟팅해주는 컴파일러가 존재하고,
안드로이드의 경우는 Java나 코틀린을 안드로이드 플랫폼에 타겟팅해주는 컴파일러가 존재한다.

하위 레벨 단에서 보면, 크로스 플랫폼인 React Native는 단지 자바스크립트 개발 코드를 OS플랫폼에 타겟팅해준다고 생각하면 된다.

로우 레벨 단에서 본다면, React Native에서는 앱을 빌드할 때, 앱의 전체 로직을 가지고 있는 JS Bundle을 만들고, 그 번들을 각 플랫폼에 심어주게 된다. JS Bundle은 JS Thread에 의해 실행이 되는데, 각 플랫폼에서 앱을 실행하기 위한 Native Thread는 JS Thread와 직접 커뮤니케이션할 수가 없고, React Native에서 제공하는 Bridge에 의해 상호작용을 한다. 

React Native로 각 Native 앱 제작이 가능한 이유는 이 Bridge 라는 개념을 제공하기 때문. 

=> 자바스크립트 코드 작성, React Native API사용, JS Bundle 만드는 법이 필요

### Expo CLI vs. React Native CLI

JS Bundle을 만들고 앱을 실행시키는 방법에는 두 가지가 있음

| Expo CLI                                                     | React Native CLI                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pros                                                         | Pros                                                         |
| 개발 환경 구축 용이<br/>실제 개발이 쉽고 편함                | Expo로는 접근하지 못하는 Native 기능에 접근 가능 (Native 모듈 사용 자유도높음)<br />원하는 언어로 추가 작성 가능(Custom<br/>Native 모듈 사용 가능) <- bridge<br />필요한 기능이 있는 경우 모듈을 직접 제작 가능 |
| Cons                                                         | Cons                                                         |
| OS Layer와 직접 상호작용 불가능 (Java,Kotlin, obj-C, Swift로 추가 작성 불가)<br/>Expo에서 제공해주는 모듈만 사용 가능<br/>Expo Client에서는 잘 동작하지만 실제 Simulator 및 단말기에서 잘 동작하지 않을 수 있음<br/>개발 관점에서의 자유도 낮음 | OS Layer와 직접적인 상호작용 가능<br/>초기 개발환경 구축 및 실제 앱 개발 시 다소 시간 소요<br />Mac일 경우에만, iOS / Android 지원 |

Expo CLI를 사용하게 되면 처음에는 편할 수 있지만 개발의 자유도도 떨어지고 앱개발보다 third party library를 배우는 느낌이 강하기 때문에 React Native CLI를 사용

### Installation 01

V nvm (Node Version Manager)
V node.js
V npm (Node Package Manager)
V Android Studio
V JAVA
V Android Studio
V ХCode
V Visual Studio Code
V Android Studio
V СосoаPod
V React Native CLI

- nvm : node.js의 버전 관리자인 동시에 node.js를 설치하는 툴. node.js를 직접 설치할 수 도 있지만 os에 특정 버전의 node.js를 설 치하면 여러 버전의 node.js를 설치해야할 경우 대응이 불가능. nvm은 하나의 시스템

### Installation 02

