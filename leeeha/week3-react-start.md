# 웹 프론트엔드 입문 (리액트, 리덕스) 

https://www.boostcourse.org/web231/lecture/1380895?isDesc=false

---

# 리액트의 시작 

## 개발 환경 구축하기 

https://www.boostcourse.org/web231/lecture/1380892?isDesc=false

- https://reactjs.org/docs/create-a-new-react-app.html#create-react-app
- https://github.com/facebook/create-react-app

npm 설치 -> create react app 설치 -> 개발 환경 세팅 

cf) "npm" 은 Node.js 기술로 만들어진 여러 앱들을 우리가 커맨드(명령어) 환경에서 아주 손쉽게 설치할 수 있도록 도와주는 도구이다. 쉽게 말하자면, Node.js 계의 앱스토어 또는 구글 플레이어 역할을 하는 소프트웨어라고 할 수 있다. 

## npm과 create-react-app 설치 

`npm install -g create-react-app` 

"npm" 과 "npx" 의 차이는 npm이 프로그램을 설치하는 프로그램이라면, npx는 프로그램을 임시로 설치해서 딱 한번만 실행시키고 지우는 프로그램이다. npx의 장점은 컴퓨터의 공간을 낭비하지 않으며, 실행할 때마다 다운로드를 새로 받기 때문에 항상 최신 상태라는 것이다. 앞으로의 실습을 위해서는 그냥 npm을 설치하여 사용할 것이다.

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

public 디렉토리 안에 있는 index.html 파일을 확인해보자! 

![image](https://user-images.githubusercontent.com/68090939/177769390-a186f0d2-b678-45d2-b2fc-7f977dac13b1.png)

리액트로 만든 컴포넌트 (사용자 정의 태그)는 id가 root인 태그 안에 들어가도록 create-react-app은 약속하고 있다! 

그러면 id가 root인 태그 안쪽에 들어가는 컴포넌트들은 어떤 파일을 수정해서 만들 수 있을까? 

"src" 디렉토리 안에 있는 파일들을 수정하면 된다! 그 중에서 index.js 파일을 살펴보자. 

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

여기서 root가 의미하는 건 index.html에서 봤던 id가 root인 태그이다. 그리고 <App />가 의미하는 건 바로 리액트를 통해 만든 사용자 정의 태그, 즉 컴포넌트이다! 

`import App from './App';` 

create-react-app이 샘플로 만든 <App /> 컴포넌트의 실제 구현은 import를 통해 불러온 src 안의 App.js 파일이다. 

![image](https://user-images.githubusercontent.com/68090939/177771238-39dd6985-8822-461d-b6ca-c045515c634b.png)
















