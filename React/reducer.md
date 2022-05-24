# useReducer

- 컴포넌트로부터 상태변화 로직을 분리할 수 있다.

- 다수의 하윗값을 포함하는 복잡한 정적 로직을 만드는 경우

- 다음 state가 이전 state에 의존적인 경우

- 위 두 경우에 해당한다면 useState보다 useReducer가 선호된다.

<br>

### 기본 구조

Counter.js

- state -> 최신의 state값
- action -> dispatch에서 발생된 action 객체의 값

```
const reducer = (state, action) => {
	switch (action.type) {
		case 1:
			return state + 1;
		case 10:
			return state + 10;
		default:
			return state;
	}
}
```

<br>

- count -> state
- dispatch -> 상태변화를 발생시키는 함수
- reducer -> reducer 상태변화를 처리해준다. (호출)
- 1 -> count state의 초기값

```
const Counter(() => {

	const [count, dispatch] = useReducer(reducer, 1);

	return (
		<div>
			{count} // 최초 1
			// type -> action 객체(상태변화)
			<button onClick={() => dispatch({ type: 1 }) }>add 1</button>
			<button onClick={() => dispatch({ type: 10 }) }>add 10</button>
		</div>
	)
})
```
