# 리액트의 이벤트 

출처: https://www.boostcourse.org/web231/lecture/1387425?isDesc=false

## 이벤트 state, props, 그리고 render 함수 

**리액트에서는 props나 state 값이 바뀌면 해당되는 컴포넌트의 render 함수가 다시 호출되도록 약속되어 있다**. 또한 render 함수가 다시 호출되면 render 함수 하위에 있는 컴포넌트들의 render 함수도 호출된다. render 함수는 어떤 HTML을 그릴 것인가를 결정하기 때문에 **결국, props나 state 값이 바뀌면 그에 따라 화면이 다시 그려지게 된다.** 

## 클릭한 링크에 따라 모드 변경하기 

[소스 코드 확인하기](https://github.com/leeeha/react-app/commits/master) 

### welcome 모드 

![image](https://user-images.githubusercontent.com/68090939/179719868-bb4020af-0b44-4040-9d87-034ffa861532.png)

### read 모드 

TOC 컴포넌트에서 클릭한 항목에 따라 selected_content_id 값이 바뀌면서, Content 컴포넌트의 내용이 달라지는 걸 확인할 수 있다. 

![image](https://user-images.githubusercontent.com/68090939/179719983-60aa1b28-68ce-49a6-a1d7-fc88c261d3de.png)

![image](https://user-images.githubusercontent.com/68090939/179720801-c682d216-7953-4081-8ba4-4e344deadfce.png)

![image](https://user-images.githubusercontent.com/68090939/179720840-9a8fb06e-54c4-4677-b042-826aa5f1332a.png)

## 요약 

### props vs. state 

![image](https://user-images.githubusercontent.com/68090939/179938461-270675f8-377e-49d0-95e1-1bf9e2a3b7e1.png)

**props는 read-only인 반면에, state는 setState로 값을 변경할 수 있다.** 

우리 코드에서 <Content> 컴포넌트를 사용하는 쪽에서는 title이라는 props를 통해 값을 주입할 수 있었다. 하지만, <Content> 내부에서 props 값을 직접 바꾸려고 하면 에러가 발생한다. 

```js
import React, { Component } from "react"; 

class Content extends Component {
    render(){
      this.props.title = 'hi' 
      return(
        <article>
          <h2>{this.props.title}</h2>
          {this.props.desc}
        </article>
      );
    }
}

export default Content;
```

![image](https://user-images.githubusercontent.com/68090939/179940554-ac846a9e-33d0-44c3-87ae-3d63298fd916.png) 
  
이처럼 props는 컴포넌트 밖에서만 수정할 수 있고, **컴포넌트 내부에서는 수정할 수 없는 read-only의 특징**을 갖고 있다. 

**내부적으로 필요한 데이터나 어떤 상태들은 state로 관리해야 한다.** props와 state 모두 render() 함수를 호출하기 때문에 props와 state 변경을 통해 UI를 업데이트 할 수 있다. 
  
![image](https://user-images.githubusercontent.com/68090939/179940996-f78b81ba-1431-4606-a0cf-7d61f39d666d.png)
  
위 그림을 통해 알 수 있는 것은, **외부에서는 props를 통해 컴포넌트를 제어하고, 컴포넌트 내부에서는 state를 사용한다**는 것이다. 즉, 사용자의 props와 구현자의 state가 있고, 컴포넌트는 props와 state의 영향에 따라서 어떤 상태를 갖게 되는 것이다. 그 상태가 실제 웹 브라우저의 HTML, 다른 말로 DOM이라는 것에 영향을 줘서 UI가 그려진다. 
  
![image](https://user-images.githubusercontent.com/68090939/179942349-fe6aafa4-3ca3-4f13-8171-304628b7936b.png)

위 그림에서 리덕스가 없는 순수한 리액트를 다룰 때를 보자.
  
우리 코드에서는 상위 컴포넌트가 <App>, 하위 컴포넌트가 <Subject>, <TOC>, <Content> 에 해당한다. 상위 컴포넌트가 하위 컴포넌트에 값을 전달할 때는 props를 이용한다. 반대로, 하위 컴포넌트가 상위 컴포넌트의 값을 바꾸고 싶을 때는 이벤트를 이용할 수 있다. 
  
**App.js의 <TOC> 컴포넌트** 
  
```js
<TOC 
  // TOC.js의 render() 함수에서 onChangePage 함수를 실행시킴. 
  onChangePage={function(id){
    this.setState({
      mode:'read',
      selected_content_id:Number(id) // 문자열에서 숫자 타입으로 변환 필수
    });
  }.bind(this)}
  data={this.state.contents}>
</TOC>
```
  
<TOC> 컴포넌트 내부 
  
```js
import React, { Component } from "react";

class TOC extends Component {
    render(){
        var lists = [];
        var data = this.props.data;
        var i = 0;
        while(i < data.length){
            lists.push(
            <li key={data[i].id}>
                <a 
                    href={"/content/"+data[i].id}
                    // bind 함수의 인자로 id를 직접 전달할 수도 있고 
                    // data-id 라는 속성 값을 이용할 수도 있음.
                    data-id={data[i].id} 
                    onClick={function(e){
                        e.preventDefault();
                        this.props.onChangePage(e.target.dataset.id);
                    }.bind(this)}
                >{data[i].title}</a>
            </li>);
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

이처럼 하위 컴포넌트 <TOC>는 상위 컴포넌트 <App>의 상태를 바꾸기 위해 onChangePage 라는 이벤트 함수를 호출한다. 
  
  
