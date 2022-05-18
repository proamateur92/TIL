# React - effect

- state값이 변경될 때 해당 component의 코드는 전부 rerendering된다.
- rerendering 하고 싶지 않은 코드가 있을 때 useEffect를 사용한다.
  <br>

### useEffect

- useEffect는 두개의 인자를 가진다.

1. callback function - 실행하려는 함수
2. dependency - 특정 state 변수를 지정하고 그 state값이 변경될 때만 실행되도록 한다.(여러개의 값을 넣어줄 수 있다.)

```
  // useState 사용
  useState(callback function, dependency[]);
```

<br>

#### useEffect 사용 전

```
const [count, setCount] = useState(0);
const [keyword, setKeyword] = useState('');

// 버튼을 클릭하면 count state 값 + 1
const onClick = () => setCount(prev => prev + 1);

// input값이 바뀔 때마다 keyword state 값 변경
const onChange = event => setKeyword(event.target.value);

// 버튼이 클릭되고 텍스트가 입력될 때마다 아래의 코드 모두 실행된다.
console.log('이 코드는 한번만 실행됩니다.');
console.log(`count: ${count}`);
console.log(`keyword: ${keyword}`);
```

<br>

#### useEffect 사용 후

```
const [count, setCount] = useState(0);
const [keyword, setKeyword] = useState('');

const onClick = () => setCount(prev => prev + 1);
const onChange = event => setKeyword(event.target.value);

// useEffect의 배열 인자는 어떠한 state도 주시하고 있지 않아 처음 component가 호출될 때만 실행된다.
useEffect(() => {
  console.log('이 코드는 한번만 실행됩니다.');
}, []);

// count state를 주시하여 해당 state값이 바뀔 때만 콜백함수가 실행된다.
useEffect(() => {
  console.log(`count: ${count}`);
}, [count]);

// keyword state를 주시하여 해당 state값이 바뀔 때만 콜백함수가 실행된다.
useEffect(() => {

  // component가 처음 호출되는 시점에 keyword값이 존재하지 않으므로 keyword 길이가 3이상이 아니면 callback function이 실행되지 않도록 한다.
  if (keyword !== '' && keyword.length > 2) console.log(`keyword: ${keyword}`);
}, [keyword]);
```

<br>

### Clean Function

- component가 destroy될 때 실행되는 callback function

#### 방법 1

```
// component가 destory될 때 실행
function die() {
    console.log('컴포넌트 쥬금 ㅠㅠ)
}

// component가 생성될 때 실행
function create() {
  conosole.log('컴포넌트 생성!');
  return die();
}

useEffect(() => {
  // callback function에 create함수를 넣어준다.
  create();
}, []);
```

<br>

#### 방법 2 (방법 1을 줄인 코드)

```
useEffect(() => {
  console.log('컴포넌트 생성!);
  return () => {'컴포넌트 쥬금 ㅠㅠ};
}, []);
```
