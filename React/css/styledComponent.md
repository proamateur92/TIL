# styled-component

### 패키지 설치

```
npm i styled-components
```

<br>

### 사용 예제

```
// Button.js

import styled from 'styled-components';

const Button = styled.button`
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;

  @media (min-width: 768px) {
    width: auto;
  }

  &:focus {
    outline: none;
  }

  &:hover,
  &:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
  }
`;

export default Button;
```

```
// Input.js
import styled from 'styled-components';
import Button from '../../UI/Button/Button';

const FormContrtol = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${props => (props.inValid ? 'red' : 'black')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
    border-color: ${props => (props.inValid ? 'red' : 'inherit')};
    background-color: ${props => (props.inValid ? 'rgb(255, 157, 157)' : '')};
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }
`;

<form onSubmit={formSubmitHandler}>
  <div className={`${styles['form-control']} ${!isValid ? styles['invalid'] : ''}`}>
    <label>Course Goal</label>
    <input type='text' onChange={goalInputChangeHandler} />
  </div>
  <Button type='submit'>Add Goal</Button>
</form>
```
