# primitive types

## 타입스크립트 기본 타입 정리

```tsx
// 내 이름, 나이, 출생지역을 변수로 저장
let myName :string = 'JEONG';
let age :number = 25;
let area :string = 'Seoul';

// 내가 좋아하는 곡, 가수 이름
let song :{title : string, singer : string} = {title : 'cruel summer', singer : 'taylor swift'}

let project :{member : string[], days : number, started : boolean } = {
    member : ['kim', 'park'],
    days : 30,
    started : true,
  }
```

자바스크립트의 타입 부분을 업그레이드해서 사용하고 싶을 때 쓰는 

**타입스크립트**

**Type Script는 타입 에러를 잡아 줌.**

### 타입 정하기 애매할 때

- Union type
    
    ```tsx
    let 이름: string | number = 'kim';
    let 나이: (string | number) = 100;
    ```
    

→ 이름에는 string 이나 number만 들어올 수 있음. (나이도 마찬가지)

```tsx
var 어레이: (number | string)[] = [1,'2',3]
var 오브젝트: {data : (number | string) } = { data : '123' }
```

- any

아무 자료형이나 집어 넣을 수 있는 타입.

```tsx
let 이름: any = 'kim';
이름 = 123;
이름 = undefined;
이름 = [];
```

타입을 바꾸어도 에러가 나지 않는다.

비상시에 쓰는 변수 타입 체크 해제 기능

- unknown

any와 마찬가지로 모든 타입을 집어 넣을 수 있음.

```tsx
let 이름: unknown = 'kim';
이름 = 123;
이름 = undefined;
이름 = [];

let 이름1: unknown;
let 변수1: string = 이름1;
let 변수2: boolean = 이름1;
```

아래처럼 했을 때 에러가 남.

타입스크립트는 정확한 언어라서 number가 아닐때는 빼기를 안해줌.

아직 뭘 집어 넣을지 모를 때 unknown을 사용할 수 있음.

unknown 타입인 변수를 조작하려면

내가 조작할 변수의 타입이 무엇인지 확실하게 체크하는 **narrowing 또는 assertion** 스킬을 사용.