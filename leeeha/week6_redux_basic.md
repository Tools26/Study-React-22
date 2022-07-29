# 목차 

- [리덕스가 없다면](#리덕스가-없다면)
- [리덕스를 사용하면](#리덕스를-사용하면)
- [리덕스의 장점](#리덕스의-장점)

# 리덕스가 없다면 

- 자료 출처: https://www.boostcourse.org/web231/lecture/1387448?isDesc=false 
- 전체 소스 코드 확인: https://github.com/leeeha/redux

<img width="500" src="https://user-images.githubusercontent.com/68090939/181704756-8f111772-f8fe-414d-bbb6-d555a36d9086.png"/>

<img width="500" src="https://user-images.githubusercontent.com/68090939/181704792-d3705d67-a7e5-4659-bd4c-7f590627fee7.png"/>

<img width="500" src="https://user-images.githubusercontent.com/68090939/181704826-4cc9105e-bf74-4b99-9121-b1040dd4ffe3.png"/> 

## without-redux.html 

```html
<!DOCTYPE html>
<html>
    <body>
        <style>
            .container{
                border: 5px solid black;
                padding: 10px;
                margin-top: 10px;
            }
        </style>
    
        <div id="red"></div>
        <div id="green"></div>
        <div id="blue"></div>
    
        <script>
            function red(){
                document.querySelector('#red').innerHTML = `
                    <div class="container" id="component_red">
                        <h1>red</h1> 
                        <input type="button" value="fire" onclick="
                        document.querySelector('#component_red').style.backgroundColor = 'red';
                        document.querySelector('#component_green').style.backgroundColor = 'red';
                        document.querySelector('#component_blue').style.backgroundColor = 'red';
                        ">
                    </div> 
                `;
            }
            red(); // 호출을 해줘야지! 

            function green(){
                document.querySelector('#green').innerHTML = `
                    <div class="container" id="component_green">
                        <h1>green</h1> 
                        <input type="button" value="fire" onclick="
                        document.querySelector('#component_red').style.backgroundColor = 'green';
                        document.querySelector('#component_green').style.backgroundColor = 'green';
                        document.querySelector('#component_blue').style.backgroundColor = 'green';
                        ">
                    </div> 
                `;
            }
            green(); // 호출을 해줘야지! 

            function blue(){
                document.querySelector('#blue').innerHTML = `
                    <div class="container" id="component_blue">
                        <h1>blue</h1> 
                        <input type="button" value="fire" onclick="
                        document.querySelector('#component_red').style.backgroundColor = 'blue';
                        document.querySelector('#component_green').style.backgroundColor = 'blue';
                        document.querySelector('#component_blue').style.backgroundColor = 'blue';
                        ">
                    </div> 
                `;
            }
            blue(); // 호출을 해줘야지! 

        </script>
    </body>
</html>
```

# 리덕스를 사용하면 

## with-redux.html 

```html
<!DOCTYPE html>
<head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.2.0/redux.js"></script>
</head>
<body>
    <style>
        .container{
            border: 5px solid black;
            padding: 10px;
            margin-top: 10px;
        }
    </style>

    <div id="red"></div>
    <div id="green"></div>
    <div id="blue"></div>

    <script>
// 이전의 state와 dispatch로부터 받은 action 객체를 참조하여 
// 새로운 state 값을 리턴하는 reducer 함수  
function reducer(state, action){
    console.log(state, action); 

    // 초기 state 값 설정 
    if(state === undefined){
        return {color:'yellow'}  
    }

    // 원본 state 대신 복사본을 만들어서 변경하자! 
    // redo, undo로 시간여행 할 수 있는, 예측 가능한 리덕스를 만들기 위해  
    var newState; 

    if(action.type === 'CHANGE_COLOR'){
        // reducer 함수가 실행될 때마다 서로 완전히 독립된 복사본들이 리턴됨. 
        newState = Object.assign({}, state, {color: action.color});
    }

    return newState; 
}

// reducer 함수를 주입하여 새로운 store 생성 
var store = Redux.createStore(reducer);

function red(){ 
    // store에 저장된 state 값에 따라 UI 변경하기 
    var state = store.getState();
    document.querySelector('#red').innerHTML = `
        <div 
            class="container"
            id="component_red" 
            style="background-color:${state.color}">

            <h1>red</h1> 

            <input type="button" value="fire" onclick="
                store.dispatch({type:'CHANGE_COLOR', color:'red'});
            ">
        </div> 
    `;
}

// store에 render 함수를 구독해두면
// state가 바뀔 때마다 render 함수가 호출되어 UI에 반영됨. 
store.subscribe(red);
red();

function green(){
    var state = store.getState();
    document.querySelector('#green').innerHTML = `
        <div 
            class="container"
            id="component_green" 
            style="background-color:${state.color}">

            <h1>green</h1> 

            <input type="button" value="fire" onclick="
                store.dispatch({type:'CHANGE_COLOR', color:'green'});
            ">
        </div> 
    `;
}
store.subscribe(green);
green();

function blue(){
    var state = store.getState();
    document.querySelector('#blue').innerHTML = `
        <div 
            class="container"
            id="component_blue" 
            style="background-color:${state.color}">

            <h1>blue</h1> 

            <input type="button" value="fire" onclick="
                store.dispatch({type:'CHANGE_COLOR', color:'blue'});
            ">
        </div> 
    `;
}
store.subscribe(blue);
blue();

    </script>
</body>
</html>
```

# 리덕스의 장점 

## 중앙 집중적인 상태 관리로 각 컴포넌트 간의 의존성 분리 

리덕스가 없을 때의 코드는 서로 강력하게 의존하고 있었다. 

이전의 blue() 함수는 red와 green 컴포넌트를 알고 있기 때문에 red()와 green()을 갑자기 지워버리면 blue()는 에러를 발생시킨다.

그리고 만약에 새로운 컴포넌트가 추가되면, 기존에 있던 컴포넌트 전체를 업데이트 해야 하는 문제가 발생한다.

그런데, **리덕스**라는 중개자를 통해 우리가 **상태를 중앙 집중적으로 관리**하게 되면, 

각각의 부품들은 상태가 바뀌었을 때 **상태가 바뀌었다는 action을 store에 dispatch 시켜주기만 하면 된다.** 

그리고 상태 변화에 따라 **자신의 UI가 어떻게 변화해야 하는지에 대한 코드를 store에 구독**시켜놓으면, 상태가 바뀔 때마다 해당 코드가 실행되며 UI가 업데이트 된다. 

이처럼 리덕스를 사용하면 blue 라는 부품은 green이나 red 라는 부품을 몰라도 된다. **그저 자신의 일에만 집중하면 된다.**

프로그램을 작성하는 우리 입장에서도 blue 라는 컴포넌트를 만들 때는 blue 컴포넌트에만 집중하면 되니까 훨씬 편하다! 

## 시간 여행 (Redux DevTools)

https://github.com/zalmoxisus/redux-devtools-extension

**리덕스의 시간여행 기능은 웹 서버를 통해 서비스 되는 웹 페이지에서만 사용할 수 있다!** 

그래서 [이 포스트](https://writingdeveloper.tistory.com/305)를 참고하여 Web Server for Chrome 이라는 앱을 간단히 설치하고, html 파일이 localhost 환경에서 실행될 수 있게 만들었다. 

![image](https://user-images.githubusercontent.com/68090939/181714271-2fc23a29-3a12-4e4b-a5b2-6537ee711052.png)

그러면 이렇게 Redux DevTools를 이용하여 상태 변화를 추적할 수 있게 된다! 정말 신기한 기능 👍👍 

나중에 내가 만든 웹 페이지가 더 복잡해지면, 이 도구가 아주 유용하게 사용될 거 같다. 








