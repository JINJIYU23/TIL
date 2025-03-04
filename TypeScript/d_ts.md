# d.ts

`이름.d.ts` 라는 파일은 타입을 저장하는 형식의 파일

1. 타입 정의만 해놓고 import해서 쓸 경우
2. 플젝에서 사용하는 타입을 정리해서 놓을 레퍼런스용으로 쓸 경우

일 때 사용한다.

### 타입 저장용 d.ts

```tsx
// test.d.ts
export type Age = number;
export type multiply = (x :number ,y :number) => number
export interface Person { name : string }
```

```tsx
// index.ts
import {Age} from './test.d'

// 변수나 타입이 너무 많을 경우는
import * as a from './test.d'
```

### 레퍼런스용 d.ts

```tsx
(tsconfig.json)

{
    "compilerOptions": {
        "target": "es5",
        "module": "es6",
        "declaration": true,
    }

```

`"declaration": true` 이걸 선언해 준다면 `ts`파일마다 `d.ts`파일이 옆에 생성됨.

```tsx
// index.ts

let 이름 :string = 'kim';
let 나이 = 20;
interface Person { name : string } 
let 사람 :Person = { name : 'park' }
```

```tsx
// index.d.ts

declare let 이름: string;
declare let 나이: number;
interface Person {
    name: string;
}
declare let 사람: Person;
```

자동으로 `d.ts` 파일에 생성됨.

`d.ts`파일은 글로벌 모듈이 아니기 때문에 다른 `ts`파일에서 import해야되는데, 이게 귀찮을 것 같다면 프로젝트에서 `types/common` 이런 폴더 두 개를 만들고 `tsconfig.json`파일에

 `“typeRoots”:[”./types”]` 옵션을 추가해주기.