# state와 props 

출처: https://www.boostcourse.org/web231/lecture/1387422?isDesc=false

## props

```js
import React, { Component } from "react";
import './App.css';

class Subject extends Component {
  render(){ // 클래스 안에 속한 메소드는 function 키워드 생략 가능  
    return (
      // 컴포넌트는 반드시 하나의 최상위 태그만 사용해야 함. 
      <header>
        <h1>WEB</h1>
        World Wide Web!
      </header>
    );
  }
}

class TOC extends Component { // Table Of Content (목차) 
  render(){
    return(
      // jsx라는 문법 덕분에 js 파일에 html 태그를 넣을 수 있음. 
      <nav>
        <ul>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ul>
      </nav>
    );
  }
}

class Content extends Component {
  render(){
    return(
      <article>
        <h2>HTML</h2>
        HTML is HyperText Markup Language.
      </article>
    );
  }
}

class App extends Component {
  render(){
    return (
      <div className="App">
         <Subject></Subject>
         <Subject></Subject>
         <TOC></TOC>
         <Content></Content>
      </div>
    );
  }
}

export default App; 
```

기존의 이 코드에서 Subject라는 태그는 언제나 같은 결과를 보여준다. 

![image](https://user-images.githubusercontent.com/68090939/178980447-11c91174-7279-43be-b7d3-8e14e632f210.png)

a 태그의 href 속성 값에 따라 연결되는 링크가 달라지는 것처럼, 컴포넌트에도 속성을 부여하여 그에 따라 다른 결과가 보이도록 할 수 있다! 

```js
import React, { Component } from "react";
import './App.css';

class Subject extends Component {
  render(){ 
    return (
      <header>
        <h1>{this.props.title}</h1> 
        {this.props.sub} 
      </header>
    );
  }
}

class TOC extends Component { 
  render(){
    return(
      <nav>
        <ul>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ul>
      </nav>
    );
  }
}

class Content extends Component {
  render(){
    return(
      <article>
        <h2>{this.props.title}</h2>
        {this.props.desc}
      </article>
    );
  }
}

class App extends Component {
  render(){
    return (
      <div className="App">
         <Subject title="WEB" sub="world wide web!"></Subject>
         <TOC></TOC>
         <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    );
  }
}

export default App; 
```

바로 이렇게 태그에 속성을 부여한 뒤에, [공식 문서](https://reactjs.org/docs/components-and-props.html)의 설명에 따라 `{this.props.title}` 이렇게 JSX에서 약속한 문법에 따라 태그의 속성을 참조하면 된다. 결국 html에서 속성이라 부르는 것을 리액트에서는 props라고 부른다고 보면 된다. 

이제 같은 태그라고 하더라도, 속성 값에 따라 다른 결과를 보여줄 수 있다! 

```js
class App extends Component {
  render(){
    return (
      <div className="App">
         <Subject title="WEB" sub="world wide web!"></Subject>
         <Subject title="React" sub="For UI"></Subject>
         <TOC></TOC>
         <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    );
  }
}
```

![image](https://user-images.githubusercontent.com/68090939/178981610-c0343d90-cedb-4c51-a5cc-a1cea3652fad.png)

## React Developer Tools

강의를 들을 때 중요한 것은, "어떻게 해야 저 강사로부터 최대한 빨리 독립할 수 있을까?"를 계속해서 고민하는 것이다! 

강사로부터 독립하기 위해 가장 중요한 도구는, **설명서를 볼 줄 아는 것과 현재 상태를 측정하고 분석하는 것**이다. 

그리고 이 두 가지 핵심을 촉진할 수 있는 굉장히 중요한 촉매가 **다른 사람에게 질문하고 또 검색하는 것**이라고 한다. 

![image](https://user-images.githubusercontent.com/68090939/178985330-6a297187-4476-40ee-8469-a3fe4e739293.png)

이 네가지를 스스로 할 수 있게 된다면, 우리는 강사로부터 독립한 것이다! 이 중에서 **현재 상태를 측정할 수 있는 도구인 React Developer Tools**를 설치해보자. 

![image](https://user-images.githubusercontent.com/68090939/178983009-7978d43b-e8c0-4a68-81a3-dfdd875a1e5f.png) 

![image](https://user-images.githubusercontent.com/68090939/178986477-4668cbc0-e278-44d4-b91d-ab4a4d8e5bdd.png)

![image](https://user-images.githubusercontent.com/68090939/178986696-6267316e-529a-470b-ad82-5bed5e2149e9.png)

이렇게 html로 보이던 컴포넌트를 React Developer Tools로 새로 생성된 **Components 탭으로 확인**해보면 웹 브라우저의 구조를 보다 쉽게 파악할 수 있다. 필요에 따라 속성 값을 바꿀 수도 있다.

![image](https://user-images.githubusercontent.com/68090939/178986809-8ae50dfa-3ca9-427a-9ed2-9c8a873c62c0.png)

## Component 파일로 분리하기 



## state

## key 

