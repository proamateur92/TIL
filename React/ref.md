# React - ref

- React에서 DOM요소를 다룰 때 사용한다.

  <br>

### useRef

1. import하기

```
import { useRef } from 'react';
```

<br>

2. 변수 생성 및 태그 명시

```
// useRef 함수를 할당 받는 변수 생성
const contentInput = useRef();

// ref property를 사용
<input ref={contentInput} value={content} type='text' />
```

<br>

3. DOM 접근

```
const onSubmit = () => {

  // content의 길이가 5 미만이면 해당 input태그에 focus
  if(content.length < 5) {
    contentInput.current.focus();
  }
}
```
