# 함수 rest 파라미터, destructuring 할 때 타입 지정

### rest parameter

함수에 파라미터가 몇 개 들어올 지 모를 때, 미리 정의가 불가할 때 써주는 rest parameter

```tsx
function 전부더하기(...a){
  console.log(a)
}

전부더하기(1,2,3,4,5)
```

rest parameter는 `[]`안에 들어 있음.

### rest parameter 타입 지정

```tsx
function 전부더하기(...a :number[]){
  console.log(a)
}

전부더하기(1,2,3,4,5)
```

`[]`에 담겨 오므로 array 타입 지정처럼 해주기.

### spread parameter

```tsx
let arr = [3,4,5];
let arr2 = [1,2, ...arr]
console.log(arr2)
```

이 경우에는 둘을 합쳐 주는 역할을 한다고 쉽게 생각해주면 되고, rest parameter 랑 헷갈리지 말기.

### Destructuring

```tsx
let 사람 = { student : true, age : 20 }
let student = 사람.student;
let age = 사람.age
```

위에는 array, object에서 데이터를 뺄 때 변수를 만들어서 빼줘야 하는 걸 훨씬 간단하게 할 수 있는 방법으로 **`Destructuring`**

```tsx
let [변수1, 변수2] = ['안녕', 123]
let { student, age1} = {student : true, age1 : 20}
```

이렇게 하는데, array에는 변수 이름을 신경 쓰지 않아도 되지만, 

**object에는 변수 이름을 속성 이름과 맞춰서 선언하도록 하자.** 

destructuring문법은 함수에서 사용 가능. (근데 개인적으로 간편한지는 잘 모르겠음)

- destructuring을 사용하지 않을 때

```tsx
let person = { student : true, age : 20 }

function 함수(a, b){
  console.log(a, b)
}
함수(person.student, person.age)
```

- destructuring을 사용할 때

```tsx
let 오브젝트1 = {student : true, age1 : 20}

function dFunc({student, age1} : {student : boolean, age1 : number}) {
    console.log(student, age1)
}
dFunc(오브젝트1)
```

```tsx
let 오브젝트1: {student : boolean, age1 : number} = {student : true, age1 : 20}

function dFunc({student, age1} ) {
    console.log(student, age1)
}
dFunc(오브젝트1)
```

타입을 먼저 지정해도 됨.

```tsx
// 최댓값 찾기기
function findMaxNum (...num:number[]) {
    let maxNum : number = num[0];

    for(let i = 0; i < num.length; i++){
        if(num[i] > maxNum){
            maxNum = num[i];
        }
    }
    return maxNum;
}
console.log(findMaxNum(1,3,455,6,7,66))

// object destructuring
function dFunc2({user, comment, admin}
    : {user : string, comment : number[], admin : boolean}){
    console.log(user, comment, admin)
}
dFunc2( { user : 'kim', comment : [3,5,4], admin : false } )

// array destructuring
function dFunc3([x,y,z]:(number|string|boolean)[]){
    console.log(x,y,z)
}
dFunc3( [40, 'wine', false] )
```