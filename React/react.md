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

#### id가 'root'인 컨테이너에 React Element를 추가하고 render하는 경우

<br>

```
const root = document.getElementById('root');

    const h1 = React.createElement(
      // elementName
      {
        /*
          property Object: eventListner, className, style 등의 property를 가질 수 있다.
        */
      },
      // content
    );

    const btn = React.createElement(
      'button',
      {
        class: 'btn',
        onClick: () => console.log('you clicked?!'),
      },
      '나는 버튼이야'
    );

    // 2개 이상의 React element를 render하는 경우 배열에 넣어준다.
    const container = React.createElement('div', null, [h1, btn]);

    // React element container를 root에 렌더링하라
    ReactDOM.render(container, root);
```

<br>

### JSX

JavaScript 확장 문법으로 React element 생성 시 보다 간단히 작성할 수 있다.

<br>

##### JSX 공식 문서

https://ko.reactjs.org/docs/introducing-jsx.html

<br>

```
const root = document.querySelector('#root');
    // React Element를 함수의 return 값으로 내보낸다.
    const H1 = function () {
      return (
        <h1 class='greeting' onMouseEnter={() => console.log('Mouse Entered')}>
          Hello, world!
        </h1>
      );
    };

    const Button = () => {
      return (
        <button class='button' onClick={() => console.log('I am a click')}>
          Button Text
        </button>
      );
    };

    const Container = () => {
      return (
        <div>
          <H1 />      // 변수명의 첫글자는 반드시 대문자로 작성해준다.
          <Button />  // 소문자로 작성할 경우 html태그로 인식한다.
        </div>
      );
    };

    ReactDOM.render(<Container />, root);
```

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
