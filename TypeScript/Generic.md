# Generic : 타입을 파라미터로 입력하기

함수만들 때 파라미터로 타입을 입력 가능 `<>` (이 기호로)

```tsx
// Generic
function 함<T>(x :T[]) :T{
    return x[0];
}

let a = 함<number>([4,2]);
let b = 함<string>(['4','2'])
console.log(a);
```

`함<number>` () 

`T` 에 number가 들어감

**`함수(x :number[]):number {`** 

**`}` 이 의미임.**

```tsx
function 함수<MyType>(x: MyType[]) :MyType {
  return x[0];
}

let a = 함수([4,2])
let b = 함수(['kim', 'park'])
```

이렇게 써도 타입을 잘 유추해서 내줌

generic타입 제한

기존 extends와는 다른 if문으로 narrowing하는 문법 (number와 비슷한 속성을 가지고 있는지)

```tsx
interface LengthCheck {
    length :number
}
function 수<T extends LengthCheck>(x : T){
    return x.length;
}
let c = 수('100')
console.log(c);
```

```tsx
// 문자를 집어넣으면 문자의 갯수, array를 집어넣으면 array안의 자료 갯수
interface 길이체크 {
    length : number
}
function Leng<T extends 길이체크|string>(a :T){
    return a.length
}
let d = Leng<string>('How many?');
let e = Leng<number[]>([1,2,3,4,5]);

// Animal 이라는 타입 반환 해주기
interface Animal {
    name : string;
    age : number 
}

let data = '{"name" : "dog", "age" : 1 }'

function 동물<T extends Animal>() :T{
    return JSON.parse(data)
}
let ani = 동물<Animal>()
console.log(ani)

//class 를 수정
class Person <T> {
    name : T;
    constructor(t :T){
      this.name = t;
    }
}
let t = new Person<string>('어쩌구');
console.log(t.name);  

```