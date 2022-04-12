# React

Node 기반의 Javascript 라이브러리

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

- React element생성, event listner을 추가하는 기능

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

##### id가 'root'인 컨테이너에 React Element를 추가하고 render하는 경우

<br>

```
const root = document.getElementById('root');

    const h1 = React.createElement(
      // elementName
      {
        /*
          property Object: eventLister, className, style 등의 property를 가질 수 있다.
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

    // React element를 render하라
    ReactDOM.render(container, root);
```
