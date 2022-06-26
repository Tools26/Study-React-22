# Setup for tutorial
## 개발환경
1. 브라우저
2. Local 개발 환경
   1. node를 설치한다. 이때, lts 버전이나 최신 버전을 다운받는걸 추천함. v16.13.2
   2. 
   ![image](https://user-images.githubusercontent.com/72017202/175800410-e62ea9eb-7a01-4834-a169-51b04898f7b5.png)

   3. 터미널을 열고 아래 명령어를 입력한다.
   4. npx create-react-app 폴더이름
   5. npm start로 동작함

![image](https://user-images.githubusercontent.com/72017202/175800488-b0da4d9e-32e4-4b32-89f3-515d36c7e527.png)

   ![image](https://user-images.githubusercontent.com/72017202/175800458-95edfc3e-3d7a-4f19-9989-382c36797b7f.png)


# Tutorial
## what is the react
React는 UI를 구축하기 위한 효유적이며 유연한 JS Library이다.
또한, Component 라는 코드 조각들을 이용하여 복잡한 UI를 구성할 수 있다.

local 환경에서 index.js 에 tutorial 소스를 넣고 저장을 한다.
```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
// import App from './App';
import reportWebVitals from './reportWebVitals';
// JavaScript 클래스 에서는 super하위 클래스의 생성자를 정의할 때 항상 호출해야 합니다
//  있는 모든 React 구성 요소 클래스 는 호출 constructor로 시작해야 합니다 .super(props)

class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 1,
    };
  }
  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}

class Board extends React.Component {
  renderSquare(i) {
    return <Square />;
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}

class Game extends React.Component {
  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}

// ========================================

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Game />);
```
![image](https://user-images.githubusercontent.com/72017202/175801260-44da3794-5c86-4a18-87b1-8b5c078770ca.png)
