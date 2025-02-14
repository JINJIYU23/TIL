# class

class는 object를 여러개 만들기 위해 사용하거나, 함수의 기능을 하는데,

```tsx
class Person {
  name;
  age;
  constructor (){
    this.name = 'kim';
    this.age = 20;
  }
}
```

`name` 이나 `age` 가 필드 값이라고 부르는데, 이것을 `constructor` 전에 미리 선언해줘야 한다.

파라미터도 써줄 수 있다.

```tsx
class Person {
  name;
  age;
  constructor ( a: string ){
    this.name = a;
    this.age = 20;
  }
}
```

요런식.

### method타입 지정

class 내부에 함수를 만들어서 넣을 수 있음.

```tsx
// class
class Person2 {
    name: string ;
    constructor(a: string){
        this.name = a;
    }
    함수(a :string) {
        console.log('안녕' + a);
    }
}
let 사람1 = new Person2('kim');
let 사람2 = new Person2('park');
console.log(사람1)
사람1.함수('철수');
```

- car class 만들기

```tsx
// car class 만들기
class Car {
    model: string;
    price: number;
    constructor(a: string, b: number){
        this.model = a;
        this.price = b;
    }
    priceTax() {
        return this.price * 0.1;
    }

}

let car1 = new Car('소나타', 3000);
console.log(car1);
console.log(car1.priceTax())
```

- 파라미터가 무제한 들어가는 class만들기

```tsx
// 문자 숫자 구분 class
class Word{
    num: number[];
    str: string[];
    // ...rest는 Rest Parameter : 함수에 전달된 인자(argument)들을 배열로 받아 준다.
    constructor(...rest: (number|string)[]){
        let numArray: number[] = [];
        let strArray: string[] = [];

        rest.forEach((i) => {
            if(typeof i === 'number'){
                numArray.push(i);
            } else {
                strArray.push(i);
            }
        })
        this.num = numArray;
        this.str = strArray;
    }
}

let obj = new Word('kim', 3, 5, 'park', 6, 7, 'Jeong');
console.log(obj.num) 
console.log(obj.str) 

```