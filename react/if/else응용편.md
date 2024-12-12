# 리액트에서 자주 쓰는 if문 패턴

## 컴포넌트 안에 쓰는 if/else

```jsx
function Component() {
  if ( true ) {
    return <p>참이면 보여줄 HTML</p>;
  } else {
    return null;
  }
} 

// else 생략
function Component() {
  if ( true ) {
    return <p>참이면 보여줄 HTML</p>;
  } 
  return null;
} 
```

→ function으로 따로 빼서 작성해주기

## JSX안에서 쓰는 삼항연산자

```jsx
function Component() {
  return (
    <div>
      {
        1 === 1
        ? <p>참이면 보여줄 HTML</p>
        : null
      }
    </div>
  )
} 

function Component() {
  return (
    <div>
      {
        1 === 1
        ? <p>참이면 보여줄 HTML</p>
        : ( 2 === 2 
            ? <p>안녕</p> 
            : <p>반갑</p> 
          )
      }
    </div>
  )
}
```

→ 간단한 경우 사용 가능, 중첩으로도 가능

## && 연산자로 if 역할 대신하기

true&&true → true

true&&false&&true → false

**자바스크립트는 &&로 연결된 값들 중에 처음 등장하는 false 값을 찾아주고** 

**그게 아니면 마지막 값을 남겨준다.**

```jsx
function Component() {
  return (
    <div>
      { 1 === 1 && <p>참이면 보여줄 HTML</p> }
    </div>
  )
}
```

마지막 값인 <p></p>안에 있는 내용을 보여줌

## switch/case 조건문

```jsx
function Component2(){
  var user = 'seller';
  switch (user){
    case 'seller' :
      return <h4>판매자 로그인</h4>
    case 'customer' :
      return <h4>구매자 로그인</h4>
    default : 
      return <h4>그냥 로그인</h4>
  }

```

1. **switch (검사할변수){}**
2. 그 안에 **case 검사할변수 :** 를 넣어준다.
3. 그래서 이게 일치하면 case : 밑에 있는 코드를 실행
4. **default :** 는 그냥 맨 마지막에 쓰는 else문

## object/array 자료형일 때

예를들어,

**현재** **state가 info면 <p>상품정보</p>**

**현재** **state가 shipping이면 <p>배송정보</p>**

**현재 state가 refund면 <p>환불약관</p>**

이렇게 각각의 화면을 보여주고 싶을 떄, 

```jsx
function Component() {
  var 현재상태 = 'info';
  return (
    <div>
      {
        { 
           info : <p>상품정보</p>,
           shipping : <p>배송관련</p>,
           refund : <p>환불약관</p>
        }[현재상태]
      }

    </div>
  )
} 
```

html을 다 정리해서 담고, {} 뒤에 []붙여서 **현재 상태인 자료를 뽑는다** 라고 해주면 된다.

→ 변수 상태에 따라 다른 html을 보여줄 수 있음 

(정리하느라 머리 아프다 !)