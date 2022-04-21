# React - state

- state를 사용하여 변수 값을 핸들링하고 효율적으로 rendering 할 수 있다.
  <br>

### Set State

- ##### Bad Example

```
<script type="text/babel">
  const root = document.querySelector('#root');

  let counter = 0;
    function countUp() {
      counter += 1;
      render(); // render 함수 호출
    }

    function render() {
      // rendering해도 전체가 아닌 변경된 부분만 rendering한다.
      ReactDOM.render(<Container />, root);
    }

    // return React Element
    const Container = function () {
      return (
      <div>
        // {변수명} 형식으로 변수에 할당된 값을 가지고 온다.
        <h1>counter: {counter}</h1>
        <button onClick={countUp}>count up</button>
      </div>
      );
    };

    render();
</script>
```

<br>

- ##### Good Example

```
<script type="text/babel">
    const root = document.querySelector('#root');
    const Container = function () {
      // state를 사용한 함수호출이 아닌 자동으로 렌더링
      // [data, modifier] = React.useState(initial value);
      const [counter, setCounter] = React.useState(0);  // 비구조화 할당
      const countUp = () => {
        // state 값이 변경되면 container가 rerendering된다.
        setCounter(counter + 1);
      };
      return (
        <div>
          <h1>counter: {counter}</h1>
          <button onClick={countUp}>count up</button>
        </div>
      );
    };
    ReactDOM.render(<Container />, root);
</script>
```

<br>

### State function

- 값을 다루는 방법은 두가지가 있다.

<br>
##### 1. 변수 값 직접 다루기

```
const [counter, setCounter] = React.useState(0);
const countUp = () => {
  // 변수 값을 직접 다루기 때문에 안전하지 않다.
  setCounter(counter + 1);
};
```

<br>

##### 2. 함수를 통해 state값 다루기

```
const [counter, setCounter] = React.useState(0);
const countUp = () => {
  // 현재 state 값을 기반으로 다음 state 값을 계산한다.
  setCounter(current => current + 1);
};
```

<br>

##### React - state 참고 사이트

https://ko.reactjs.org/docs/state-and-lifecycle.html

<br>
