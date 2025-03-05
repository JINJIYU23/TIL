# implement

```tsx
interface CarType {
  model : string,
  price : number
}

class Car implements CarType {
  model : string;
  price : number = 1000;
  constructor(a :string){
    this.model = a
  }
}
let 붕붕이 = new Car('morning');
```

class가 mode, price  속성을 가지고 있는지 확인하고 싶다면

interface 로 type 선언을 먼저 해주고, implement키워드를 써주면 됨.

→ class가 interface안에 있는 속성을 다 가지고 있는지 확인.

implement는 타입 지정이 아니기 때문에

```tsx
interface CarType {
  model : string,
  tax : (price :number) => number;
}

class Car implements CarType {
  model;   ///any 타입됨
  tax (a){   ///a 파라미터는 any 타입됨 
    return a * 0.1
  }
}
```

`Car`  안에 `CarType` 이 반영되는것이 아님.