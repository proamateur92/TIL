# React

Node 기반의 Javascript 라이브러리

<br>

##### React 공식 사이트

https://ko.reactjs.org/

<br>

### React를 사용하는 3가지 이유

<br>

1. Component 단위

- 여러 파일의 중복되는 부분을 Component단위로 나누어 조립할 수 있다.

<br>

2. 선언형 프로그래밍

<br>

3. Virtual DOM

- DOM요소의 조작이 있을 때마다 웹 브라우저의 렌더링이 이루어지는 경우 Virtual DOM을 통해 수시로 렌더링 되는 것이 아니라 연산 전, 후를 비교하여 변동된 사항을 반영한다.

<br>

### React 사용을 위한 라이브러리

<br>

1. React 라이브러리

- React element생성, Event listner을 추가하는 기능

```
<script crossorigin src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
```

<br>

2. React DOM

- React element를 HTML로 변경

```
 <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
```

<br>

<details>
<summary>id가 'root'인 컨테이너에 React Element(span)를 추가하고 render해볼래?</summary>
<div markdown="1">

```
const root = document.getElementById('root');
const span = React.createElement('span', {}, '안냥');
ReactDOM.render(span, root);
```

</div>
</details>

<br>

<details>
<summary>id가 'root'인 컨테이너에 React Element(span, button)를 추가하고 render해볼래?</summary>
<div markdown="1">

```
const root = document.getElementById('root');
const span = React.createElement('span', {}, '안냥');

// 두번째 인자로 id, class 등 props를 작성해준다.
const button = React.createElement('button', { onClick: () => alert('누르지 마잉~') }, '난 버튼이야!');
    ReactDOM.render([span, button], document.body);

ReactDOM.render([span, button], root);
```

</div>
</details>

<br>

<br>

### Babel

ES6를 ES5로 바꿔주는 도구이다. 여기서는 JSX 코드를 브라우저가 이해하는 형태로 변환하기 위해 사용한다.

<br>

##### Babel 공식 문서 참고

https://babeljs.io/docs/en/babel-standalone

<br>

##### Babel Complier 참고

https://babeljs.io/repl

<br>

- Babel을 사용하기 위한 Script

```
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

<br>

- Babel 사용을 위해 type을 작성한다.

```
<script type='text/babel'></script>
```

<br>

- Babel을 사용한 코드와 그렇지 않은 코드를 살펴보자.

```
<!-- JSX 코드 -->
const Title = (
      <h1 id='title' onMouseEnter={() => alert('건드리지마!')}>
        반가워잉
      </h1>
    );
```

```
<!-- Babel은 위의 JSX 코드를 아래처럼 변환시켜준다. -->
const Title = /*#__PURE__*/React.createElement("h1", {
  id: "title",
  onMouseEnter: () => alert('건드리지마!')
}, "\uBC18\uAC00\uC6CC\uC789");
```

### JSX

JavaScript 확장 문법으로 React element 생성 시 보다 간단히 작성할 수 있다.

<br>

##### JSX 공식 문서

https://ko.reactjs.org/docs/introducing-jsx.html

<br>

#### JSX 써보기

<br>

```
<!-- 기존 react element 생성 방식 -->
const span = React.createElement('span', {}, '안냥');

<!-- JSX 코드로 작성했을 때 -->
<!-- const span = <span>안냥</span> -->
```

<br>

#### JSX 써보기2

```
<!-- 함수를 할당 받는 변수로 선언해준다. -->
const Title = () => {
  return (
    <h1 id='title' onMouseEnter={() => alert('건드리지마!')}>
      반가워잉
    </h1>
  );
};

const Button = () => {
  return (
    <button
      onClick={() => {
        alert('누르지 마잉~');
      }}
    >
      난 버튼이야
    </button>
  );
};

const Container = () => {
  return (
    <div>
      <!-- html 요소처럼 선언해준다. -->
      <!-- 첫글자가 대문자인 것을 주의하자. -->
      <Title />
      <Button />
    </div>
  );
};

ReactDOM.render(<Container />, root);
```
