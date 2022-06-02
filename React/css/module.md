# css module

- module css를 import하여 사용할 때에는 특정 태그에 className을 명시해주어야 한다.

<br>

##### Button.module.css

> <br>
> media query를 사용할 때에도 클래스 선택자를 사용해야 한다.
> <br>
> <br>
> import 받는 js파일에서 module의 객체 중 명시된 클래스 값을 가져오기 때문이다.<br>
> <br>

```
.button {
  width: 100%;
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
}

.button:focus {
  outline: none;
}

.button:hover,
.button:active {
  background: #ac0e77;
  border-color: #ac0e77;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}

@media (min-width: 768px) {
  .button {
    width: auto;
  }
}
```

<br>

##### Button.js

> <br>
> module.css를 import 할 때는 styles 또는 classes라는 명칭을 사용한다. <br>
> <br>

```
import styles from './Button.module.css';

<button type={props.type} className={styles.button} onClick={props.onClick}>
  // wrapper component는 children property를 사용한다.
  {props.children}
</button>
```

<br>

###### Input.module.css

```
.form-control {
  margin: 0.5rem 0;
}

.form-control label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

.form-control input {
  display: block;
  width: 100%;
  border: 1px solid #ccc;
  font: inherit;
  line-height: 1.5rem;
  padding: 0 0.25rem;
}

.form-control input:focus {
  outline: none;
  background: #fad0ec;
  border-color: #8b005d;
}

.form-control.invalid input {
  background-color: rgb(255, 157, 157);
  border-color: red;
}

.form-control.invalid label {
  color: red;
}
```

<br>

###### Input.js

> <br>
> module css를 동적으로 사용할 때에는 백틱을 사용하여 className을 유동적으로 적용해준다. <br>
> <br>

```
import styles from './Input.module.css';

<div className={`${styles['form-control']} ${!isValid ? styles['invalid'] : ''}`}>
  <label>Course Goal</label>
  <input type='text' onChange={goalInputChangeHandler} />
</div>
```

<br>

##### 참고 사이트

https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/
