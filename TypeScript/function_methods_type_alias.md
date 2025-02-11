# 함수와 methods에 type alias 지정

### 함수안에 type alias

```tsx
type NumOut = (x : number, y : number ) => number ;
```

arrow function에 타입을 지정할 때에는 아래처럼 해야 함.

```tsx
type NumOut = (x : number, y : number ) => number 
let ABC :NumOut = function(x,y){
  return x + y
}
```

### methods 안에 type alias

```tsx
let 회원정보 = {
  name : 'kim',
  age : 30,
  plusOne (x){
    return x + 1
  },
  changeName : () => {
    console.log('안녕')
  }
}
회원정보.plusOne(1);
회원정보.changeName();
```

arrow function, 일반 함수 모두 object안에 넣을 수 있음

`plusOne()`과 `changeName()`의 차이는  각각

**개체의 메서드로 사용할 때, (객체 안에서 `this`를 사용해 해당 객체의 값을 변경하거나 사용할 때)**

**내부에서 `this`를 변경하고 싶지 않을 때 (콜백, setTimeout)일 때 사용.**

- `cutZero()`라는 함수는 문자를 하나 입력하면 맨 앞에 '0' 문자가 있으면 제거하고 문자 type으로 return
- `removeDash()`라는 함수는 문자를 하나 입력하면 '-' 가 있으면 전부 제거해주고 그걸 숫자 type으로 return

```tsx
type cutZeroType =(a :string) => string;
type removeDashType = (b:string) => number;

let cutZero :cutZeroType = function (a) {
    return a.replace(/0/g,'');
}
console.log(cutZero('0000안녕'))

let removeDash :removeDashType = function (b) {
    let result =  b.replace(/-/g,'');
    return parseFloat(result);
}
console.log(removeDash('12300----'))
```

이 함수는 파라미터 3개가 들어가는데 첫째는 문자, 둘째는 함수, 셋째는 함수를 집어넣을 수 있다.

1. 첫째 파라미터를 둘째 파라미터 (함수)에 파라미터로
2. 둘째 파라미터 (함수)에서 return된 결과를 셋째 파라미터(함수)에 넣어주기
3. 셋째 파라미터 (함수)에서 return된 결과를 콘솔창에 출력

```tsx
type cutZeroType =(a :string) => string;
type removeDashType = (b:string) => number;

let cutZero :cutZeroType = function (a) {
    return a.replace(/0/g,'');
}

let removeDash :removeDashType = function (b) {
    let result =  b.replace(/-/g,'');
    return parseFloat(result);
}

function final(a :string, func1 : cutZeroType, func2 : removeDashType){
    let result1 = func1(a);
    let result2 = func2(result1);
    console.log(result2);
}

final('010-1111-2222', cutZero, removeDash)
```