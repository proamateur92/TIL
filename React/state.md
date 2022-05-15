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
      // render 함수 호출
      render();
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

### useState 실습

- 단위를 변환하는 컴포넌트를 2개 이상 생성한다.
- 최상위 컴포넌트인 App에서 select, option 태그를 사용해 사용자가 선택하는 컴포넌트를 호출하도록 한다.

```
<script type="text/babel">
    const root = document.querySelector('#root');

    // 분 -> 시간 / 시간 -> 분으로 변환하는 컴포넌트
    const MinutesToHours = () => {
      // 입력 값에 대한 state
      const [amount, setAmount] = React.useState(0);

      // 시간과 분 두 단위를 바꿔주기 위한 state
      const [inverted, setInverted] = React.useState(false);

      const handleMinutes = event => {
        setAmount(event.target.value);
      };

      // reset 버튼을 클릭하면 입력 값을 0으로 초기화시켜준다.
      const reset = () => {
        setAmount(0);
      };

      // 단위 변환을 전환시켜준다.
      const onInvert = () => {
        reset();
        setInverted(!inverted);
      };
      return (
        <div>
          <div>
            <label htmlFor='minutes'>분: </label>
            <input type='number' value={inverted ? amount * 60 : amount} onChange={handleMinutes} id='minutes' placeholder='Minutes' disabled={inverted} />
          </div>
          <div>
            <label htmlFor='hours'>시간: </label>
            <input
              type='number'
              value={inverted ? amount : Math.round(amount / 60)}
              onChange={handleMinutes}
              id='hours'
              placeholder='Hours'
              disabled={!inverted}
            />
          </div>
          <button onClick={reset}>리셋</button>
          <button onClick={onInvert}>{!inverted ? '분 -> 시간' : '시간 -> 분'}</button>
        </div>
      );
    };

    // 화씨를 섭씨로, 섭씨를 화씨로 변환하는 컴포넌트
    const CelsiusToFahrenheit = () => {
      const [amount, setAmount] = React.useState('0');
      const [reverted, setReverted] = React.useState(false);
      const onChange = event => {
        setAmount(event.target.value);
      };
      const onRevert = () => {
        setReverted(!reverted);
        reset();
      };
      const reset = () => {
        setAmount('0');
      };
      return (
        <div>
          <div>
            <label htmlFor='fahrenheit'>화씨: </label>
            <input value={!reverted ? amount : (amount * 9) / 5 + 32} onChange={onChange} id='fahrenheit' type='number' disabled={reverted} />
          </div>
          <div>
            <label htmlFor='celsius'>섭씨: </label>
            <input value={!reverted ? ((amount - 32) * 5) / 9 : amount} onChange={onChange} id='celsius' type='number' disabled={!reverted} />
          </div>
          <button onClick={reset}>초기화</button>
          <button onClick={onRevert}>{!onRevert ? '화씨 -> 섭씨' : '섭씨 -> 화씨'}</button>
        </div>
      );
    };

    // 최상위 컴포넌트
    const App = () => {
      const [index, setIndex] = React.useState('xx');

      // select로부터 변경된 value값을 state로 다룬다.
      const onSelect = event => {
        setIndex(event.target.value);
      };
      return (
        <div>
          <h1>단위 변환기</h1>
          <select onChange={onSelect} value={index}>
            <option value='xx'>변환 종류를 고르세요</option>
            <option value='0'>시간 변환</option>
            <option value='1'>온도 변환</option>
          </select>
          <hr />

          // state로 선언된 index로 컴포넌트를 호출한다.
          {index === 'xx' ? <span>단위 변환을 선택해주세요</span> : null}
          {index === '0' ? <MinutesToHours /> : null}
          {index === '1' ? <CelsiusToFahrenheit /> : null}
        </div>
      );
    };

    ReactDOM.render(<App />, root);
  </script>
```

##### React - state 참고 사이트

https://ko.reactjs.org/docs/state-and-lifecycle.html

<br>
