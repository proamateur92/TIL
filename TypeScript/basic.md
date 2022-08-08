# TypeScript

## 특징

- 컴파일 언어, 정적 타입 언어
  - 자바스크립트는 동적 타입의 인터프리터 언어로 런타임에서 오류를 발견할 수 있습니다. 이에 반해 타입스크립트는 정적 타입의 컴파일 언어이며 타입스크립트 컴파일러 또는 바벨(Babel)을 통해 자바스크립트 코드로 변환됩니다. 코드 작성 단계에서 타입을 체크해 오류를 확인할 수 있고 미리 타입을 결정하기 때문에 실행 속도가 매우 빠르다는 장점이 있습니다. 하지만 코드 작성 시 매번 타입을 결정해야 하기 때문에 번거롭고 코드량이 증가하며 컴파일 시간이 오래 걸린다는 단점이 있습니다.

<br>

- 자바스크립트 슈퍼셋(Superset)
  - 타입스크립트는 자바스크립트의 슈퍼셋, 즉 자바스크립트 기본 문법에 타입스크립트의 문법을 추가한 언어입니다. 따라서 유효한 자바스크립트로 작성한 코드는 확장자를 .js에서 .ts로 변경하고 타입스크립트로 컴파일해 변환할 수 있습니다.

<br>

## 기본 문법

```
// permtivie types

let count = 0;
count += 1;
count = '문자열'; // 에러

const message: string = '문자열';

const done: boolena = true;

// more complex types
// array type

const numbers: number[] = [1, 2, 3];
const messages: string[] = ['문', '자', '열'];

messages.push(1); // 에러

// Object type

let person: {
  name: string;
  age: number;
};  // any; 어느 타입이든 들어올 수 있다. 사용 지양할 것.

person = {
  name: '홍길동',
  age: 22,
}

// person = {
//   isAdult: true
// };

// 객체 배열을 가지는 변수
let people: {
  name: string;
  age: number;
}[];
```

<br>

## 타입 추론

```
// 타입을 명시하지 않아도 적용된다.

let course = '강좌 제목';
// let course: string = '강좌 제목'; 불필요한 타입 선언
// couse = 1234; // 에러
```

<br>

## 유니온 타입

```
//여러 타입을 명시해줄 수 있다.

let userName = string | string[];
let phoneNumber string | number = 01011112222;
phoneNumber = '01011112222';

let mightBeUndefined: string | undefined = undefined;
let nullableNumber: number | null = null;

let color: 'red' | 'orange' | 'yellow' = 'red';
color = 'yellow';
color = 'green'; // 에러
```

<br>

## 타입 별칭

```
// 공통된 타입을 가지는 변수로부터 별칭을 가져와 변수에게 별칭을 선언

type Person = {
  name: string;
  age: number;
}

let person: Person;
person = {
  name: '아무개',
  age: 33
}

let people: Person[];
```

<br>

## 함수 & 타입

```
function add(a: number, b:number) {
  //: number -> return 타입을 명시하거나 타입 추론을 통해 지정하지 않아도 된다.
  return a + b;
}

function printOutput(value: any) {
  //: void -> return 값이 없을때 사용.(함수에서만 사용된다.)
  coonsole.log(value);
}

```

<br>

## 제네릭

```
// 제네릭 적용 전

// any로 타인을 선언해주어 특정 타입의 배열이 오는 것을 알 수 없다.
// array: number[]로 선언해준다면 유틸리티 함수로서 문자열 배열이 들어왔을 때 함수가 제 기능을 하지 못한다.
const insertNewValue(array: any[], value: any) {
  const newArray = [value, ...array];
  return newArray;
}

const demoArray = [1, 2, 3];

const updatedArray = inserNewValue(demoArray, -1); // [-1, 1, 2, 3]
```

<br>

```
// 제네릭 적용 후
// 타입스크립트는 제네릭 타입을 통해 호출된 함수의 타입을 알 수 있다.

const insertNewValue<T>(array: T[], value: T) {
  const newArray = [value, ...array];
  return newArray;
}

const demoArray = [1, 2, 3];

// 제네릭 적용 전에는 문자열 배열에만 사용하는 함수를 사용하더라도 런타임 단계에서 오류를 발생했다.
// 제네릭 적용 후에는 문자열 함수 선언 때 부터 오류를 발생한다.
const updatedArray = inserNewValue(demoArray, -1); // [-1, 1, 2, 3]

const stringArray = inserNewValue(['a', 'b', 'c'], 'd'); // ['a', 'b', 'c', 'd]
```
