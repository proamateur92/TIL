# React - 성능최적화

### Memoization

- 똑같은 연산은 기억하여 반환한다.
  -> 연산과정 최적화

- 컴포넌트의 state 변화 등의 이유로 rerendering 될 때, state값이나 어떤 변수의 값이 rerender 이전 값과 동일하다면 수행하지 않는다.

<br>

### 성능 최적화 1 - useMemo()

- data(배열) state 값이 변경되면 하기의 함수가 호출된다.
- 아래의 함수(getDiaryAnalysis)는 data의 길이만을 변수로 할당 받는다.
- 따라서, 일기의 update는 data의 길이에 지장을 주지 않으므로 계속해서 render 된다면 비효율적이다.

```
// App.js
const getDiaryAnalysis = () => {
  console.log('일기 분석 시작');

  const goodCount = data.filter(v => v.point >= 3).length;
  const badCount = data.length - goodCount;
  const goodRatio = (goodCount / data.length) * 100;
  return { goodCount, badCount, goodRatio };
};

const { goodCount, badCount, goodRatio } = getDiaryAnalysis();
```

<br>

#### useMemo함수를 사용한 코드

```
// data.length가 변하지 않으면 호출되지 않는다.
// useMemo는 return 값을 가진다.
const getDiaryAnalysis = useMemo(() => {

// useMemo를 사용하기 이전에는  글 수정 등을 통해 state값이 변경되면 getDiaryAnalysis함수가 호출 되는 구조였다.
// useMemo를 통해 이전 값과 비교하여 data.length값이 변하지 않은 경우라면 rerender 대상에서 제외한다.
  console.log('일기 분석 시작');

  const goodCount = data.filter(v => v.point >= 3).length;
  const badCount = data.length - goodCount;
  const goodRatio = (goodCount / data.length) * 100;
  return { goodCount, badCount, goodRatio };
}, [data.length]);

// getDiaryAnalysis 함수가 아니다.
const { goodCount, badCount, goodRatio } = getDiaryAnalysis;
```

<br>

### 성능 최적화 2 - React.memo

<br>

#### 원시 값을 가지는 데이터 state

```
// prop 'text'가 변하지 않으면 rerender 되지 않는다.
const Textview = React.memo(({ text }) => {
  return <div>{text}</div>;
});

// prop 'count'가 변하지 않으면 rerender 되지 않는다.
const Countview = React.memo(({ count }) => {
  return <div>{count}</div>;
});

const OptimizeTest = () => {
  const [count, setCount] = useState(1);
  const [text, setText] = useState('');

  return (
    <div style={{ padding: 50 }}>
      <div>
        <h2>Count</h2>
        <Countview count={count} />
        <button onClick={() => setCount(prev => prev + 1)}>+</button>
      </div>
      <div>
        <h2>Text</h2>
        <Textview text={text} />
        <input value={text} type='text' onChange={e => setText(e.target.value)} />
      </div>
    </div>
  );
};

export default OptimizeTest;
```

<br>

#### 객체 값을 가지는 데이터 state

- 원시 데이터의 경우에는 값이 동일할 경우 state이 동작하지 않는다.
- 객체는 얕은 비교(비원시 타입을 비교할 때 객체의 주소에 의한 비교)를 하게 된다.

```
const CounterA = React.memo(({ count }) => {
  useEffect(() => {
    console.log(`CounterA is updated:: ${count}`);
  });
  return <div>{count}</div>;
});

const CounterB = ({ obj }) => {
  useEffect(() => {
    console.log(`CounterB is updated:: ${obj.count}`);
  });
  return <div>{obj.count}</div>;
};

// 깊은 비교를 통한 비교
// true는 이전 값과 동일 false는 이전 값과 상이함을 나타낸다.
const areEqual = (prevProps, nextProps) => {
  return prevProps.obj.count === nextProps.obj.count;
};

// 고차 컴포넌트를 사용한다.
const MemoizedCounterB = React.memo(CounterB, areEqual);

const OptimizeTest = () => {
  const [count, setCount] = useState(1);
  const [obj, setObj] = useState({
    count: 1,
  });

  return (
    <div style={{ padding: 50 }}>
      <div>
        <h2>Counter A</h2>
        <button onClick={() => setCount(prev => prev)}>A button</button>
        <CounterA count={count} />
      </div>
      <div>
        <h2>Counter B</h2>
        <button
          onClick={() => {
            setObj(prev => ({ count: prev.count }));
          }}
        >
          B button
        </button>
        <MemoizedCounterB obj={obj} />
      </div>
    </div>
  );
};
```
