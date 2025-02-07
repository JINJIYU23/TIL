# literal type & const

자료를 값으로 지정하고 싶을 때 literal type 사용하기

```tsx
let john :'jone';
let kim :'single';

let 방향: 'left' | 'right';
방향 = 'left';

function 함수(a : 'hello') : 1 | 0 | -1 {
  return 1 
}
```

→ 특정 글자나 숫자만 가질 수 있게 제한을 줌.

- ‘가위’, ‘바위’, ‘보’ 문자만 파라미터로 입력, ‘가위’, ‘바위’, ‘보’ 문자만 담을 수 있는 array만 return

```tsx
// literal types
function game(a :'가위'|'바위'|'보') :('가위'|'바위'|'보')[]{
    return ['가위'];
}
game ('가위');
```

`const` 변수의 확장판 느낌, 

`const` 변수는 **값을 바꿀 수 없는** 변수.

```tsx
const 이름 = 'kim' | 'park' (이런 식의 문법은 자바스크립트에 없음)
```

### as const

```tsx
var 자료 = {
  name : 'kim'
}

function 내함수(a : 'kim') {

}
내함수(자료.name)
```

이렇게 하면 오류가 남. `자료` 의 `name` 타입은 `string` 이기 때문.

- 해결 방안
1. object의 타입을 잘 정하기.
2. assertion (`as ‘kim’` )활용하기.
3. `as const` 를 object에 붙여주기.

```tsx
var 자료 = {
  name : 'kim'
} as const;

function 내함수(a : 'kim') {

}
내함수(자료.name)
```

- `as const` 의 효과
1. 타입을 object의 value로 바꿔 준다.
2. object안에 있는 모든 속성을 readonly로 바꿔 준다.