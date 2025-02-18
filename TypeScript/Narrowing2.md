# Narrowing2

### **null & undefined 체크하는 법**

일단 `&&` 기호를 이용해서 체크할 수 있는데 

`&&` 기호로 비교할 때 true와 false를 넣는게 아니라 **자료형**을 넣으면

**`&&` 사이에서 처음 등장하는 false** 값을 찾아주고 그게 아니면 **마지막 값**을 남겨줌.

**null, undefined, NaN** 이런 값들을 의미.

```tsx
1 && null && 3   // null이 남음
undefined && '안녕' && 100  // undefined 남음
```

그래서 `&&` 을 이용해서 써주기.

```tsx
// null & undefined 체크하는 법
function printAll(strs: string | undefined) {
    if (strs && typeof strs === 'string') {  
        console.log('s');
    } 
}
printAll('안녕')
```

`‘안녕'` 이 string이기 때문에 s를 반환해준다.

### in 연산자로 object 자료 narrowing

```tsx
// in 연산자로 object 자료 narrowing
type Fish = { swim: string };
type Bird = { fly: string };

function 함수(animal: Fish | Bird) {
    if ('swim' in animal) {
        console.log(animal.swim);
        return animal.swim;
    }
        return animal.fly
} 
함수({fly : '헤엄'})

```

서로 다른 속성을 가지고 있을 때 사용 가능.

### class로 생산된 object라면 instanceof narrowing

```tsx
let 날짜 = new Date();
if (날짜 instanceof Date){
  console.log('참이에요')
}
```

class로 부터 new 키워드로 생산된 object들이 있을 때, instanceof 키워드를 붙여서 부모 클래스가 누군지 검사 가능.

### literal type 이 있으면 narrowing이 easy

```tsx
type Truck = {
    wheel : '4개',
    color : string
}

type Bike = {
    wheel : '2개',
    color : string
}

function 함수1(x : Truck | Bike){
    if(x.wheel === '4개'){
        console.log('x는 Truck타입이예요')
    }
}
함수1({wheel : '4개', color : 'red'})
```

literal type으로 object안에 다른 속성의 자료형이 있으면 구분하기가 편리해짐.