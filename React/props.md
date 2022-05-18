# React - props

- 부모 컴포넌트와 자식 컴포넌트 간의 parameter를 전달 받는 방식
  <br>

### Props의 이해

- 부모컴포넌트(App)에서 자식컴포넌트(Button)을 호출할 때 propery값을 parameter로 넘겨준다.
- 자식컴포넌트에서는 props객체를 인자로 받아 컴포넌트 내에서 사용할 수 있다.

```
// 인자를 변수로 받을 수 있다. { text, big }
const Button = (props) => {
      return (
        <button
          style={{
            backgroundColor: 'pink',
            color: 'white',
            padding: 15,
            borderRadius: 15,
            border: 0,
            // 전달받은 props로 속성을 개별적으로 지정할 수 있다.
            fontSize: props.big ? 25 : 15
          }}
        >
          // 전달 받은 props객체의 text에 접근한다.
          {props.text}
        </button>
      );
    };

    const App = () => {
      return (
        <div>
          // text와 big property를 Button 컴포넌트에 전달한다. (여러개의 property 가능)
          <Button text='버튼이에옹' />
          <Button text='저는 그냥 버튼이 아니에옹' big={true} />
          <Button text='저는 그냥 버튼에옹' />
        </div>
      );
    };
```

<br>

### React memo

- 부모컴포넌트의 state 값이 변하는 경우, state값을 사용하지 않더라도 모든 자식컴포넌트는 rerendering된다.
- state값을 사용하지 않는 자식컴포넌트의 rerendering되는 것을 막고 싶다면 memo 메서드를 사용한다.

```
const Button = ({ text, onClick }) => {
      console.log({ text }, 'was rendered');
      return (
        <button
          onClick={onClick}
          style={{
            backgroundColor: 'pink',
            color: 'white',
            padding: 15,
            borderRadius: 15,
            border: 0,
          }}
        >
          {text}
        </button>
      );
    };

    // 버튼 객체를 기억한다.
    // state값을 사용하지 않는 자식컴포넌트는 rerendering하지 않는다.
    const MemoRizedButton = React.memo(Button);

    const App = () => {
      const [value, setValue] = React.useState('저장');
      const changeValue = () => {
        setValue('저장완료');
      };
      return (
        <div>
          <MemoRizedButton text={value} onClick={changeValue} />
          <MemoRizedButton text='다음' />
        </div>
      );
    };
```

<br>

### PropTypes이란?

- prop값의 타입을 지정하고자 할 때 사용하는 객체

```
// text 값에는 문자열 값만 padding값에는 숫자 값만 받고 싶다.
<div>
  <Button text='저장' padding={50} />
  <Button text={50} padding='hi' />
</div>
```

위와 같은 경우에 react에서 지원하는 propType을 사용한다.

<br>

#### PropType CDN 설치

```
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
```

<br>

### PropType을 사용한 prop값의 자료형 체크

#### 1. 자료형 확인

```
Button.propTypes = {
  // prop.text 값은 문자열만 받겠다.
  text: PropTypes.string,

  // prop.padding 값은 숫자만 받겠다.
  padding: PropTypes.number,
};
```

<br>

#### 2. 자료형 확인, undefined 확인

```
Button.propTypes = {
  // prop.text 값은 문자열만 받겠다.
  text: PropTypes.string,

  // prop.padding 값은 숫자만 받겠다.
  // 필수로 값을 받겠다.
  padding: PropTypes.number.isRequired,
};
```

<br>

#### 3. React 프로젝트에서 PropTypes 사용 예제

```
import PropTypes from 'prop-types';

Movie.propType = {
  coverImg: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired,
  summary: PropTypes.string.isRequired,
  genres: PropTypes.arrayOf(PropTypes.string).isRequired,
};
```

<br>

### PropType 더 알아보기

- PropType에서 지원하는 내용은 아래의 공식 사이트에서 확인할 수 있다.

```
https://ko.reactjs.org/docs/typechecking-with-proptypes.html
```
