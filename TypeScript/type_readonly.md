# 변수에 type 담기 & readonly

type이 너무 길어질 수 있음.

**→ 타입을 변수로 만들어서 키워드를 쓰는 것 type alias**

```tsx
type Animal = string | number | undefined;
let animal :Animal = 123;

type Human = {name : string, age : number};
let human :Human = {name : 'kim', age : 20}
```

### readonly

```tsx
type GirlFriend = {
    readonly name :string
}

const girlfriend : GirlFriend = {
    name : 'Amber'
}

girlfriend.name = 'Jessica' //에러
```

const 변수는 값이 변하지 않는 변수를 만들고 싶을 때 사용.

object 자료를 const에 집어넣어도 object 내부는 마음대로 변경가능.

이때 속성을 바뀌지 않게 하려면 **readonly**

**readonly는 특정 속성을 변경할 수 없게 잠궈준다.**

속성 몇 개가 선택 사항이라면, 물음표 연산자만 추가

```tsx
type Square = {
  color? : string,
  width : number,
}

let 네모2 :Square = { 
  width : 100 
}
```

 물음표는 **"undefined 라는 타입도 가질 수 있다."**라는 뜻임.

### type 키워드 여러 개 합치기 → type extend

```tsx
type Name = string;
type Age = number;
type NewOne = Name | Age; 

type PositionsX = { x :number};
type PositionsY = { y :number};
type NewType = PositionsX & PositionsY;
let position :NewType = {x : 10, y : 20}
```

타입 키워드는 재정의 불가.