# state와 props 

출처: https://www.boostcourse.org/web231/lecture/1387422?isDesc=false

* [props](#props)
* [React Developer Tools](#react-developer-tools)
* [Component 파일로 분리하기](#component-파일로-분리하기)
* [state 소개](#state-소개)
* [state 사용](#state-사용)

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

a 태그의 href 속성 값에 따라 연결되는 링크가 달라지는 것처럼, **컴포넌트에도 속성을 부여하여 그에 따라 다른 결과가 보이도록** 할 수 있다! 

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

바로 이렇게 컴포넌트에 원하는 속성을 부여한 다음에 [공식 문서](https://reactjs.org/docs/components-and-props.html)의 설명에 따라 JSX의 문법으로 컴포넌트의 속성을 참조하면 된다. 결국 html에서의 속성이 리액트에서는 props인 것이다. 이제 같은 컴포넌트라고 하더라도, 그 속성 값에 따라 다른 결과를 보여줄 수 있다! 

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

이를 위해 가장 중요한 도구는, **설명서를 볼 줄 아는 것과 현재 상태를 측정하고 분석하는 것**이다. 

그리고 이 두 가지 핵심을 촉진할 수 있는 굉장히 중요한 촉매가 **다른 사람에게 질문하고 또 검색하는 것**이다. 

![image](https://user-images.githubusercontent.com/68090939/178985330-6a297187-4476-40ee-8469-a3fe4e739293.png)

이 네가지를 스스로 할 수 있게 된다면, 우리는 강사로부터 독립한 것! 

이 중에서 **현재 상태를 측정할 수 있는 도구인 React Developer Tools**를 설치하고 사용해보자. 

![image](https://user-images.githubusercontent.com/68090939/178983009-7978d43b-e8c0-4a68-81a3-dfdd875a1e5f.png) 

![image](https://user-images.githubusercontent.com/68090939/178986477-4668cbc0-e278-44d4-b91d-ab4a4d8e5bdd.png)

![image](https://user-images.githubusercontent.com/68090939/178986696-6267316e-529a-470b-ad82-5bed5e2149e9.png)

이렇게 html로 보이던 컴포넌트를 React Developer Tools로 새로 생성된 **Components 탭으로 확인**해보면 컴포넌트 이름으로 웹 브라우저를 분석할 수 있게 된다. 그리고 필요에 따라 그 속성 값을 바꿀 수도 있다. 

![image](https://user-images.githubusercontent.com/68090939/178986809-8ae50dfa-3ca9-427a-9ed2-9c8a873c62c0.png)

## Component 파일로 분리하기 

https://github.com/leeeha/react-app/commit/72eb6ebfa2f897c4e2af933b7902f795ba3d8f05

모든 컴포넌트들을 App.js 파일 하나에 전부 정의하면 유지보수가 힘들기 때문에, 각 컴포넌트마다 파일을 따로 생성하여 정의할 수 있다. 그리고 export, import를 통해 서로 다른 파일 간에 참조가 가능하도록 만들어준다. 

## state 소개 

어떤 제품이든 **사용자의 입장**과 그것을 구현하는 **구현자의 입장**이 있다.

사용자의 입장에서 장치의 버튼 클릭, 화면 터치 등의 동작으로 제품을 조작하는 것을 '유저 인터페이스' 라고 부른다.

리액트에서는 "props"가 바로 사용자가 제품을 조작할 수 있게 하는 장치 같은 것이다. 그리고 제품을 만드는 사람은 제품의 내부적인 구현과 다양한 상태들을 사용하기 위한 여러 장치를 갖고 있다. 이를 비유적으로 "state"라고 볼 수 있다. 

즉, **"props"는 사용자가 컴포넌트를 조작할 수 있게 하는 장치**이고, **"state"는 props의 값에 따라 내부적으로 기능을 구현하기 위한 여러 데이터들**이라 볼 수 있다. 

![image](https://user-images.githubusercontent.com/68090939/179201439-89643971-836b-4922-95ed-4ef19aaf259b.png) 

**리액트로 만든 컴포넌트가 좋은 부품이 되려면, props와 state가 철저하게 분리되어 있어야 한다.** 사용자와 구현자를 서로 격리시켜서 양쪽의 편의성을 도모하는 것이 좋은 부품을 만드는 데 핵심이 된다. 

이제 **좀더 복합적으로 다양한 일을 하는 컴포넌트를 만들기 위해 필요한 "state"에 대해 알아보자.** 이 과정에서 우리는 "props"도 더 잘 이해하게 될 것이다. 

## state 사용 

**App.js** 

```js
import React, { Component } from "react";
import TOC from "./components/TOC"
import Subject from "./components/Subject"
import Content from "./components/Content"
import './App.css';

class App extends Component {
  // render() 보다 먼저 실행되어 초기화를 담당하는 생성자 
  constructor(props){
    // 부모 클래스의 생성자를 먼저 호출해주지 않으면, this에 접근 불가! 
    super(props);
    this.state = {
      subject:{title:'WEB', sub:'World Wide Web!'}, 
      // 속성이 가진 데이터가 여러 개일 때는 배열 사용
      contents:[
        {id:1, title:'HTML', desc:'HTML is for information'},
        {id:2, title:'CSS', desc:'CSS is for design'},
        {id:3, title:'JavaScript', desc:'JavaScript is for interaction'}
      ]
    }
  }

  render(){
    return (
      <div className="App">
         <Subject
            // props의 데이터를 state에서 가져옴. 
            title={this.state.subject.title}
            sub={this.state.subject.sub}>
          </Subject>

          <TOC 
            // contents에 담긴 배열 정보를 TOC 컴포넌트에 주입하기 
            data={this.state.contents}>
          </TOC>

         <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    );
  }
}

export default App; 
```

<br>

**TOC.js** 

```js
import React, { Component } from "react";

class TOC extends Component {
    render(){
        var lists = [];
        var data = this.props.data; // TOC 컴포넌트의 props 참조 
        var i = 0;
        while(i < data.length){ 
            // 여러 항목을 자동으로 생성할 때는, 각 항목이 key 값을 가져야 한다. 
            lists.push(<li key={data[i].id}><a href={"/content/"+data[i].id}>{data[i].title}</a>
            </li>)
            i++;
        }

        return(
            <nav>
                <ul>
                    {lists}
                </ul>
            </nav>
        );
    }
}

export default TOC;
```

![image](https://user-images.githubusercontent.com/68090939/179208431-336be1b5-5832-4879-bc72-db522126cd76.png)

이 에러를 해결하려면 **리스트의 각 항목이 key 값을 통해 서로 구분될 수 있도록**, li 태그에 key 속성을 부여해줘야 한다. 

`lists.push(<li key={data[i].id}><a href={"/content/"+data[i].id}>{data[i].title}</a></li>)`

<br> 

![image](https://user-images.githubusercontent.com/68090939/179209485-8e3c3695-5c12-4717-a01c-810e02ef530b.png)

이처럼 **상위 컴포넌트 \<App>의 내부 state를 \<TOC>에 주입하면, \<TOC> 내부 데이터가 \<App>에 의해 자동으로 바뀌도록 만들 수 있다.** \<App>의 입장에서는 \<TOC>가 내부적으로 어떻게 동작하는지 알 필요가 없어진다! 

