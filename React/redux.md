# React - redux

- 전역 상태 관리 라이브러리
- props Drilling 방지

<br>

##### React - route 참고 사이트

https://ko.redux.js.org/introduction/getting-started

<br>

### redux 패키지 설치

```
npm i redux react-redux
```

<br>

### 덕스 구조

- redux의 정석적인 구조 방식

```
https://github.com/erikras/ducks-modular-redux
```

<br>

1. redux 파일 생성

> src - redux - modules - test.js (redux를 작성할 파일)

<br>

2. 저장소 파일 생성

> src - redux - configStore.js

<br>

```
// configStore.js
import { createStore, combineReducers } from 'redux';
import test from './modules/test';

// reducer 묶어주기
// store는 총 1개, riducer의 개수는 제한이 없다.
const rootReducer = combineReducers({ test });
const store = createStore(rootReducer);

export default store;
```

3. store, provider와 컴포넌트 연결

```
// index.js
import { Provider } from 'react-redux';
import store from './redux/configStore';

<Provider store={store}>
</Provider>
```

4. redux에서 데이터 가져오기, 업데이트 하기

```
<useDispatch> // 데이터를 업데이트 하기
<useSelector> // 저장소로부터 값 가져오기
```
