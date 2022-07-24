# 리덕스란 무엇인가? 

https://www.boostcourse.org/web231/lecture/1387443?isDesc=false

# 리덕스의 동작 방식 

## state와 render의 관계 

리덕스의 핵심은 **"store"** 라는 것이다. **은행**이라고 비유적으로 생각해도 좋다. 

store 라는 것은 말그대로 **정보가 저장되는 곳**이다. store 안에는 "state" 라는 실제 정보가 저장된다. 이때 중요한 것은 **절대로 state에 직접 접근해서는 안 된다**는 것이다. 항상 무언가를 통해서 접근해야 한다! 

store를 만들 때 가장 먼저 해야 하는 것은 reducer 라는 함수를 만들어서 인자로 공급해주는 것이다. 

![image](https://user-images.githubusercontent.com/68090939/180643711-629a833b-0706-4ce6-a728-b602405c011a.png)

위의 코드처럼 `Redux.createStore(reducer);` 라고 하면 store가 생성된다. **store를 생성할 때 꼭 넣어줘야 하는 인자가 "reducer"인데, 이것은 함수이다.** 

![image](https://user-images.githubusercontent.com/68090939/180643945-fb2398e6-8f9d-4e08-91d3-ad855abe71b0.png) 

또 하나 중요한 것은 **"render"** 라는 것이다. 위의 그림을 보면, render는 store 안쪽에 있지 않다. 즉, 리덕스와는 상관없이 **UI를 만들어주는 역할을 하는 우리가 작성해야 할 코드**이다. 

![image](https://user-images.githubusercontent.com/68090939/180643966-48b5fae5-fbbb-4837-97dc-20cb871f314f.png) 

아까 말했듯이 store에 있는 state에 직접 접근하는 것은 금지되어 있기 때문에, **store 앞단에 일종의 은행 창구 직원 역할을 하는 3가지의 중요한 함수들**이 있다. 

이 함수들과 우리가 작성한 render가 서로 어떻게 협력하여 어플리케이션을 만드는지 살펴보자. 

![image](https://user-images.githubusercontent.com/68090939/180644157-a4d5e186-0975-4a9b-be9e-3fade951e7d9.png)

![image](https://user-images.githubusercontent.com/68090939/180644164-8cae1571-5f0d-48e6-8876-3ceb83a1982d.png) 

render는 getState를 통해 state의 값을 가져오고 그와 관련된 동작을 실행하여, 오른쪽 그림과 같은 **state를 반영한 UI를 그리게 된다.** 

언제나 store의 state 값이 바뀔 때마다 render 함수를 호출할 수 있다면 얼마나 좋을까? 그러면, 신경쓸 것없이 **render 함수만 잘 만들면 알아서 state 값이 바뀔 때마다 UI가 갱신**되지 않을까? 그때 사용하는 것이 바로 구독이라는 뜻의 **subscribe** 이다. 

render 함수를 subscribe에 등록할 때는 `store.subscribe(render)` 와 같은 형식으로 코드를 작성할 수 있다. **subscribe에 render 함수를 등록하면 state 값이 바뀔 때마다 render 함수가 호출되면서 UI가 새롭게 갱신된다.** 

## action과 reducer 

Submit 버튼을 눌러 추가된 글 목록이 갱신될 때, 리덕스가 어떻게 동작하는지 그 원리를 알아보자! 처음이라 어렵게 느껴지지만 일단 전체적인 큰 흐름을 먼저 살펴보고, 앞으로 직접 사용을 많이 해보면서 익숙해지면 된다! 겁먹지 말자! 

![image](https://user-images.githubusercontent.com/68090939/180644877-5d5bf356-9255-4442-8a7c-f5471d69910d.png)

Submit 버튼에 설정되어 있는 onsubmit 라는 이벤트가 발생하면, store의 dispatch에게 action이라는 객체를 하나 전송하게 된다. 여기서 가장 중요한 건, type이 'create'라는 것이다. 

dispatch는 두 가지 역할을 한다. 첫번째는 reducer를 호출해서 state 값을 변경시키는 것이고, 두번째는 subcribe로 render 함수를 호출하여 화면을 갱신하는 것이다. 

우선 dispatch가 reducer를 어떻게 다루는지 먼저 살펴보자. 

dispatch가 reducer를 호출할 때 **현재의 state 값과 action 데이터를 전달**한다. 

![image](https://user-images.githubusercontent.com/68090939/180645176-06316120-ebd3-4430-9ce1-662521537099.png)

위에 보이는 reducer 함수의 매개변수에는, dispatch의 인자로 전달한 **현재 state 값과 action 데이터가 공급**된다. 이때 action의 타입이 create라면 reducer 안의 if문에 해당하는 코드가 실행된다. **실행 후 리턴되는 객체가 바로 state의 새로운 값이 된다.** 

즉, **reducer는 state를 입력 받고 action을 참조하여, 새로운 state 값을 만들어 리턴해주는 state를 가공하는 가공자**라고 볼 수 있다. 

이렇게 state 값이 변경되면 **dispatch가 subscribe에 등록되어 있는 구독자들을 다 호출**해주고 render가 호출된다. 

![image](https://user-images.githubusercontent.com/68090939/180645257-06657bb6-95dc-4fd4-8007-393e38f7d7b7.png) 

그 결과 **getState를 통해 state를 가져오고 render가 화면을 갱신해주면서, 새로운 state 값에 맞게 UI가 바뀌게 되는 것**이다. 

![image](https://user-images.githubusercontent.com/68090939/180645271-3eabe70f-3f57-4c80-a894-9248cab238d1.png) 

# 리덕스의 핵심

리덕스 동작에서 핵심은 **state**이다. 그 다음 핵심은 state를 기반으로 **화면에 그려준다**는 것이다. 

또 하나의 핵심은 store에 있는 **state에 직접 접근하는 게 금지**되어 있기 때문에, 

getState를 통해 값을 가져오고, 

dispatch를 통해 값을 변경시키고, 

subscribe를 이용해 값이 변경되었을 때 구동될 함수들을 등록해준다는 것이다. 

그리고 또 하나의 핵심은 **reducer를 통해서 state 값을 변경한다**는 것이다! 




