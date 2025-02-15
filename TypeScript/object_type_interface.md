# object에 타입 지정 :interface

### object앞에 쓸 수 있는 `interface`

```tsx
interface Square { 
  color :string, 
  width :number, 
} 

let 네모 :Square = { color : 'red', width : 100 } 
```

1. 대문자로 작성
2. `{}` 안에 타입을 지정

### extends

일명, 겹치는 조건끼리는 `extends`로 확장시켜서 중복을 없애 줄 수 있음

```tsx
  // extends
interface Student { name : string};
// 중복 허용
interface Student { score :number};
interface Teacher extends Student {age : number};
let stu :Student = {name : 'kim', score : 100}
let tea :Teacher = {name : 'min',score : 100, age : 20}
```

`tea` 안에 속성 중 age 빼고 겹치기 때문에 `extends`를 이용하면 편리하게 확장 가능

`type` 으로 써줄 때는 `extends`말고 `&` 기호를 이용해서 합치기 가능

```tsx
// type alias extends
type Ani = {name : string}
type Cat = {age : number} & Ani

// interface도 &기호로 합치기 가능
interface Student {
  name :string,
}
interface Teacher {
  age :number
}

let 변수 :Student & Teacher = { name : 'kim', age : 90 }
```

그리고 `interface`를 사용하면 타입 이름을 중복 선언 가능하다.

(`type`은 불가능)

```tsx
interface Student { name : string};
// 중복 허용
interface Student { score :number};
```

- interface 이용해서 간단하게 타입을 만들기

```tsx
// interface 이용해서 간단하게 타입을 만들기
interface Product {
    brand : string,
    serialNumber : number,
    model : string[]
}
let 상품 : Product= { 
    brand : 'Samsung', 
    serialNumber : 1360, 
    model : ['TV', 'phone'] 
}
```

- array안에 있는 object

```tsx
// array 안에 object
interface Cart {
    product :string,
    price : number
}
let 장바구니1 : Cart[] = [ 
    { product : '청소기', price : 7000 }, 
    { product : '삼다수', price : 800 } 
]
```

- 위에꺼를 extends

```tsx
// 위에서 만든 타입을 extends
interface Cart {
    product :string,
    price : number
}
interface Card extends Cart{
    card : boolean
}
let 장바구니2 : Card[] = [ 
    { product : '청소기', price : 7000, card : false }
]
```

- object 안에 함수를 2개 넣기

```
// object 안에 함수를 2개 넣기
interface numType {
    plus : (a:number, b:number) => number
    minus : (a:number, b:number) => number
}

let numObj :numType = {
    plus(a,b) {
        return a + b
    },
    minus(a,b) {
        return a - b
    }
}
console.log('======================')
console.log(numObj.plus(7, 6));
console.log(numObj.minus(7, 6));
```