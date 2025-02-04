# Narrowing & Assertion

```tsx
function 내함수(x :number | string){
   return x + 1  
}
```

이렇게 하면 에러가 난다. `number | string` 같은 union type에는 조작을 못하기 때문이다.

이럴 때 **Narrowing**

### Type Narrowing

if문으로 타입을 하나로 정해주는 것

```tsx
function 내함수(x :number | string){
  if (typeof x === 'number') {
    return x + 1
  } 
  else if (typeof x === 'string') {
    return x + 1
  }
  else {
    return 0
  }
}
```

이렇게 하면 타입 에러가 안뜸. 타입이 확실하지 않을 때 생기는 오류를 막기 위함. 

→ “defensive하게 코딩한다.”라고 함.

if 문 뒤에 else문 꼭 써주기. 안그러면 에러남.

### Type Assertion

```tsx
function 내함수(x :number | string){ 
    return (x as number) + 1 
}
console.log( 내함수(123) )
```

assert는 변수의 타입을 number로 생각해 줘~ 라는 의미이다.

`변수명 as number` 

- `as` 사용 시 주의 사항

`as` 는 union type을 하나의 정확한 타입으로 줄이는 역할을 수행

---

```tsx
// 숫자와 문자가 섞인 array를 입력하면
// [1,2,3] 이렇게 숫자로 깔끔하게 변환되어 나오는 클리닝함수
function intoInt (arr : (number|string)[]) {
    let newArr :number[] = [];
    for (let i :number = 0; i < arr.length; i++){
        if(typeof arr[i] == "string"){
            newArr.push(Number(arr[i]));
        }else {
            newArr.push(Number(arr[i]));
        }
    }
    console.log(newArr);
}
intoInt(['1', 2, '3']);
```

별로 좋은 코드는 아닌 듯 한데, else문을 저렇게 안 써주면 에러남. 왜지?

```tsx
let 철수쌤 :{ subject :string } = { subject : 'math' }
let 영희쌤 :{ subject : string[] } = { subject : ['science', 'english'] }
let 민수쌤 :{ subject : string[] } = { subject : ['science', 'art', 'korean'] }

function teacher(a :{subject :string|string[]}) {
    if(Array.isArray(a.subject) == true){
        return a.subject[a.subject.length - 1];
    } else {
        return a.subject
    }
}
console.log(teacher(민수쌤));
```

지금 여러 변수에 선생님이 가르치고 있는 과목이 저장이 되어있습니다.

과목 1개만 가르치는 쌤들은 문자 하나로 과목이 저장이 되어있고

과목 2개 이상 가르치는 쌤들은 array 자료로 과목들이 저장되어있습니다.

'철수쌤' 같은 object 자료를 파라미터로 집어넣으면

그 선생님이 가르치고 있는 과목중 맨 뒤의 1개를 return 해주는 **함수**를 만들어봅시다.