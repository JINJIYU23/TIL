# declare & ambient module

### declare

JavaScript로 작성된 파일의 코드를 가져다 쓰고 싶으면 declare

```tsx
// data.js

var a = 10;
var b = {name :'kim'};
```

```tsx
// index.ts
declare let a:number;
console.log(a + 1);
```

```tsx
// index.html

<script src="data.js"></script>
<script src="index.js"></script> 
```

`.ts` 파일에 있는 것은 import, export을 해줘야 함.

```tsx
// data.ts

export var a = 10;
```

```tsx
// index.ts
import {a} from './data'
console.log(a + 1);
```

### Ambient Module

근데, TS에서는 import, export 하지 않아도 다른 파일에서 가져다 쓸 수 있음.

```tsx
// data.ts

type Age = number;
let 나이 :Age = 20;
```

```tsx
// index.ts

console.log(나이 + 1) //가능
let 철수 :Age = 30; //가능
```

ts파일에 입력한 변수와 타입들은 전부 global 취급을 받는다.

반면,

**import / export 키워드가 적어도 하나 있으면** 그 파일은 **로컬 모듈**이 되고 거기 있는 모든 변수는 export를 해줘야 다른 파일에서 사용 가능.

TS 파일이 다른 파일에 영향 끼치는걸 막고 싶으면 export 키워드를 강제로 추가해주기.

### Declare Global

ts 파일에 **import export 문법이 없으면** **글로벌 모듈**

ts 파일에 **import export 문법이 있으면 로컬 모듈**

로컬 모듈에서 전역 변수로 만들어 주면 global 키워드 붙이기

```tsx
// data.ts
export {}

declare global {
    type Dog = string;
}

```

```tsx
// index.ts
let b : Dog = 'angang';
```