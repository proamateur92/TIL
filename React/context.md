# React - context

- props chaining이 과도해질 때 React context를 사용하여 전역적으로 state를 관리할 수 있다.
  <br>

## Context 사용하기

- store 폴더 생성
- auth-context.js 파일 생성

<br>

##### auth-context.js

```
import React from 'react';

const AuthContext = React.createContext({
  isLoggedIn: false,
  onLogout: () => {},
});

export default AuthContext;
```

<br>

### context 사용 예제 1

<br>

##### App.js

```

import MainHeader from './components/MainHeader/MainHeader';
const [isLoggedIn, setIsLoggedIn] = useState(false);

// state를 선언하여 isLoggedIn 값에 따라 변경되도록한다.
<AuthContext.Provider value={isLoggedIn: isLoggedIn}>
  <MainHeader onLogout={logoutHandler} />
  <main>
	{!isLoggedIn && <Login onLogin={loginHandler} />}
	{isLoggedIn && <Home onLogout={logoutHandler} />}
  </main>
</AuthContext.Provider>

```

<br>

##### Navigation.js

```
import AuthContext from '../../store/auth-context';

// <AuthContext.Consumer>로 JSX코드를 감싸주고 함수를 선언하여 return한다.
// 함수를 통해 context선언 파일의 객체에 접근한다.
const Navigation = props => {
  return (
    <AuthContext.Consumer>
      {ctx => {
        return (
          <nav className={classes.nav}>
            <ul>
              {ctx.isLoggedIn && (
                <li>
                  <a href='/'>Users</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <a href='/'>Admin</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <button onClick={props.onLogout}>Logout</button>
                </li>
              )}
            </ul>
          </nav>
        );
      }}
    </AuthContext.Consumer>
  );
};
```

위와 같은 경우에 react에서 지원하는 propType을 사용한다.

<br>

### context 사용 예제 2

<br>

##### Navigation.js

- 위의 코드에서 consumer를 삭제해준다.

```
import React, { useContext } from 'react';

const ctx = useContext(AuthContext);
```

<br>

## Context 동적으로 사용하기

- App.js에 선언되어 있던 함수를 context에 넣어주어 공급할 수 있다.

- logoutHandler는 MainHeader -> Navigation 으로 전달되어지고 있다.

<br>

##### App.js

```
const logoutHandler = () => {
    localStorage.removeItem('logInCheck');
    setIsLoggedIn(false);
  };

<AuthContext.Provider
  value={
    isLoggedIn: isLoggedIn,
    onLogin: loginHandler,
    onLogout: logoutHandler,
  }
>
  <MainHeader />
  <main>
	{!isLoggedIn && <Login />}
	{isLoggedIn && <Home />}
  </main>
</AuthContext.Provider>
```

<br>

##### Navigation.js

- useContext 훅을 사용했던 변수 그대로 명시해준다.

```
// ex) ctx.onLogin / ctx.onLogout

<button onClick={ctx.onLogout}>Logout</button>
```

<br>

#### tip 1

- 공급해줄 변수에 객체 값을 선언해주면 소비해줄 컴포넌트에서 자동완성을 사용할 수 있다.

<br>

##### auth-context.js

```
const AuthContext = React.createContext({
  isLoggedIn: false,
  onLogout: () => {},
});
```

<br>

#### tip2 - auth 기능과 App.js 분리하기

- App에서 관리하던 data, function 등의 핸들링을 auth-context로 옮겨준다.

<br>

##### auth-context.js

```
export const AuthContextProvider = props => {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  useEffect(() => {
    if (localStorage.getItem('logInCheck') === '1') {
      setIsLoggedIn(true);
    }
  }, []);

  const loginHandler = (email, password) => {
    localStorage.setItem('logInCheck', '1');
    setIsLoggedIn(true);
  };

  const logoutHandler = () => {
    localStorage.removeItem('logInCheck');
    setIsLoggedIn(false);
  };

  return <AuthContext.Provider value={{ isLoggedIn: isLoggedIn, onLogin: loginHandler, onLogout: logoutHandler }}>{props.children}</AuthContext.Provider>;
};
```

<br>

##### index.js

- App을 provider로 감싸준다.

```
import { AuthContextProvider } from './store/auth-context';

ReactDOM.render(
  <AuthContextProvider>
    <App />
  </AuthContextProvider>,
  document.getElementById('root')
);
```

<br>

##### App.js

```
import AuthContext from './store/auth-context';

function App() {
  const authCtx = useContext(AuthContext);
  console.log(authCtx);
  return (
    <React.Fragment>
      <MainHeader />
      <main>
        {!authCtx.isLoggedIn && <Login />}
        {authCtx.isLoggedIn && <Home />}
      </main>
    </React.Fragment>
  );
}
```

<br>

## React Context Limitations

- state 변경이 상당히 잦은 경우에 Reaxt Context는 적합하지 않다.
- context와 props의 사용이 적합하지 않은 상황에서 해결책은 redux이다.
