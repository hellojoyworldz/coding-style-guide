# JavaScript Style Guide

> 이 스타일 가이드는 [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript), [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html), [StandardJS](https://standardjs.com/), [MDN Web Docs](https://developer.mozilla.org/), [Clean Code JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)를 참고하여 작성되었습니다.


## 목차
명명 규칙  
코드 포맷팅  
코드 구성  
기본 원칙  
최신 문법 활용  
성능 고려사항  
주석 작성 규칙  
에러 처리  
비동기 처리  

## 명명 규칙(Naming Conventions)
### 변수명
- 기본적으로 변수명은 camelCase를 사용합니다.
- 명확하고 발음 가능한 이름을 사용합니다.
- 검색 가능한 의미있는 이름을 사용합니다.
- 약어는 피하고 전체 단어 사용을 권장합니다.
- 약어 사용 시 널리 알려진 약어만 사용합니다.
- 약어는 전체 대문자로 표기하지 않습니다.

```js
// bad
const yyyymmdstr = moment().format('YYYY/MM/DD');   // 명확하지 않은 이름
const n = 10;                                       // 의미없는 이름
const fn = 'John';                                  // 약어 사용 지양
const bgCol = '#fff';                               // 약어 사용 지양
const userID = 1;                                   // 약어는 전체 대문자로 표기하지 않음


// good
const currentDate = moment().format('YYYY/MM/DD');
const maxCount = 10;
const firstName = 'John';
const backgroundColor = '#fff';
const userId = 1;
```

#### Array
- 배열명은 복수형으로 작성합니다.
- 배열임을 나타내는 접미나 List, Array 등은 사용하지 않습니다.
    
```js
// bad
const namesList = ['John', 'Jane', 'Jim'];  // List 접미사 불필요   
const color = ['#fff', '#000', '#f00'];     // 단수형 사용
const array = [1,2,3];                      // 의미없는 이름

// good
const names = ['John', 'Jane', 'Jim'];
const colors = ['#fff', '#000', '#f00'];
const activeItems = [1,2,3];
```

#### Object
- 객체명은 단수형으로 작성합니다.
- 객체임을 나타내는 접미사 Object, Map, Set 등은 사용하지 않습니다.

```js
// bad
const userObject = {name:'John', age:30};           // Object 접미사 불필요
const obj = {theme:'dark', lang:'en'};              // 의미없는 이름
const data = {brand:'Hyundai', model:'Sonata'};     // 너무 모호함

// good
const user = {name:'John', age:30};
const config = {theme:'dark', lang:'en'};
const car = {brand:'Hyundai', model:'Sonata'};
```

#### Boolean
- Boolean 변수명은 is의 접두사를 사용합니다.
- Boolean 변수명은 긍정을 true로 표현합니다.
- Boolean 변수명은 긍정문을 사용하며 부정문은 지양합니다.

```js
// bad
let visible = false;      // 동사로 시작하지 않음
let isHidden = false;     // 부정이 true로 표현됨
let notActive = true;     // 부정문 사용
let processing = true;    // 현재 상태가 불분명함

// good
let isVisible = true;
let isShow  = true;
let isActive = true;
```

#### Class
- 클래스명은 PascalCase를 사용합니다.
- 클래스명은 명사로 작성합니다.

```js
// bad
class userProfile{} // camelCase 사용
class DoThis{}      // 동사 사용

// good
class UserProfile{}
class PaymentProcessor{}

```
#### Constant
- 상수명은 UPPER_SNAKE_CASE(대문자와 언더스코어)를 사용합니다.
- 명확한 의미 전달을 해야합니다.
- 값이 절대 변하지 않는 경우에만 사용합니다.

```js
// bad
const taxRate = 0.1;            // camelCase 사용
const API = 'https://api.com';  // 명확한 의미정보 부족
const TIMEOUT = 5000;           // 단위 정보 누락

// good
const TAX_RATE = 0.1;
const API_BASE_URL = 'https://api.com';
const DEFAULT_TIMEOUT_MS = 5000;
```

### 함수명
- 함수명은 camelCase를 사용합니다.
- 함수명은 동사 + 명사 형태로 작성합니다.
- 함수명은 명확하고 간결하게 작성합니다.
- 함수명은 기능을 설명하도록 작성합니다.
- handle, get, calculate, validate, fetch, create, update, delete 등의 접두사를 사용합니다.

```js
// bad
function user_data(){}             // snake_case 사용
function DoThing(){}               // PascalCase 사용
function useProfileGet() {}        // 동사로 시작하지 않음
function handle(){}                // 너무 모호함

// good
function getUserProfile(){}
function calculateTotal(){}
function validateEmail(){}
function handleClick(){}
```

#### 이벤트 핸들러
- 이벤트 핸들러 함수명은 handle + 이벤트명 형태로 작성합니다.
- props로 넘길 경우 on + 이벤트명 형태로 넘깁니다.
- 어떤 기능을 가지고 있는지 유추할 수 있도록 작성합니다.
```js
// bad
<button onClick={handleClick1}>리셋 버튼</button>
<button onClick={handleClick2}>제출 버튼</button>

// good 
<button onClick={handleResetClick}>리셋 버튼</button>
<button onClick={handleSubmitClick}>제출 버튼</button>
```
```js
// props로 넘길 경우
<button onResetClick={handleResetClick}>리셋 버튼</button>
<button onSubmitClick={handleSubmitClick}>제출 버튼</button>
```

#### 유틸 함수
- 유틸함수가 반환하는 값을 기준으로 함수명을 작성합니다.
- boolean 값을 반환하는 경우 has + 명사 형태로 작성합니다.
- 데이터에서 추출한 값을 반환하는 경우 get + 명사 형태로 작성합니다.
- 데이터를 계산하는 경우 calculate + 명사 형태로 작성합니다.
- 데이터를 검증하는 경우 validate + 명사 형태로 작성합니다
- 데이터를 변환하는 경우 convert + 명사 형태로 작성합니다.
- 데이터를 필터링하는 경우 filter + 명사 형태로 작성합니다.
- 데이터를 정렬하는 경우 sort + 명사 형태로 작성합니다.

```js
const hasUser = () => {}
const getUserById = () => {}
const calculateTotal = () => {}
const validateEmail = () => {}
const convertToCamelCase = () => {}
const filterActiveUsers = () => {}
const sortUsersByAge = () => {}
```

#### API 요청 함수
- API 요청 함수명은 fetch + 명사 형태로 작성합니다.
- create, read, update, delete(CRUD)에 따라 함수명을 작성합니다.
```js
// API 요청
const fetchUser = () => {}

// 추가
const createUser = () => {}

// 수정
const updateUser = () => {}

// 1개 삭제
const deleteUser = () => {}

// 전체 삭제
const removeUser = () => {}
```

---
#### 버전 및 수정정보
현재버전: 0.0.2

수정이력:
- 2024.11.04(v.0.0.2): 명명 규칙 작성
- 2024.11.04(v.0.0.1): 초기 문서 작성
