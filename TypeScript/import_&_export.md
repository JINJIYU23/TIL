# import & export

`b.ts` (export)→ `a.ts` (import)

1. 변수를 다른 파일에서 쓰이게 내보내고 싶으면 export
2. export된 변수를 가져와서 쓰고 싶으면 import

```tsx
// b.ts
export var 이름 = 'kim';
export type Name = string;
```

```tsx
// a.ts
import {이름} from './b';
console.log(이름);

let 변수 :Name = 'park';
```

```tsx
// b.ts
export type Car = {
    wheel : number,
    model : string
}
export interface Bike {
    wheel : 2,
    model : string
}

// a.ts
import { Car} from './b';
import { Bike } from './b';
let 빠방 :Car = {wheel : 4, model : 'audie'}
let 따릉 :Bike = {wheel : 2, model : '삼천리'}
console.log(빠방, 따릉);
```

```
// b.ts
export function mani(a? :object) {
    return ;
}

// a.ts
import { mani } from './b';
let 많이 :typeof mani = mani
console.log(많이);
```