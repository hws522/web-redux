# Start Redux with Egoing

<br>
<br>

### **redux 의 핵심은 store 이다.**

---

<br>

store 라고 하는 것은 정보가 저장되는 곳이다.

store 안에는 state 가 있고 여기에 실제 정보가 저장된다. 허나 절대로 state 에 직접 접속이 금지, 불가하다. 무언가를 통해서 접속해야만 한다.

store 를 만들면서 가장먼저 반드시 해야할 것은 reducer 라고 하는 함수를 만들어 공급해줘야 한다.

redux 에서 이해하는 것이 가장 힘든 것이 reducer 다.

지금까지의 과정을 간단히 설명하면 이러한 모양이 된다.

```js
function reducer(oldState, action) {
  //....
}
var store = Redux.createStore(reducer);
```

redux 에 createStore 를 하게 되면 store 가 생성이 되고, 그 store 를 생성할 때 꼭 줘야하는 인자가 reducer 다. 위의 형식같은 reducer 를 만드는 것이 redux 를 만드는 일이라 해도 과언이 아니라 할 수 있다.

render 는 redux 와는 상관없이, UI 를 만들어주는 역할을 하는 우리가 짤 코드다.

우리는 store 에 있는 state 에 직접 접근하는 것이 금지되어 있기 때문에, store 와 render 앞단에 우리가 원하는 일을 행해줄 dispatch, subscribe, getState 함수가 있다.

render 는 이러한 형식이다.

```js
function render() {
  var state = store.getState();
  //....
  document.querySelector("#app").innerHTML = `
    <h1>WEB</h1>
    ....
    `;
}
```

store 에서 getState 를 통하여 state 값을 가져오는 것이며, innerHTML 을 통하여 state 의 값을 이용해서 웹페이지를 만든다음 실행하면 UI 가 되는 형식이다.

render 는 언제나 현재 state를 반영한 UI 를 만든다.

store의 state 값이 바뀔 때 마다 render 함수를 호출 할 수 있다면, 즉 render 함수만 잘 만들면 state 값이 바뀔 때 마다 UI가 갱신되게 할 수 있다.

그때 사용되는 것이 subscribe 이다.

우리가 render 함수를 subscribe 에 등록하는데에 필요한 코드는 이런식이다.

```js
store.subscribe(render);
```

action 이라고 하는 객체가 dispatch 에게 전달이 된다.

dispatch 는 reducer 를 호출해서 state 의 값을 바꾼다.

그리고 그 작업이 끝난다음 subscribe 를 이용해서 render 함수를 호출하여 화면을 갱신한다.

dispatch 가 reducer 를 호출할 때, 두개의 값을 전달한다. 첫번째는 현재의 state 값, 두번째는 action data. 이후 return 을 해주는 객체는 state 의 새로운 값이 된다.

즉, reducer 는 state를 입력값으로 받고 action 을 참조해서 새로운 state 값을 만들어 리턴해주는 state 를 가공해주는 가공자 역할이다.

state 값이 변경되었으니 dispatch 가 subscribe 을 통하여 render 가 호출되고 이전의 과정을 반복한다. 그리하여 화면을 갱신해주는 것이다.

요약

- redux 는 state 를 기반으로 화면에 그려주는 것이다.

- state 를 직접 접근할 수 없으니 중간에서 getState 를 통해 state 값을 가져오고, dispatch 를 통해 값을 변경하고, subscribe 를 이용해서 값이 변경됐을 때 구동될 함수들을 등록해준다.

- reducer 를 통해서 state 값을 변경한다.
