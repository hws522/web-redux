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
