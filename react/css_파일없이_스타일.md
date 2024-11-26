# css 파일 없이 스타일 넣기

컴포넌트가 많으면 css 관리가 어려운데, 

이때 **styled-components** 라는 라이브러리를 설치하여 이용가능

터미널 열어서

**npm install styled-components**

```jsx
import styled from 'styled-components'

let Box = styled.div`
  padding : 20px;
  color : grey
`;
let YellowBtn = styled.button`
  background : yellow;
  color : black;
  padding : 10px;
`;

function Detail(){
  return (
    <div>
      <Box>
        <YellowBtn>버튼임</YellowBtn>
      </Box>
    </div>
  )
}
```

1. 변수 선언 해 준 뒤, ``(backtick) 기호를 이용해서 css스타일을 쓸 수 있음
2. 사용할 땐 그냥 컴포넌트 쓰는 것처럼 써주면 됨.

- 장점
1. css 오픈 할 필요없이 js파일에서 바로 스타일 넣을 수 있음
2. 페이지 로딩 시간 단축
3. css 파일을 사용하면 여러 js파일에 영향을 미치지만, styled-components는 **모듈화**가 있음.
    
    **컴포넌트명.module.css**
    
    이렇게 css 파일을 저장하고 컴포넌트명.js 파일에서 import해서 쓰면 그 파일은 컴포넌트명.js 파일에만 적용
    
4. props로 다르게 적용 가능

```jsx
let YellowBtn = styled.button`
  background : ${ props => props.bg };
  color : ${ props => props.bg == 'blue' ? 'white' : 'black' };
  padding : 10px;
`;

function Detail(){
  return (
    <div>
        <YellowBtn bg="orange">오렌지색 버튼임</YellowBtn>
        <YellowBtn bg="blue">파란색 버튼임</YellowBtn>
    </div>
  )
}
```

같은 컴포넌트를 공유하지만 다른 기능을 여러 컴포넌트 선언 없이 사용 가능

또, 스타일 프로그래밍도 가능(if문…)

- 단점
1. js파일이 복잡해짐 → 이게 일반 컴포넌트인지 스타일 컴포넌트인지 헷갈림
2. 협업 시 불편할 수도.