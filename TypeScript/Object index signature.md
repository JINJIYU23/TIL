# Object index signature

object 자료에 타입을 미리 만들 때, 타입 지정할 속성이 반복되거나, 아직 모를 경우

```tsx
// object index signatures
interface StingOnly {
    [key : string] : string | number,
}

let UserOnly : StingOnly = {
    name : "jessica",
    age : '30',
    location : 'seoul'
}
console.log(UserOnly);
```

`[key : string] : string | number`  이렇게 작성하면 `{모든 속성 : string}` 의미와 같아짐.

```tsx
interface StringOnly {
  age : number,   // 불가능
  [key: string]: string,
}

interface StringOnly {
  age : string,   // 가능  
  [key: string]: string,
}

interface StringOnly {
  age : number,   // 가능
  [key: string]: string | number,
}

```

array형식일 경우도 가능

```tsx
interface ArrayOnly {
    [key : number] : string
}

let ArrOnly : ArrayOnly = {
    0 : '1',
    1 : '2',
    2 : '3'
}
console.log(ArrOnly[0]);
```

### Recursive Index Signature

```tsx
interface MyType {
  'font-size' : {
    'font-size' : {
      'font-size' : number
    }
  }
}

let obj = {
  'font-size' : {
    'font-size' : {
      'font-size' : 14
    }
  }
}
```

이런식으로 타입 지정해도 되지만, 이것은 비효율적이다.

```tsx
interface MyType {
  'font-size': MyType | number
}

let obj :MyType = {
  'font-size' : {
    'font-size' : {
      'font-size' : 14
    }
  }
}
```

`MyType` 을 만들면 `MyType` 을 안에서 사용할 수 있음.

**내 타입이 내부에 중첩되는 것에 계속 가능**인데, 

마지막 `font-size`에 `number type`이 지정되었으므로 마지막엔 `|number` 로 끝내줘야 함.

```tsx
// 자료의 타입을 지정
interface WorkType {
    [key : string] :string|number 
}

let WorkObj : WorkType = {
    model : 'k5',
    brand : 'kia',
    price : 6000,
    year : 2030,
    date : '6월',
    percent : '5%',
    dealer : '김차장',
}
console.log(WorkObj);

// object 자료의 타입을 interface 써서 만들어보기
interface CssType {
    'font-size' : number,
    [key : string] : CssType | number,
}
let Cssobj = {
    'font-size' : 10,
    'secondary' : {
      'font-size' : 12,
      'third' : {
        'font-size' : 14
      }
    }
}
```