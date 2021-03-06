# React - route

- 페이지를 전환하는 것

<br>

##### React - route 참고 사이트

https://reactrouter.com/docs/en/v6/getting-started/tutorial

<br>

### route 사용하기

1. Router package 설치

```
// 6버전
npm install react-router-dom@6
```

<br>

2. componet 폴더, routes 폴더에 js파일 분류하기

<br>

3. react-router-dom import

- hash router - #이 붙은 url형태
- browser router - 일반적인 url과 같은 형태

<br>

4. Routes

- Routes 태그 안에 맞는 조건의 Route를 선택한다.

<br>

5. Route

- 이동할 url을 path 값에 적어주고, 이동할 페이지를 element 값에 적어준다.

<br>

#### App.js

```
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Detail from './routes/Detail';

<BrowserRouter>
  <Routes>
    // /를 입력하면 Home Component 호출
    <Route path='/' element={<Home />}></Route>

    // /movie를 입력하면 Detail Component 호출
    <Route path='/movie' element={<Detail />}></Route>

    // /drama/ + 키워드를 입력하면 Drama Component 호출
    <Route path='/drama/:genre' element={<Drama />}></Route>

  </Routes>
</BrowserRouter>
```

<br>

### Link Component 사용하기

- a태그는 페이지 이동과 함께 브라우저를 새로고침한다.
- 5.의 문제를 해결하기 위해 link component 사용한다.(SPA, 새로고침 발생x )

<br>

##### React - Link Component 참고 사이트

```
https://reactrouter.com/docs/en/v6/components/link
```

<br>

1. link component 를 import한다.

```
import { Link } from 'react-router-dom';
```

<br>

#### Movie.js

```
// Link Component Import
import { Link } from 'react-router-dom';

// Link Component 사용
<Link to='/movie'>{title}</Link>
```

<br>

### url 이동할 때 동적 데이터 전달하기

<br>

1. 데이터를 전달할 때는 콜론을 작성해주자

```
path='/movie/:id'
```

<br>

> path='/movie/id'에서 콜론을 제거하면 id를 텍스트 자체로 인식하여
> /movie/id 로 이동하게 된다.

<br>

#### App.js

```
  <Route path='/movie/:id' element={<Detail />}></Route>
```

<br>

#### Movie.js

```
<h2>
  <Link to={`/movie/${id}`}>{title}</Link>
</h2>
```

<br>

### url 이동할 때 동적 데이터 전달 받기

<br>

#### Detail.js

1. useParams를 import 해준다.

```
import { useParams } from 'react-router-dom';
```

<br>

2. 전달 받은 데이터를 useParams 함수로부터 할당 받는다.

```
const { id } = useParams();
```

<br>

### useNavigate 사용하기

- v6버전 이전에서는 useHistory를 사용할 수 있었다.
- useNavigate를 통해 뒤로가기, 페이지 이동이 가능하다.
  <br>

```
// useNavigate를 받아줄 객체를 생성한다.
const navigate = useNavigate();

// Link와 사용법은 일맥상통하다.
<button onClick={() => navigate('/')}>Main페이지</button>

// 뒤로가기
<button onClick={() => navigate(-1)}>Main페이지</button>
```

<br>

### PageNotFound page만들기

```
<Route path={'*'} element={<NotFound />}></Route>

// NotFound.js
<div>
  <h1>존재하지 않는 페이지입니다.</h1>
  <button onClick={() => navigate(-1)}>뒤로가기</button>
</div>
```
