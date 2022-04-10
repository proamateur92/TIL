# Promise

- 비동기적으로 처리되는 객체 타입

<br>
Promise 객체는 3가지의 상태를 가진다.
<br>
<br>
1. pending - 대기상태
<br>
2. fullfilled - promise 이행(resolve를 콜백함수로 받는다.)
<br>
3. rejected - promise 거부(reject를 콜백함수로 받는다.)
<br>
<br>

```
  let promise = new Promise((resolve, reject) => {
    //executor
    resolve(return '')
  });
```

<br>

```
  promise
    .then((res) => { // promise 이행 시 리턴 값
      console.log(res);
    })
    .catch((err) => { // promise 거부 시 리턴 값
      console.log(err);
    })
    .finally(
      console.log('promise 이행 여부 상관없이 무조건 실행')
    );
```
