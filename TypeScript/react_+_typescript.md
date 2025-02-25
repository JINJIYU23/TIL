# React에서 typescript 이용하기

### 일반 변수, 함수 타입 지정

(타입스크립트에서 똑같음)

```tsx
let a : string = 'kim'
```

### JSX 타입 지정

```tsx
let 박스 :JSX.Element = <div></div>
let 버튼 :JSX.Element = <button></button>
```

이런식으로 변수에 html코드를 담게 되면 이건 JSX문법이 됨.

이런 자료의 타입을 지정하고 싶으면 `JSX.Element` 타입 붙여 주기.

### component 만들 때 타입 지정

```tsx
function Profile () {
  return (
    <div>프로필</div>
  )
}
```

함수이기 때문에 **파라미터, return** 의 타입을 지정해줘야 함.

html을 return 한다면 JSX 타입 지정하는 것과 마찬가지로 아래처럼 해주기

```tsx
function Profile () : JSX.Element {
  return (
    <div>프로필</div>
  )
}
```

### component props 타입 지정

함수의 파라미터 같은 느낌.

```tsx
function App () {
  return (
    <div>프로필</div>
    <Profile name= "철수"></Profile>
  )
}

function Profile (props :{name : string}) : JSX.Element {
  return (
    <div>{props.name}프로필</div>
  )
}
```

props에는 `{name  : ‘철수’}` 이렇게 남게 된다.

`{props.name}` 출력하면 `철수`가 나옴.

`(props :{name : string})` 이렇게 지정해주면 됨.

너무 길다 싶으면 type alias 이용해주기.

props로 JSX를 입력할 수 있게 코드를 짠다면

`JSX.IntrinsicElements` 라는 이름의 타입을 사용.

`<div>` `<a>` `<h4>` 등 기본 태그를 표현해주는 타입이다.

```tsx
<Container a={<h4>안녕</h4>} />

function Container (props) {
  return (
    <div>{props.a}</div>
  )
}

type ContainerProps = {
  a: JSX.IntrinsicElements['h4'];
}; 

function Container (props: ContainerProps) {
  return (
    <div>{props.a}</div>
  )
}
```

### useState 타입 지정

```tsx
// 자동 지정
const [user, setUser] = useState('kim');

// generic
const [user, setUser] = useState<string | null>('kim');
```

state 만들 때는 자동으로 타입이 할당됨.