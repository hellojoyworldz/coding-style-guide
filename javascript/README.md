# JavaScript Style Guide

> 이 스타일 가이드는 [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript), [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html), [StandardJS](https://standardjs.com/), [MDN Web Docs](https://developer.mozilla.org/), [Clean Code JavaScript](https://github.com/ryanmcdermott/clean-code-javascript), [Toast UI Coding Convention](https://ui.toast.com/fe-guide/ko_CODING-CONVENTION)를 참고하여 작성되었습니다.


## 목차
명명 규칙  
코드 구성   
주석 작성 규칙  
성능 고려사항  

에러 처리  
비동기 처리
조건 확인

## 명명 규칙(Naming Conventions)
### 변수명
- 기본적으로 변수명은 camelCase를 사용합니다.(Class, Constant 제외)
- 명확하고 발음 가능한 이름을 사용합니다.
- 검색 가능한 의미있는 이름을 사용합니다.
- 약어는 피하고 전체 단어 사용을 권장합니다.
- 약어는 전체 대문자로 표기하지 않습니다.

```js
// bad
const yyyymmdstr = moment().format('YYYY/MM/DD');   // 명확하지 않은 이름
const n = 10;                                       // 의미없는 이름
const fn = 'John';                                  // 약어 사용 지양
const bgCol = '#fff';                               // 약어 사용 지양
const userID = 1;                                   // 약어는 전체 대문자로 표기하지 않음

// ✅ good
const currentDate = moment().format('YYYY/MM/DD');  // 명확한 이름
const maxCount = 10;                                // 의미 있는 이름
const firstName = 'John';                           // 약어를 풀어서 사용
const backgroundColor = '#fff';                     // 약어를 풀어서 사용
const userId = 1;                                   // 약어도 camelCase에 맞게 일관성 유지
```

#### 예약어 사용 금지

#### Array
- 배열명은 복수형으로 작성합니다.
- 배열임을 나타내는 접미나 List, Array 등은 사용하지 않습니다.

```js
// bad
const namesList = ['John', 'Jane', 'Jim'];  // List 접미사 불필요   
const color = ['#fff', '#000', '#f00'];     // 단수형 사용
const array = [1,2,3];                      // 의미없는 이름

// ✅ good
const names = ['John', 'Jane', 'Jim'];      // 복수형 사용
const colors = ['#fff', '#000', '#f00'];    // 복수형 사용으로 의미 명확화
const activeItems = [1,2,3];                // 구체적인 배열의 의미 전달
```

#### Object
- 객체명은 단수형으로 작성합니다.
- 객체임을 나타내는 접미사 Object, Map, Set 등은 사용하지 않습니다.

```js
// ❌ bad
const userObject = { name:'John', age:30 };           // Object 접미사 불필요
const obj = { theme:'dark', lang:'en' };              // 의미없는 이름
const data = { brand:'Hyundai', model:'Sonata' };     // 너무 모호함

// 👍🏻 good
const user = { name:'John', age:30 };                 // 명확한 단수형 이름
const config = { theme:'dark', lang:'en' };           // 객체의 용도를 명확히 표현
const car = { brand:'Hyundai', model:'Sonata' };      // 객체의 의미를 직관적으로 표현
```

#### Boolean
- Boolean 변수명은 is, has, can 의 접두사를 사용합니다.
- Boolean 변수명은 긍정문을 사용하여 true로 표현합니다.
- Boolean 변수명은 부정문은 지양합니다.

```js
// bad
let visible = false;         // 동사로 시작하지 않음
let isHidden = false;        // 부정이 true로 표현
let notActive = true;        // 부정문 사용
let processing = true;       // 현재 상태가 불분명함

// 👍🏻 good
let isVisible = true;        // 동사로 시작
let isShow  = true;          // 긍정이 true로 표현
let isActive = true;         // 긍정문 사용
let isProcessing = true;     // 현재 상태를 명확히 전달
```

#### Class
- 클래스명은 PascalCase를 사용합니다.
- 클래스명은 명사로 작성합니다.

```js
// bad
class userProfile{} // camelCase 사용
class DoThis{}      // 동사 사용

// 👍🏻 good
class UserProfile{}      // PascalCase 사용
class PaymentProcessor{} // 명사 사용

```
#### Constant
- 상수명은 UPPER_SNAKE_CASE(대문자와 언더스코어)를 사용합니다.
- 상수명은 명확한 의미 전달을 해야합니다.
- 값이 절대 변하지 않는 경우에만 상수를 사용합니다.

```js
// bad
const taxRate = 0.1;            // camelCase 사용
const API = 'https://api.com';  // 명확한 의미정보 부족
const TIMEOUT = 5000;           // 단위 정보 누락으로 명확하지 않음

// 👍🏻 good
const TAX_RATE = 0.1;                   // 대문자와 언더스코어 사용
const API_BASE_URL = 'https://api.com'; // 명확한 정보 제공
const DEFAULT_TIMEOUT_MS = 5000;        // 단위 정보 포함으로 명확한 정보 제공
```

### 함수명
- 함수명은 camelCase를 사용합니다.
- 함수명은 동사 + 명사 형태로 작성합니다.
- 함수명은 수행하는 기능을 설명 가능하도록 작성합니다.
- handle, get, calculate, validate, fetch, create, update, delete 등의 접두사를 사용합니다.

```js
// ❌ bad
function user_data(){}             // snake_case 사용
function DoThing(){}               // PascalCase 사용
function useProfileGet() {}        // 동사로 시작하지 않음
function handle(){}                // 너무 모호한 이름

// ✅ good
function getUserProfile(){}     // 동사 + 명사 형태
function calculateTotal(){}     // 함수 기능에 맞는 이름 사용
function validateEmail(){}      // 수행하는 작업이 구체적으로 드러남
function handleClick(){}        // 기능이 명확하게 드러남
```

#### 이벤트 핸들러
- 이벤트 핸들러 함수명은 handle + 이벤트명 형태로 작성합니다.
- props로 넘길 경우 on + 이벤트명 형태로 사용합니다.
- 어떤 기능을 가지고 있는지 유추할 수 있도록 작성합니다.
```js
// ❌ bad
<button onClick={handleClick1}>리셋 버튼</button>
<button onClick={handleClick2}>제출 버튼</button>

// 👍🏻 good 
<button onClick={handleResetClick}>리셋 버튼</button>
<button onClick={handleSubmitClick}>제출 버튼</button>
```
```js
// props로 넘길 경우
<button onResetClick={handleResetClick}>리셋 버튼</button>
<button onSubmitClick={handleSubmitClick}>제출 버튼</button>
```


#### 유틸 함수
- 유틸함수가 반환하는 값이나 수행하는 작업을 기준으로 함수명을 작성합니다.
- boolean 값을 반환하는 경우 is, has, can + 명사 형태로 작성합니다.
- 데이터를 추출할 경우 get + 명사 형태로 작성합니다.
- 데이터를 설정할 경우 set + 명사 형태로 작성합니다.
- 테이터를 갱신할 경우 refresh + 명사 형태로 작성합니다.
- 데이터를 변경할 경우 modify/change + 명사 형태로 작성합니다
- 데이터를 제거할 경우 remove + 명사 형태로 작성합니다.
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

#### API 요청 관련 함수
- HTTP Method에 따라 함수명을 작성합니다.
- 조회 - GET 요청은 fetch + 명사 형태로 작성합니다.
- 생성 - POST 요청은 create + 명사 형태로 작성합니다.
- 수정 - PUT, PATCH 요청은 update + 명사 형태로 작성합니다.
- 삭제 - DELETE 요청은 delete + 명사 형태로 작성합니다.

```js
// 조회 (GET)
const fetchUsers = () => {}

// 생성 (POST)
const createUser = () => {}

// 수정 (PUT/PATCH)
const updateUser = () => {}

// 삭제 (DELETE)
const deleteUser = () => {}
```

##### 조회
- 목록 조회는 복수형으로 작성하고 단일 항목 조회는 단수형으로 작성합니다.
- 특정 속성을 조회하는 경우 조회하는 속성을 명시합니다.
- 식별자 명시가 필요한 경우 by + 속성명 형태로 작성합니다.

```js
// 목록 조회
const fetchUsers = () => {}
const fetchUsersEmails = () => {}

// 단일 항목 조회
const fetchUsersEmails = () => {}
const fetchUserEamil = (userId) => {}

// 식별자 명시
const fetchUserEmailById = (userId) => {}
```

##### 삭제
- 단일 항목 삭제는 단수형, 여러 항목 삭제는 복수형으로 작성합니다.
- 전체 삭제의 경우 deletetAll 을 사용합니다.

```js
// 단일 항목 삭제
const deleteUser = (userId) => {}

// 여러 항목 삭제
const deleteUsers = (userIds) => {}

// 전체 삭제
const deleteAllUsers = () => {}
```

### 폴더명
- 일반적으로 폴더명은 kebab-case를 사용합니다.
- 폴더명은 명사 복수형으로 작성합니다.
- 폴더의 용도나 목적을 명확히 표현합니다.

```js
// ❌ bad
util_functions/        // snake_case 사용
util/                  // 단수형 사용
component/             // 단수형 사용
imgs/                  // 약어 사용
        
// ✅ good
utils/                 // 복수형 사용
components/            // 복수형 사용
images/                // 전체 단어 사용
```
```js
// 프로젝트 구조 예시
src/
  assets/             // 정적 파일들
  components/         // 재사용 컴포넌트들
  pages/              // 페이지 컴포넌트들
  hooks/              // 커스텀 훅들
  utils/              // 유틸리티 함수들
  apis/               // API 관련 파일들
  contexts/           // Context 파일들
  constants/          // 상수 파일들
  types/              // 타입 정의 파일들
  styles/             // 스타일 관련 파일들
```

### 파일명
- 일반적으로 파일명은 kebab-case를 사용합니다.
- 파일명은 명사로 작성합니다.
- 파일의 용도나 목적을 명확히 표현합니다.
```js
// bad
userProfile.js        // camelCase 사용
UserProfile.js        // PascalCase 사용
user_profile.js       // snake_case 사용
usrprof.js            // 약어 사용

// good
user-profile.js        // kebab-case 사용
auth-validator.js      // 파일 목적 명확
api-error-handler.js   // 전체 단어 사용
```

### API 관련 파일
- API 관련 파일명은 kebab-case를 사용합니다.
- API 관련 파일은 용도와 리소스를 명확히 표현합니다.
- 특정 도메인이나 기능별로 구분하여 작성합니다.
```js
// bad
api.js               // 너무 일반적인 이름
userAPI.js           // camelCase 사용
UserRequests.js      // PascalCase 사용

// good
user-api.js          // 사용자 관련 API
auth-service.js      // 인증 관련 서비스
product-repository.js // 상품 관련 저장소
```

### 컴포넌트 파일
- 컴포넌트 파일은 PascalCase 사용을 권장하며, kebab-case를 사용할 수 있습니다.
- 컴포넌트의 역할이나 기능을 명확히 표현합니다.
```js
// bad
userprofile.jsx        // camelCase 사용
user_profile.jsx       // snake_case 사용

// good
UserProfile.jsx        // PascalCase 사용
user-profile.jsx       // kebab-case 사용
```

### 이미지 파일
- 이미지 파일명은 kebab-case를 사용합니다.
- 이미지의 용도나 내용을 명확히 표현합니다.
- button-, icon-, thumb- 등 접두사로 이미지의 종류나 용도를 표현할 수 있습니다.
- -light, -dark 등 접미사로 이미지의 테마를 표현할 수 있습니다.
- -1x, -2x, -3x 등 접미사로 이미지의 해상도를 표현할 수 있습니다.

```js
// bad
mainBanner.jpg        // camelCase 사용
Image_1234.png            // 의미 없는 이름

// good
main-banner.jpg       // kebab-case 사용
button-close.png      // 이미지의 용도 명확히 표현
icon-sns-facebook.png // 이미지의 종류와 용도 명확히 표현
thumb-product.jpg     // 이미지의 용도 명확히 표현
logo-dark-2x.png      // 이미지의 테마와 해상도 명시
icon-email-2x.png     // 이미지의 해상도 명시
```

### 파일 접미사 규칙
- 같은 폴더 내 파일의 용도나 종류를 구분하기 위해 접미사를 사용합니다.
- 컴포넌트가 PascalCase인 경우 PascalCase인를, 그 외의 경우 kebab-case를 사용합니다.
- 접미사는 점(.)으로 구분합니다.
- 파일 확장자 앞에 위치합니다.
```js
components/Button/
  Button.tsx           // 컴포넌트
  Button.styles.ts     // 스타일 
  Button.test.tsx      // 테스트
  Button.types.ts      // 타입 정의

services/auth/
  auth.ts              // 주요 로직
  auth.constants.ts    // 상수
  auth.types.ts        // 타입 정의
  auth.test.ts         // 테스트
  auth.utils.ts        // 유틸리티
```

#### 테스트 파일
- 타입 정의를 별도 파일로 분리할 때 사용합니다.
- 테스트 대상 파일명 뒤에 .test 또는 .spec 접미사를 사용합니다.
- 테스트 대상 파일명과 일치하도록 작성합니다.

```js
// 테스트 대상 파일
UserProfile.js             
user-profile.js

// bad
UserProfileTest.js        // 접미사를 점으로 구분하지 않음
user-profile-test.js      // 테스트 대상 파일명과 일치하지 않음

// good
UserProfile.test.js       // 점으로 접미사 구분
user-profile.spec.js      // 테스트 대상 파일명과 일치
```

#### 타입 정의 파일
- TypeScript 타입 정의를 별도 파일로 분리할 때 사용합니다.
- 타입 정의 파일명 뒤에 .types 접미사를 사용합니다.
- 타입 정의 파일명과 일치하도록 작성합니다.
```js
// 타입 정의 대상 파일
UserProfile.ts          
user-profile.ts

// bad
UserProfileType.ts               // 접미사를 점으로 구분하지 않음
user-profile-type.ts              // 타입 정의 파일명과 일치하지 않음

// good
UserProfile.types.ts             // 점으로 접미사 구분
user-profile.types.ts             // 타입 정의 파일명과 일치
```

#### 스타일 파일
- 스타일 파일명 뒤에 .styles 접미사를 사용합니다.
- CSS Module을 사용할 때는 .styles.module 접미사를 사용합니다.
- 
```js
// 타입 정의 대상 파일
UserProfile.js
user-profile.js

// bad
UserProfileStyle.css       // 접미사를 점으로 구분하지 않음
user-profile-style.css     // 스타일 파일명과 일치하지 않음

// good
UserProfile.styles.css     // 점으로 접미사 구분
user-profile.styles.module.css    // CSS Module 사용 시
```

#### 상수 파일
- 상수 파일명 뒤에 .constants 접미사를 사용합니다.
```js
// 타입 정의 대상 파일
UserProfile.js
user-profile.js

// bad
UserProfileConstants.js          // 접미사를 점으로 구분하지 않음
user-profile-constants.js         // 상수 파일명과 일치하지 않음

// good
UserProfile.constants.js         // 점으로 접미사 구분
user-profile.constants.js         // 상수 파일명과 일치
```

#### 유틸리티 파일
- 유틸리티 파일명 뒤에 .utils 접미사를 사용합니다.
```js 
// 타입 정의 대상 파일
UserProfile.js
user-profile.js

// bad
UserProfileUtil.js               // 접미사를 점으로 구분하지 않음
user-profile-util.js              // 유틸리티 파일명과 일치하지 않음

// good
UserProfile.utils.js             // 점으로 접미사 구분
user-profile.utils.js             // 유틸리티 파일명과 일치
```

## 코드 구성
### 모듈 시스템
- 모듈시스템은 CommonJS와 ES Modules 두 가지가 있습니다.
- 프로젝트 내에서 하나의 모듈 시스템으로 통일하는 것이 바람직합니다.
- ES Modules 사용 시 package.json 파일에 type: module을 추가합니다.
```json
// package.json
{
  "type": "module"    
}
```

#### CommonJS
- 확장자가 cjs 또는 js인 파일은 CommonJS를 사용합니다.
- CommonJS 시스템은 require() 함수를 사용하여 모듈을 불러옵니다.
- module.exports 또는 export 객체를 사용하여 모듈을 내보냅니다.

```js
// 불러오기
const express = require('express');
const { helper } = require('./helper');

// 내보내기
module.exports = class Service { };
// 또는
exports.helper = { };
````

#### ES Modules
- 확장자가 mjs 또는 js인 파일은 ES Modules를 사용합니다.
- 모듈 시스템은 ES6의 import/export 구문을 사용하여 모듈을 불러옵니다.
- export 또는 export default를 사용하여 모듈을 내보냅니다.
- 
```js
// 불러오기
import React from 'react';
import { useState } from 'react';
import * as utils from './utils';

// 내보내기
export default class Service { }    
export const helper = { };
````

#### 혼용 시 주의사항
- 한 프로젝트 내에서는 하나의 모듈 시스템을 사용하여 일관성을 유지합니다.
- 부득이하게 혼용해야 할 경우 파일 확장자로 명확히 구분합니다.
  - .mjs: ES Modules 전용
  - .cjs: CommonJS 전용
  - .js: package.json의 "type" 필드 설정을 따름

### 모듈 설계 원칙
- 모듈은 단일 책임 원칙을 준수하여 작성합니다.
- 모듈은 재사용 가능하도록 설계합니다.
- 모듈은 의존성을 최소화하여 결합도를 낮춥니다.

```js
// Good - 단일 책임 원칙 준수
// 사용자 관리와 관련된 기능만 포함하여 단일 책임 원칙을 준수합니다.
class UserService {
  getUser() { }
  updateUser() { }
  deleteUser() { }
}

// Bad - 여러 책임이 혼합됨
// 사용자 조회, 이메일 전송, 결제 처리 등 여러 역할을 포함하여 단일 책임을 위반합니다.
class Service {
  getUser() { }
  sendEmail() { }
  processPayment() { }
}
```

### 파일 내부 구조
- 모듈은 종속성이 높은 것부터 낮은 순서로 작성합니다. (상위 모듈부터 하위 모듈 순)
- 사용하지 않는 모듈은 즉시 제거하여 불필요한 임포트를 방지합니다.
- 핵심 노드 모튤 -> 외부 라이브러리 -> 설정/환경 파일 -> 데이터베이스/ORM 관련 -> 내부 모듈 순으로 작성합니다.
- 내부 모듈은 미들웨어 -> 서비스 -> 유틸리티 -> 상수 순으로 작성합니다.
- 각 그룹 사이에 빈 줄을 넣어 구분하는 것을 권장합니다.
- 각 그룹 내에서는 알파벳 순으로 정렬하는 것을 권장합니다.

#### CommonJS 예시
```js
// CommonJS 사용 시:
// 1. 핵심 노드 모듈
const path = require('path');
const fs = require('fs');
const http = require('http');

// 2. 외부 라이브러리
const express = require('express');
const lodash = require('lodash');
const axios = require('axios');

// 3. 설정/환경 파일
const config = require('../config');
const env = require('../env');

// 4. 데이터베이스/ORM 관련
const mongoose = require('mongoose');
const { sequelize } = require('../models');

// 5-1. 내부 미들웨어
const { auth } = require('../middleware/auth');
const { validate } = require('../middleware/validate');

// 5-2. 내부 서비스
const UserService = require('../services/user-service');
const AuthService = require('../services/auth-service');

// 5-3. 내부 유틸리티
const { logger } = require('../utils/logger');
const { formatDate } = require('../utils/date');

// 5-4. 내부 상수
const { ERROR_CODES } = require('../constants/errors');
const { API_ROUTES } = require('../constants/routes');
```

#### ES Modules 예시
```js
// ES Modules 사용 시:
// 1. 핵심 노드 모듈
import path from 'path';
import fs from 'fs';
import http from 'http';

// 2. 외부 라이브러리
import express from 'express';
import lodash from 'lodash';
import axios from 'axios';

// 3. 설정/환경 파일
import config from '../config';
import env from '../env';

// 4. 데이터베이스/ORM 관련
import mongoose from 'mongoose';
import { sequelize } from '../models';

// 5. 내부 미들웨어
import { auth } from '../middleware/auth';
import { validate } from '../middleware/validate';

// 6. 내부 서비스
import UserService from '../services/user-service';
import AuthService from '../services/auth-service';

// 7. 내부 유틸리티
import { logger } from '../utils/logger';
import { formatDate } from '../utils/date';

// 8. 내부 상수
import { ERROR_CODES } from '../constants/errors';
import { API_ROUTES } from '../constants/routes';
```



## 기본 원칙

### 변수 선언

#### 변수 선언자 사용
- `const` 사용을 기본으로 합니다.
- `let`은 재할당이 필요한 경우에만 사용합니다.
- `var` 사용 금지합니다.

```js
// best - const 사용
const superPower = new SuperPower();

// good - 재할당이 필요한 경우만
let counter = 0;
counter += 1;

// bad
var superPower = new SuperPower();
```

#### 선언과 할당
- 변수는 한 번에 하나씩만 선언합니다.
- 선언과 할당을 분리하지 않습니다.

```js
// good
const superPower = new SuperPower();
const name = 'Bruce Wayne';
const heroes = ['Batman', 'Superman'];

// bad - 한 줄에 여러 변수 선언
const items = getItems(),
      goSportsTeam = true,
      dragonball = 'z';

// Bad - 선언과 할당 분리
let superPower;
superPower = new SuperPower();
```

#### 객체와 배열 선언
- 객체와 배열을 선언할 때 `const` 를 사용합니다.
- 객체와 배열의 내부 요소를 변경할 수 있지만 재할당은 금지합니다.

```js
// Good
const person = {
  name: 'Bruce Wayne'
};
person.name = 'Batman';

const heroes = ['Batman'];
heroes.push('Superman');

// Bad - 객체/배열 재할당
let person = {
  name: 'Bruce Wayne'
};
person = {
  name: 'Batman'
};
```

#### 그룹화와 순서
- 모든 `const` 선언을 먼저 그룹화하고 그 다음`let`선언을 그룹화합니다.
```js
// good
const superPower = new SuperPower();
const name = 'Bruce Wayne';
let counter = 0;
let items;

// bad - const와 let 혼용
let counter = 0;
const superPower = new SuperPower();
let items;
const name = 'Bruce Wayne';
```

#### 호이스팅 방지
- `var`는 호이스팅으로 인해 선언 전에 접근할 수 있기 때문에 사용 금지입니다.
- `let`과 `const`로 선언한 변수는 선언하기 전까지 접근할 수 없습니다.
- TDZ(Temporal Dead Zone) 이슈를 피하기 위해 선언 전에 참조하지 않습니다.
- 변수는 사용하기 전 스코프의 시작부분에 선언합니다.

```js
// bad 
function getUserName() {
  console.log(userName);  // error! 아직 userName이 TDZ에 있음

  let userName = "Bruce";
  return userName;
}

//good 
function getUserName() {
  let userName = "Bruce";  // 먼저 선언

  console.log(userName);  // 정상 동작
  return userName;
}
```

### 글로벌 변수
- 전역 변수 사용을 피합니다.
- 필요한 경우 모듈 패턴이나 클래스를 사용합니다.
    
```js
// Bad - 전역 변수
let userName = "John";
const API_URL = "https://api.example.com";

function someFunction() {
  console.log(userName);  // 전역 변수 사용
}

// good - 모듈로 분리
// userConfig.js
export const userName = "John";
export const API_URL = "https://api.example.com";

// good - 필요한 스코프 내에서 선언
function someFunction() {
  const userName = "John";
  console.log(userName);
}

// good - 클래스/객체 사용
class UserService {
  userName = "John";

  someFunction() {
    console.log(this.userName);
  }
}
```

### 변수 스코프
- 변수는 사용되는 곳과 가장 가까운 스코프에서 선언합니다.
- 블록 스코프를 적극적으로 활용합니다.
```js
// bad - 불필요하게 넓은 스코프
function checkName(name) {
  const validName = name && name.length > 0;
  let returnValue;

  if (!validName) {
      returnValue = false;
  } else {
      returnValue = name;
  }

  return returnValue;
}

// good
function checkName(name) {
  const validName = name && name.length > 0;
  if (!validName) {
    return false;
  }

  return name;
}
```

### 구조 분해 할당
- 객체나 배열에서 필요한 값만 추출하여 사용합니다.
- 함수의 매개변수로 객체를 받을 때 구조 분해를 활용하면 필요한 프로퍼티만 명시적으로 받을 수 있습니다.
- 중첩된 객체의 경우에도 구조 분해를 활용할 수 있습니다.

```javascript
// ❌ bad
const name = user.name;
const age = user.age;
function processUser(user) {
  const id = user.id;
  const name = user.name;
}

// ✅ good - 필요한 값 추출하여 사용
const { name, age } = user;
const [first, ...rest] = items;

// ✅ good - 기본값 할당
const { name = 'Anonymous', age = 0 } = user;

// ✅ good - 함수의 매개변수로 객체를 받을 때
function processUser({ id, name }) {}

// ✅ good - 중첩된 객체의 구조 분해
const { address: { street, city } } = user;

```

### 전개 구문 (Spread Operator)
- 배열이나 객체를 복사하거나 병합할 때 전개 구문을 사용합니다.
- 배열에서 `concat()` 대신 배열 전개 구문을 사용합니다.
- 객체에서 `Object.assign()` 대신 객체 전개 구문을 사용하면 더 간결하고 읽기 쉽습니다.
- 전개 구문은 얕은 복사(shallow copy)를 수행합니다.

```javascript
// ❌ bad
const newArray = oldArray.concat([newItem]);
const newObject = Object.assign({}, oldObject, { newProp: value });

// ✅ good
const newArray = [...oldArray, newItem];
const newObject = { ...oldObject, newProp: value };

// ✅ good - 배열 복사 및 추가
const moreNumbers = [...numbers, 4, 5];

// ✅ good - 여러 객체 병합
const mergedObject = { ...obj1, ...obj2, ...obj3 };

```

### 옵셔널 체이닝과 Nullish 병합
- 중첩된 객체 속성에 안전하게 접근할 때는 옵셔널 체이닝(?.)을 사용합니다.
- 기본값 설정 시 Nullish 병합 연산자(??)을 권장합니다.
- 논리 연산자(&&, ||) 대신 옵셔널 체이닝과 Nullish 병합을 권장합니다.

```javascript
// ❌ bad
const name = user && user.profile && user.profile.name || 'Anonymous';
const count = data && data.count || 0;  // 0이 유효한 값일 때도 덮어씀

// ✅ good
const name = user?.profile?.name ?? 'Anonymous';
const count = data?.count ?? 0;
```

### 루프 최적화
- 배열 길이는 루프 밖에서 캐시하여 사용합니다.
- `for...of` 루프를 사용하여 성능을 향상시킵니다.
- `for...in` 안에서는 hasOwnProperty 조건 검사를 수행합니다.
```javascript
// ❌ bad
for (let i = 0; i < array.length; i++) {
  // 매 반복마다 length 접근
}

// ✅ good - length 캐싱
const length = array.length;
for (let i = 0; i < length; i++) {
  // 캐시된 length 사용
}

// ✅ good - for...of 사용
for (const item of items) { }
for (const [key, value] of Object.entries(obj)) { }
for (const prop in object) {
  if (object.hasOwnProperty(prop)) { }
}
```

### 메모리 관리
```javascript
// Good
function processLargeData() {
  const heavyObject = {};
  try {
    // ... 작업 수행
    return result;
  } finally {
    // 명시적 메모리 해제
    heavyObject = null;
  }
}

// Bad
const heavyObject = {};  // 전역 범위 사용
```

## 주석 작성 규칙

### 한줄 주석과 여러줄 주석
- 한줄 주석은 `//`를 사용하며, 코드의 위나 오른쪽에 작성합니다.
- 여러줄 주석은 `/* */` 를 사용하며, 첫번째와 마지막 줄을 비워두고 *로 정렬합니다.
- 주석은 설명하려는 구문에 맞춰 들여쓰기를 합니다.
- 문장 끝에 주석을 작성할 경우, 한줄 주석을 사용하며 공백을 추가합니다.
- 코드 블럭 주석처은 단축키로 한줄 주석(`//`)을 사용합니다.

```js
// ❌ bad - 한줄주석은 //로 사용하며 공백 추가
const name = 'Bruce Wayne';/* 한줄주석 */

// ❌ bad - 여러줄 주석 규칙 어김
/* 복잡한 정규식 설명:
 1. ^: 문자열의 시작
 2. [A-Z]: 대문자
*/

// ✅ good - 문장 끝 한줄 주석
const name = 'Bruce Wayne'; // 이름

// ✅ good - 여러줄 주석 (* 정렬 스타일)
/*
 * 복잡한 정규식 설명:
 * 1. ^: 문자열의 시작
 * 2. [A-Z]: 대문자
 * 3. [a-z]*: 소문자 0개 이상
 * 4. $: 문자열의 끝
 */
```

### 주석 작성 원칙
- 코드로 표현할 수 있는 것은 주석 대신 코드로 표현합니다.
- 필요한 경우 비즈니스 로직의 "왜"를 설명하는 주석 작성합니다.
- 임시 주석은 TODO, FIXME로 표시합니다.

```javascript
// ❌ bad - 자명한 내용에 대한 불필요한 주석
// 숫자를 증가시킴
count++;

// ✅ good - 복잡한 로직 설명
// 주말과 공휴일을 제외한 영업일 계산
const businessDays = calculateBusinessDays(startDate, endDate);

// ✅ good - TODO, FIXME 주석
// TODO: 성능 최적화 필요
// FIXME: 특정 케이스에서 버그 발생
```

### JSDoc 스타일 주석
- JSDoc 스타일로 함수와 클래스 문서화를 권장합니다.
- 복잡한 알고리즘이나 비즈니스 로직에 대한 설명을 작성합니다.
```javascript
// ✅ good - 함수 문서화
/**
 * 사용자 정보를 가져오는 함수
 * @param {string} userId - 사용자 ID
 * @returns {Promise<Object>} 사용자 정보 객체
 * @throws {Error} 사용자를 찾을 수 없는 경우
 */
async function getUser(userId) { }

// ✅ good - 클래스 문서화
/**
 * 사용자 인증을 처리하는 클래스
 * @class
 * @since 2.0.0
 * @implements {AuthInterface}
 */
class AuthService {
  /**
   * AuthService 인스턴스를 생성합니다.
   * @param {Object} config - 인증 설정
   * @param {string} config.apiKey - API 키
   * @param {string} [config.baseUrl] - 기본 URL (선택사항)
   */
  constructor(config) { }
}
```

## 에러 처리

### 에러 생성과 throw
```javascript
// Good
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
  }
}

throw new ValidationError('잘못된 입력값');

// Bad
throw 'Invalid input';  // 문자열 throw
```

### try-catch 사용
```javascript
// Good
async function saveData() {
  try {
    await api.save(data);
  } catch (error) {
    logger.error({
      message: error.message,
      stack: error.stack,
      context: 'saveData'
    });
    throw new CustomError('데이터 저장 실패', { cause: error });
  }
}

// Bad
async function saveData() {
  try {
    await api.save(data);
  } catch (e) {
    console.log(e);
    throw e;
  }
}
```

## 비동기 처리

### Promise 사용
```javascript
// Good
async function getData() {
  try {
    const [user, items] = await Promise.all([
      fetchUser(),
      fetchItems()
    ]);
    return { user, items };
  } catch (error) {
    handleError(error);
    throw error;
  }
}

// Bad
function getData() {
  return fetchUser()
    .then(user => {
      return fetchItems()
        .then(items => ({ user, items }));
    });
}
```


---
#### 버전 및 수정정보
현재버전: 0.0.5

수정이력:
- 2024.12.04(v.0.0.6): 기본 원칙, 주석 작성 규칙, 에러 처리, 비동기 처리 추가
- 2024.11.07(v.0.0.5): 명명 규칙 폴더명 추가
- 2024.11.07(v.0.0.4): 코드 구성 작성
- 2024.11.07(v.0.0.3): 명명 규칙 API 요청 함수 추가
- 2024.11.05(v.0.0.2): 명명 규칙 작성
- 2024.11.04(v.0.0.1): 초기 문서 작성
