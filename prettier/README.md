# prettier 스타일 가이드

> 이 스타일 가이드는 [Prettier](https://prettier.io/docs/en/options)를 참조하여 작성되었습니다.
 
Prettier는 코드 포멧터로, 코드를 일관되게 유지하는 데 사용됩니다.  
.prettierrc 파일에 Prettier의 설정을 정의하는 JSON 파일입니다.

## 1.Prettier 설치
### 프로젝트에 Prettier 설치(필수)
```bash
npm install --save-dev prettier
```
### IDE 확장 프로그램 설치(권장)
Prettier를 사용하려면 IDE에 Prettier 확장 프로그램을 설치해야 합니다.  
- Visual Studio Code: "Prettier - Code formatter" 확장 프로그램 설치
- WebStorm: 내장된 "Prettier" 지원 활성화

## 2. Prettier 설정
### .prettierrc 파일 경로
root 디렉토리에 .prettierrc 파일을 생성합니다.

### .prettierignore 파일 경로(선택)
root 디렉토리에 .prettierignore 파일을 생성하여 Prettier에서 무시할 파일을 지정합니다.


## 3. .prettierrc 옵션 설명
```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5",
  "tabWidth": 2,
  "useTabs": false,
  "printWidth": 80,
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "lf",
  "jsxSingleQuote": false,
  "bracketSameLine": false
}
```

### 1. semi: 세미콜론 사용 여부  
명령문 끝에 세미콜론(;)을 자동으로 추가할지 여부입니다.
>- true: 명령문 끝에 세미콜론(;)을 자동으로 추가합니다. (기본값)
>- false: 세미콜론을 생략합니다.
```js
// semi: true
const name = 'John';

// semi: false
const name = 'John'
```
---
### 2. singleQuote: 작은따옴표 사용 여부  
문자열에 큰따옴표(") 대신 작은따옴표(')를 사용할지 여부입니다.
>- true: 작은따옴표(')를 사용
>- false: 큰따옴표(")를 사용 (기본값)
```js
// singleQuote: true
const greeting = 'Hello, World!';

// singleQuote: false
const greeting = "Hello, World!";
```
---
### 3. trailingComma: 마지막 요소 뒤에 쉼표 사용 여부  
객체, 배열 등에서 마지막 요소 뒤에 쉼표를 넣을지 여부입니다.

>- none: 쉼표 없음
>- es5: ES5에서 유효한 곳(배열, 객체 등)에는 쉼표를 추가 (기본값)
>- all: 가능한 모든 곳에 쉼표를 추가(함수의 안자값에도 쉼표 표시)
```js
// 배열, 객체 

// trailingComma: none
const array = [
    'apple',
    'banana'
];

// trailingComma: es5
// trailingComma: all
const array = [
    'apple',
    'banana', // 배열 마지막 요소에 쉼표 추가
];
```
```js
// 함수

// trailingComma: none
// trailingComma: es5
function greet(
    name,
    age
) {
    console.log(`Hello, ${name}! You are ${age} years old.`);
}

// trailingComma: all
function greet(
    name,
    age, // 함수의 마지막 인자에 쉼표 추가
) {
    console.log(`Hello, ${name}! You are ${age} years old.`);
}
```
---
### 4. tabWidth: 탭의 너비 설정
탭의 공백을 몇 칸으로 대체할지를 결정합니다.
> 기본값: 2
```js
// tabWidth: 2
function greet() {
  console.log('Hello!');
}

// tabWidth: 4
function greet() {
    console.log('Hello!');
}
```
---
### 5. useTabs:  탭 대신 공백을 사용 여부
>- true: 탭 사용
>- false: 공백 사용 (기본값)
```js
// useTabs: true (탭 사용)
function greet() {
→console.log('Hello!');
}

// useTabs: false (공백 사용)
function greet() {
··console.log('Hello!');
}
```
(→: 탭 문자, ··: 공백 2칸)

---

### 6. printWidth: 한 줄의 최대 길이   
한 줄의 최대 길이를 설정합니다. 이 길이를 넘으면 줄바꿈을 합니다.
> 기본값: 80
```js
// printWidth: 80
function greet() {
  console.log('This is a long sentence that will wrap to the next line after it exceeds 80 characters.');
}
```
---
### 7. bracketSpacing: 중괄호 사이의 공백 여부  
객체 리터럴에서 중괄호 사이에 공백을 넣을지 여부입니다.
>- true: 중괄호 안에 공백 넣음 (기본값)
>- false: 중괄호 안에 공백 넣지 않음
```js
// bracketSpacing: true
const object = { foo: bar }

// bracketSpacing: false
const object = {foo: bar}
```
---
### 8. arrowParens: 화살표 함수 매개변수 괄호 사용 여부  
화살표 함수에서 매개변수가 하나일 때 괄호를 사용할지 여부입니다.
>- always: 괄호 사용 (기본값)
>- avoid: 괄호 생략
```js
// arrowParens: always
const greet = (name) => `Hello, ${name}`;

// arrowParens: avoid
const greet = name => `Hello, ${name}`;
```
---
### 9. endOfLine: 줄바꿈 문자 설정
줄바꿈(줄 끝)에 사용할 문자를 설정합니다.
>- lf: \n - Unix 및 macOS 줄바꿈 문자(LF) (기본값)
>- crlf: \r\n - Windows 줄바꿈 문자(CRLF) 
>- cr: \r - Macintosh 줄바꿈 문자(CR) 
>- auto: 파일의 첫 줄바꿈 문자에 따라 설정
---
### 10. jsxSingleQuote: JSX에서 작은따옴표 사용 여부
JSX에서 문자열에 작은따옴표(')를 사용할지 여부입니다.
>- true: 작은따옴표(')를 사용
>- false: 큰따옴표(")를 사용 (기본값)
```js
// jsxSingleQuote: true
const element = <div className='container'></div>;

// jsxSingleQuote: false
const element = <div className="container"></div>;
```
---
### 11. bracketSameLine: 중괄호 위치 설정
JSX 요소의 마지막 중괄호(`>`)를 같은 줄에 둘지 다음 줄로 내릴지 설정합니다.
>- true: 같은 줄에 둠
>- false: 다음 줄로 내림 (기본값)
```js
// bracketSameLine: true
<button
    className="prettier-class"
    id="prettier-id"
    onClick={this.handleClick}>
    Click Here
</button>

// bracketSameLine: false
<button
    className="prettier-class"
    id="prettier-id"
    onClick={this.handleClick}
>
    Click Here
</button>
```

---
#### 버전 및 수정정보
현재버전: 0.0.2  

수정이력:
- 2024.11.04(v.0.0.2): Prettier 설치 방법 및 .prettierrc 옵션 설명 추가
- 2024.09.16(v.0.0.1): 초기 문서 작성
