# 함수에 타입 지정하는 법 & void 타입

```tsx
function myFunc(x){
  return x * 2
}
myFunc(2);  //이러면 4가 이 자리에 남음
myFunc(4);
```

소괄호 안에 들어가는 x같은 자료 : 파라미터

return 오른쪽에 있는 자료 : 리턴값 

1. 파라미터를 작명해주면 함수를 사용할 때 ( ) 소괄호 안에 아무 자료 넣을 수 있음
2. 리턴값은 함수가 사용되고 나서 그 자리에 남는 값

`myFunc(2)` 이렇게 쓰고 나면 return 우측에 있던 값이 나옴.

함수는 총 두 군데 타입지정이 가능

1. **파라미터**
2. **return**

### Void 타입

return 할 자료가 없는 함수의 타입으로 사용가능

```tsx
function myFunc(x :number) :void { 
  return x * 2 //여기서 에러남 
} 
```

함수 return에서 에러가 난다면, return을 안해주고 싶을 때 void 타입을 활용하기.

### 파라미터가 옵션일 때

```tsx
function myFunc(x? :number) { 

}
myFunc(); //가능
myFunc(2); //가능
```

파라미터를 만들어 놨지만, 없이 쓸 경우 가능

**`x : number | undefined`** 이것과 똑같은 의미임. (정의가 안되면 자동으로 undefined)

### 함수가 Union type을 사용할 때

```tsx
function num(x :number | string){ 
  return x + 1 
} 

function myFunc(x? :number) :number { 
  return x * 2 
}
```

타입스크립트에서는 `number | string` 이런 union type인 경우 자료 조작을 금지

아래 경우는 파라미터가 옵션이면  `number | undefined` 이런 식으로 정의 되기 때문에 x가 확실 하지 않아서 에러를 낸다.