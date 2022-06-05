# Fragments, Portals & Refs

<br>

### Fragments

JSX 제한 사항 및 해결 방법

1. JSX는 컴포넌트가 반환하는 코드로 DOM을 통해 렌더링 된다,

2. root JSX 요소는 반드시 1개여야 한다. -> React element로 반환된다.

3. 2번 항목의 이유로 <strong>'div Suop'</strong>가 발생한다. - 실제 DOM으로 렌더링 될 때 불필요한 HTML요소가 모두 렌더링 되는 현상

<br>

```
<div>
  <div>
    <div>
      <div>
        <h2>불필요한 div가 모두 렌더링 된다!</h2>
      </div>
    </div>
  </div>
</div>
```

<br>

##### Wrapper.js

```
const Wrapper = props => {
// children => 열린 태그와 닫힘 태그 사이의 코드를 받아온다.
return props.children;
}

export defualt
```

<br>

React.Fragment 태그로 감싸주어 최종적으로 불필요한 HTML 요소는 DOM에 추가되지 않도록 한다.

<br>

```
<React.Fragment>
</React.Fragment>

<Fragment>
</Fragment>
```

<br>

## Portals 필요성

- modal은 전체 페이지 상위에 있다.(오버레이 되어있다.)
- 따라서 HTML코드에 중첩되어 있는 것은 좋은 구조가 아니다.

<br>

##### App.js

```
const App = () => {
  return (
    <>
      // Modal 컴포넌트를 호출하는 위치를 위로 올려주어야겠다.
      <Modal />
      <UserForm />
    </>
  )
}
```

<br>

## Portals 사용법

- React Portal을 사용하여 root와 인접하도록 만들어준다.

<br>

##### index.html

- 포탈 될 위치를 명시해준다.

```
<div id='backdrop-root'>
<div id='overlay-root'>
<div id='root'>
```

<br>

##### Modal.js

```
// portal을 사용하기 위해 react-dom import
import ReactDOM from 'react-dom';

// modal창 발생 시 주변 어둡게 만들기
const BackDrop = () => {
  return <MakeDark></MakeDark>;
};

// modal 창 발생
const ModalOverylay = props => {
  return (
    <Container onClick={props.onClose}>
      <header>
        <span>{props.title}</span>
      </header>
      <div>
        <h1>{props.msg}</h1>
      </div>
      <footer>
        <button onClick={props.onClose}>닫기</button>
      </footer>
    </Container>
  );
};

const Modal = props => {
  return (
    <React.Fragment>
      // 첫번째 인자 portal로 내보낼 JSX코드
      //  두번째 인자 portal 시킬 위치
      {ReactDOM.createPortal(<BackDrop />, document.getElementById('backdrop-root'))}
      {ReactDOM.createPortal(<ModalOverylay title={props.title} msg={props.msg} onClose={props.onClose} />, document.getElementById('overlay-root'))}
    </React.Fragment>
  );
};
```
