# React - 성능최적화2

> Udemy - React 완벽 가이드 with Redux, Next.js, TypeScript를 참고하여 작성하였습니다.

<br>

## 컴포넌트 리렌더링 조건

- 컴포넌트의 props, state, context가 변경될 때마다 재평가 된다.
- 위의 조건이 충족되면 리액트는 컴포넌트를 실행하게 된다.

<br>

```
App.js

const [showPragraph, setShowParagraph] = useState(false);
  const toggleParagraphHandler = () => {
    setShowParagraph(prev => !prev);
  };

  console.log('App running');

<div className='app'>
  <h1>Hi there!</h1>
  {showPragraph && <p>This is new!</p>}
  <Button type='button' className='toggle-button' onClick={toggleParagraphHandler}>
    Toggle Button
  </Button>
</div>


Button.js

console.log('Button Running');

return (
  <button
    type={props.type || 'button'}
    className={`${classes.button} ${props.className}`}
    onClick={props.onClick}
    disabled={props.disabled}
  >
    {props.children}
  </button>
);
```

프로젝트를 실행하면 버튼을 클릭할 때마다 'App running', 'Button Running'이 콘솔에 찍히게 된다.

<br>

```
// App.js
console.log('App running');
return (
  <div className='app'>
    <h1>Hi there!</h1>
    <DemoOutput show={showPragraph} />
    <Button type='button' className='toggle-button' onClick={toggleParagraphHandler}>
      Toggle Button
    </Button>
  </div>
);


// DemoOutput.js
console.log('DemoOutput running');
return <>{props.show ? <p>Toggle output</p>}</>;


// Button.js
console.log('Button Running');

return (
  <button type={props.type || 'button'} className={`${classes.button} ${props.className}`} onClick={props.onClick} disabled={props.disabled}>
    {props.children}
  </button>
);
```

위의 코드에서 Demoutput에 state가 아닌 고정된 값(false)을 props로 내려주어도 버튼을 클릭하면 'App running', 'DemoOutput Running', 'Button Running'이 콘솔에 찍히게 된다. 상위 컴포넌트가 렌더링되면 하위 컴포넌트도 리렌더링되기 때문이다.

<br>

## React.memo

<br>

### 예제1

```
// App.js
 <DemoOutput show={false} />

// DemoOutput.js
export default React.memo(DemoOutput);
```

'App running', 'Button Running', 최초 렌더링 후 'DemoOutput Running'는 더 이상 찍히지 않는다.

- 함수형 컴포넌트를 React.memo로 묶어 최적화 할 수 있다.
  인자로 들어간 컴포넌트에 어떤 props가 입력되는지 확인하고 입력되는 모든 props와 이전 props를 비교해서 다른 경우에만 재평가, 재실행한다.

<br>

- 최적화에는 비용이 필요하다. 기존의 props를 저장하고 비교해야 하는 데 필요한 성능 비용을 따져봐야 하기 때문에 모든 컴포넌트에 적용되지는 않는다.
  성능 비용에는 props의 갯수, 컴포넌트의 복잡도 그리고 자식 컴포넌트의 숫자에 따라 상이하다.

<br>

- 부모 컴포넌트가 매번 변경되거나 컴포넌트의 변화가 있거나 props가 바뀌는 경우에는 적합하지 않다.
  매우 작은 앱이나 컴포넌트를 가진 경우에도 적합하지 않다.

<br>

### 예제2

```
// Button.js
export default React.memo(Button);
```

Button.js에 React.memo를 적용했음에도 콘솔에는 'App running', 'Button Running'가 계속해서 찍힌다.

자바스크립트에서 App함수가 실행될 때마다 App에 선언된 값들은 전부 새로 생성되어진다. 원시 값을 비교하면 서로 값이 동일하지만 함수는 참조 값이기 때문에 새로운 함수 props.toggleParagraphHandler와 이전 함수 props.prev.toggleParagraphHandler는 서로 다른 값이 되기 때문에 React.memo로 최적화할 수 없다.

<br>

## useCallback()으로 함수 재생성 방지하기

- 우리는 useCallback로 함수를 저장하고 매번 실행할 때마다 재생성 할 필요없다고 알려준다.
- 같은 메모리 주소를 참조하여 비교하게 된다.
- useCallback함수로 저장하려는 함수를 감싸기만하면 된다.
- useEffect처럼 dependecy 인자가 필요하다.
  <br>

```
// App.js
const toggleParagraphHandler = useCallback(() => {
  setShowParagraph(prev => !prev);
}, []);
```

<br>

이제 리렌더링 할 때 console에는 'App running'만이 찍히게 된다.
어떤 함수가 절대 변경이 되지 않아야 한다면 useCallback을 사용한다.

<br>

## useMemo로 같은 값 rerendering 방지하기

```
// App.js

const [listTitle, setListTitle] = useState('NO TITLE');

  const showList = useCallback(() => {
    setListTitle('ITEM LIST');
  }, []);

  console.log('App running');

  return (
    <div className='app'>
      <DemoList title={listTitle} items={[5, 3, 2, 1]} />
      <Button type='button' onClick={showList}>
        Show List
      </Button>
    </div>
  );

// DemoList.js

const DemoList = ({ title, items }) => {
  console.log('DemoList running');
  const newItems = items.sort((a, b) => a - b);
  return (
    <>
      <h1>{title}</h1>
      <ul>
        {newItems.map(items => (
          <li key={items}>{items}</li>
        ))}
      </ul>
    </>
  );
};

export default React.memo(DemoList);
```

'App running', 'DemoList running' 문구가 콘솔에 찍힌다.

props로 내려 받는 배열의 값의 변동이 없다면 불필요한 재정렬을 막고 싶다.

useCallback와는 비슷하지만 값을 비교하는 useMemo를 사용한다.

<br>

```
// DemoList.js
const newItems = useMemo(() => {
    console.log('sorted');
    return items.sort((a, b) => a - b);
  }, [items]);

그러나 여전히 정렬이 두번 일어난다. 그 이유는 상위 컴포넌트인 App에서 내려주는 items를 살펴보면 알 수 있다.

<DemoList title={listTitle} items={[5, 3, 2, 1]} />

앞서 알아본 것과 같이 DemoList의 props 중 items는 계속 같은 값을 가진 배열로 내려주는 것처럼 보이지만
리렌더링되면 items가 새로 생성되면서 다른 주소값을 가진 items가 만들어진다.

따라서 items도 useMemo로 감싸준다.

// App.js
const itemList = useMemo(() => [5, 3, 2, 1], []);
<DemoList title={listTitle} items={itemList} />
```

콘솔에 sorted가 한번만 찍히는 것을 볼 수 있다.
