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
let count = 0;
count += 1;
count = '문자열'; // 에러

const message: string = '문자열';

const done: boolena = true;

const numbers: number[] = [1, 2, 3];
const messages: string[] = ['문', '자', '열'];

messages.push(1); // 에러

let mightBeUndefined: string | undefined = undefined;
let nullableNumber: number | null = null;

let color: 'red' | 'orange' | 'yellow' = 'red';
color = 'yellow';
color = 'green'; // 에러
```
