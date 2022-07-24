# 리덕스란 무엇인가? 

https://www.boostcourse.org/web231/lecture/1387443?isDesc=false

# state와 render의 관계

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

# action과 reducer 

