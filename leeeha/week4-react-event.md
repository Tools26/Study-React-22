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

