# 삼항 연산자 & infer

삼항 연산자를 사용하면 조건을 넣어줄 수 있음.

```
// 삼항연산자
3 > 1 ? console.log('맞음') : console.log('아님');
```

3이 1보다 크면 `‘맞음’`을 반환, 아니면 `‘아님’`을 반환.

타입을 만들어서 쓰고 싶으면, `extends`를 이용해주면 됨.

```tsx
type Prison1<T> = T extends string ? T : unknown;
```

타입 파라미터에 `string`을 넣는다면 `string`을 반환해주고, 아니면 `unknown`

```tsx
type Age<T> = T extends string ? string : unknown;
let al : Age<number>; // unknown
```

**타입 조건식은 `extends`키워드와 삼항 연산자를 이용.** (왼쪽이 오른쪽의 성질을 가지고 있냐? 이런 의미)

- 파라미터로 array 자료를 입력하면 array의 첫 자료의 타입을 그대로 주고
    
    array자료가 아닌 것을 입력하면 ant타입을 남겨주는 타입?
    

```tsx
type FirstItme<T> = T extends any[] ? T[0] : any;
let Item1 : FirstItme<[1,2,3]>
let Item2 : FirstItme<1>
```

### infer

infer키워드는 지금 입력한 타입을 변수로 만들어주는 키워드

```tsx
// infer
type Prison2<T> = T extends infer R ? R : unknown
type P = Prison2<string>
```

1. infer는 조건문 안에서만 사용 가능
2. infer R은 타입을 T에서 유추해서 R에 집어 넣으라는 뜻
3. R을 조건식 안에서 사용가능

→ **타입 파라미터에서 타입을 추출해서 쓰고 싶을 때** 쓰는 키워드

```tsx
//            T 는 string[], infer R은 string, R은 string
type 타입추출<T> = T extends (infer R)[] ? R : unknown
// pp는 string
type pp = 타입추출<string[]>

// 함수의 return 타입이 어떤 타입인지
//            T 는 () => void, infer R은 void, R은 void
type 타입추출1<T> = T extends (() => infer R) ? R : unknown
// pp는 void
type pp1 = 타입추출1<() => void>

// 함수의 타입을 return해주는 문법
type b = ReturnType<() => void>
```

```tsx
type Age2<T> = T extends [string, ...any] ? T[0] : unknown
let age1 :Age2<[string, number]>;  // string
let age2 :Age2<[boolean, number]>; // unknown

// 함수 타입을 입력하면 함수 파라미터 부분의 타입을 뽑아주는 기계

type 타입뽑기<T> = T extends ((x : infer R) => any) ? R : unknown
let a1 :타입뽑기<(x :number) => void> //number
let b1 :타입뽑기<(x :string) => void> //string
```