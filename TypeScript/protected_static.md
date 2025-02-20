# protected & static

class는 extends 가능

```tsx
// class복사
class me {
    x = 10;
}

class Newme extends me {
}
let 나 = new Newme();
console.log(나)
```

### protected

private랑 비슷하지만 덜 빡빡한 느낌 

extends된 class안에서도 사용 가능

`private`로 `y`를 쓴다면 `NewYou` 클래스에서 `y`를 사용할 수 없지만,

`protected`이기 때문에 가능

```tsx
// protected
class You {
    protected y = 11;
}
class NewYou extends You {
    doThis() {
        this.y = 20;
    }
}
let 너 = new NewYou();
console.log(너);
```

class내에서 class끼리 공유하는 속성을 만들고 싶으면 `protected`

class내에서 하나만 사용할 수 있는 속성을 만들고 싶으면 `private`

### static

원래 `class{}` 안에 넣는 변수, 함수는 object에 있음.

하지만 class에 직접 함수, 변수를 넣고 싶으면 `static`

```tsx
class User {
  x = 10;
  y = 20;
}

let john = new User();
john.x //가능
User.x //불가능
```

User로 생성된 `john` 으로 가능인데,

```tsx
class User {
  static x = 10;
  y = 20;
}

let john = new User();
john.x //불가능
User.x //가능

// static
class We {
    static x = 10;
    y = 30;
}
```

이렇게 써주면 `User` 로 직접 사용 가능.

전문가입니다. 앞에 유동적으로 바꿔주기 위해서 static을 사용하기도 함.

`민수`는 `js 전문가입니다.`로  출력이 되고, 후에 바꿔준 `민수1`은 `ts 전문가입니다.`로 출력 됨.

```tsx
let 우리 = new We();
console.log(We.x)

class UnI {
    static skill = 'js';
    intro = UnI.skill +' 전문가입니다.'
}
let 민수 = new UnI();
console.log(민수);

UnI.skill = 'ts'
let 민수1 = new UnI();
console.log(민수1);
```

static은 private, protected, public키워드 동시 사용 가능

```tsx
class User {
  private static x = 10;

  // static을 이용하면 class 이름을 통해 직접 접근할 수 있어서 함수로 사용 가능
  static addOne(a :number){
    User.x += a;
    console.log(User.x)
  }

  static printX() {
    console.log(User.x)
  }
}
User.addOne(3) //이렇게 하면 x가 3 더해져야함
User.addOne(4) //이렇게 하면 x가 4 더해져야함
User.printX()
```

![image.png]