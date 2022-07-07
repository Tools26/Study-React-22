# 웹 프론트엔드 입문 (리액트, 리덕스) 

강의 자료: https://www.boostcourse.org/web231/lecture/1380895?isDesc=false

## React란?

"React"는 facebook.com의 UI를 더 잘 만들기 위해서 **페이스북에서 만든 Javascript UI 라이브러리**입니다. 

## 컴포넌트 

웹사이트는 매우 빠른 속도로 복잡해집니다. 정보가 조금만 증가해도 그 정보를 표현하는 html은 기하급수적으로 복잡해집니다. 예로 페이스북을 보겠습니다. 눈으로 보기에는 별로 복잡하지 않을 것 같은 이 웹 사이트도 사실 HTML 코드가 굉장히 복잡합니다. 

이런 복잡성 속에서 허우적대고있는 사람이라면 엄청난 절망감을 가질 것입니다. 그 절망감이 충분히 성숙한 사람은 어떤 꿈을 꾸게 될까요? 이 복잡한 코드를 바깥쪽으로 빼내서 정리정돈하고 싶은 욕심이 생기지 않을까요? 

**사용자 정의 태그를 만들어주는 여러가지 기술이 있는데 리액트 역시도 그런 기술 중에 하나입니다. 그리고 리액트에서는 이렇게 사용자가 정의해서 태그를 만드는 것을 "사용자 정의 태그"라고 하지 않고 "컴포넌트" 라고 부릅니다.**

## 컴포넌트의 기능

컴포넌트를 작성하면 **가독성**을 획기적으로 높일 수 있습니다.

또한 **재사용성**이 높아진다는 중요한 효과도 갖게 됩니다.

만약 top.html이란 파일에서 버그가 있거나 개선을 해야되는 경우에도 top.html의 변경된 내용이 이 파일을 사용하고 있는 모든 태그들에서 동시 다발적으로 업데이트가 일어납니다. 다시 말해서 **유지보수**가 훨씬 더 편리해진다는 폭발적인 효과를 제공해줍니다.

지금부터 **컴포넌트를 중심으로 웹 애플리케이션 UI를 만드는 방법**을 알아봅시다. 

---

# 리액트의 시작 

## 개발 환경 구축 

https://www.boostcourse.org/web231/lecture/1380892?isDesc=false

- https://reactjs.org/docs/create-a-new-react-app.html#create-react-app
- https://github.com/facebook/create-react-app

npm 설치 -> create react app 설치 -> 개발 환경 세팅 

cf) "npm" 은 **Node.js 기술로 만들어진 여러 앱들을 우리가 커맨드(명령어) 환경에서 아주 손쉽게 설치할 수 있도록 도와주는 도구**이다. 쉽게 말하자면, **Node.js계의 앱스토어 또는 구글 플레이어 역할을 하는 소프트웨어**라고 말할 수 있다.  

## npm과 create-react-app 설치 

`npm install -g create-react-app` 

"npm" 과 "npx" 의 차이는 **npm이 프로그램을 설치하는 프로그램**이라면, **npx는 프로그램을 임시로 설치해서 딱 한번만 실행시키고 지우는 프로그램**이다. 

npx의 장점은 컴퓨터의 공간을 낭비하지 않으며, 실행할 때마다 다운로드를 새로 받기 때문에 항상 최신 상태라는 것이다. 앞으로의 실습을 위해서는 그냥 npm을 설치하여 사용할 것이다. 

`cd [현재 디렉토리 위치]`

`create-react-app .`

![image](https://user-images.githubusercontent.com/68090939/177764407-4e87b347-97c7-46dc-bb04-d3af4a87e263.png)

바탕화면의 react-app이라는 디렉토리에 개발환경 구축 완료! 

## VSCode에서 샘플 웹앱 실행해보기 

`npm run start` 

```
Windows PowerShell
Compiled successfully!

You can now view react-app in the browser.       

  Local:            http://localhost:3000        
  On Your Network:  http://192.168.56.1:3000     

Note that the development build is not optimized.
To create a production build, use npm run build. 

webpack compiled successfully
```

![image](https://user-images.githubusercontent.com/68090939/177764760-dafda9eb-a8d4-4725-aa84-13774a5abe7b.png)

이 앱은 react기술을 이용해서 만든 웹앱이며, "create-react-app"이 가장 최소한의 앱을 미리 구현해서 보여주는 것이다!

실행을 종료하고 싶을 때는 terminal에서 "ctrl + C"를 누르면 된다. 

![image](https://user-images.githubusercontent.com/68090939/177765476-e37e9be7-d7c5-4a73-b105-584d766f305a.png)

---

# 리액트 맛보기 

## 리액트의 디렉토리 구조 이해하기

### JavaScript 파일 수정하기 

먼저 "public" 디렉토리 안에 있는 index.html 파일을 확인해보자! 

![image](https://user-images.githubusercontent.com/68090939/177769390-a186f0d2-b678-45d2-b2fc-7f977dac13b1.png)

**리액트로 만든 컴포넌트 (사용자 정의 태그)는 id가 root인 태그 안에 들어가도록 create-react-app은 약속하고 있다! **

그러면 id가 root인 태그 안쪽에 들어가는 컴포넌트들은 어떤 파일을 수정해서 만들 수 있을까? 바로 "src" 디렉토리 안에 있는 파일들을 수정하면 된다! 그 중에서 index.js 파일을 살펴보자! 

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App /> 
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

여기서 `root`가 의미하는 건 index.html에서 봤던 **id가 root인 태그**이다. 그리고 `<App />`가 의미하는 건 바로 리액트를 통해 만든 사용자 정의 태그, 즉 **컴포넌트**이다! 

`import App from './App';` 

**create-react-app이 샘플로 만든 <App /> 컴포넌트의 실제 구현은 import를 통해 불러온 src 안의 App.js 파일인 것이다!**

![image](https://user-images.githubusercontent.com/68090939/177771238-39dd6985-8822-461d-b6ca-c045515c634b.png) 

### CSS 파일 수정하기 

index.js 파일을 다시 살펴보면, `import './index.css';` 이 부분을 볼 수 있다. 즉, index.css 파일에서 css 코드를 수정할 수 있다. 

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App /> 
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

![image](https://user-images.githubusercontent.com/68090939/177773421-4aebadd8-067b-4271-b7d5-3cac94115412.png)

App.js 파일을 다시 보면 App.css 파일을 import 하고 있다는 것도 알 수 있다. 

```js 
import React, { Component } from "react";
import './App.css';

class App extends Component {
  render(){
    return (
      <div className="App">
         Hello, React!!!!!
      </div>
    );
  }
}

export default App; 
```

### 배포 (deploy) 



### 리액트가 없다면 

## 리액트의 컴포넌트 만들기 


















