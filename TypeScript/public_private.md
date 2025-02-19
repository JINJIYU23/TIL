# public & private

### public, private 키워드로 제한

```tsx
// public
class User1 {
    public name = 'Han'
    constructor(a :string) {
        this.name = a
        console.log(this.name) // kim
    }
    
}
let 유저1 = new User1('Kim');
유저1.name = '안뇽';
console.log(유저1.name) // 안뇽
```

public이 붙은 속성은 자식 object들이 마음대로 사용하고 수정 가능.

```tsx
// private
class User2 {
    name:string ;
    private familyName:string = 'Han'
    constructor(a :string) {
        this.name = this.familyName + a;
    }
}
let 유저2 = new User2('소희');
console.log(유저2)
```

private가 붙은 속성은 수정 불가. 오직 `class{}`안에서만 수정이 가능.

단, private가 붙은 속성을 class밖에서 수정하고 싶을 때는 

class안에 constructor함수를 만들어서 실행 시키면 됨.

```tsx
// private
class User2 {
    name:string ;
    private familyName:string = 'Han'
    constructor(a :string) {
        this.name = this.familyName + a;
    }
    이름변경함수() {
        this.familyName = 'Park';
    }
    
}
let 유저2 = new User2('소희');
유저2.이름변경함수()
console.log(유저2)
```