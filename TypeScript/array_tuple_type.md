# array : tuple type

array 타입을 지정할 때 구체적인 타입을 지정하기 위해서는 tuple type!

```tsx
// tuple type
let 멍멍: [string,boolean] = ['dog', true];
```

이건 rest parameter에서도 가능한데, 

```tsx
function tupleFunc(...x :[number, string]) {
    console.log(x)
}
tupleFunc(1,'2')

let arr :number[] = [1,2,3];
let arr2 :[number, number, ...number[]] = [4,5, ...arr];
```

`?` 연산자는 옵션이라고 표현하는 의미

```tsx
let 멍멍: [string,boolean?] = ['dog', true];
```

단, 옵션 기호는 뒤에만 붙일 수 있음.

2개면 뒤에서 2개,

100개면 뒤에서 100개

```tsx
// 음식의 1. 이름 2. 가격 3. 맛있는지여부를 array 자료에 담아보고 타입지정
let food :[string, number, boolean] = ['donka', 11500, false];
console.log(food);

// 타입지정 
let tea :[string, number, ...boolean[]] = ['동서녹차', 4000, true, false, true, true, false, true]
console.log(tea);

// 함수에 타입지정
function babo(...a :[string, boolean, ...(number|string)[]]) {
    console.log(a)
}
babo('안녕', true, 1);

// 문자/숫자 분류기 함수
function sorter(...s :(string|number)[]) {
    let result : [number[], string[]] = [[],[]];

    s.forEach((a) => {
        if(typeof a === 'string'){
            result[1].push(a)
        } else {
            result[0].push(a)
        }
    })
    console.log(result);
    return result;
}
sorter('b', 5, 6, 8, 'a');
```