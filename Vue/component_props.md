# Component 사용하기와 props

`<div>`가 정말 많이 사용되는데, 이때 조금이라도 덜 복잡해 보이기 위해  `component` 를 이용한다.

### 컴포넌트 만드는 법

1. `이름.vue` 파일을 하나 만들어서 아래처럼 작성

```jsx
<template>
  HTML
</template>

<script>
export default {
  name : '이름두글자이상',

}
</script>
<style>
  스타일 
</style>
```

1. 원하는 파일에 `import` 하고 `component` 등록

```jsx
// 이름이 Discount.vue일때
import DiscountBanner from './Discount.vue 경로'

export default {
  data() {

  },
  components : {
    DiscountBanner,
  }
}
```

1. 원하는 곳에 사용해주기

```jsx
<DiscountBanner/>
```

- 컴포넌트를 사용한다면 HTML 재사용이 용이함.

---

### props로 전송하는 법

- 부모 → 자식 이렇게 전송해주어야 사용 가능
- 보내고 등록하기

원룸들이라는 `App.vue`에 있는 데이터를 `Modal.vue`로 보내보자

```jsx
(App.vue)

<Modal :원룸들="원룸들" />
```

이렇게 하면 데이터를 `<Modal>`로 보낼 수 있음

(:콜론의 역할은 데이터 바인딩, props전송)

```jsx
 // (Modal.vue)

<script>
  export default {
    name : 'Modal',
    props : {
      원룸들 : Array,
    }
  }
</script>
```

자식 컴포넌트는 데이터를 받으면 props로 등록할 것

→ `props:{}`열고 작명한 이름 {데이터이름 : 자료형}으로 적어주기

(자료형에는 `Array, Object, String, Number` 같은 것..)

근데, 데이터를 전송할 무슨 데이터 형태던지 다 가능.

```jsx
<DiscountBanner :데이터이름="[1,2,3]" />
<DiscountBanner :데이터이름="{ age:20 }" />
<DiscountBanner :데이터이름="100" />
<DiscountBanner 데이터이름="안녕하쇼" />

// object자료로 보내는 법 
<DiscountBanner :데이터이름="오브젝트.name" :데이터이름="오브젝트.age"  />
// 혹은
<DiscountBanner v-bind="오브젝트명" />
```

### 반복문을 써서 상품 Card 만들어 보기

일단 `Card.vue`만들어주기

```jsx
<template>
    <div>
    <!-- <img :src="onerooms[i].image" class="room-img" @click="modalOpen = true; clicked = i"> -->
    <img :src="onerooms.image" class="room-img"
    @click="$emit('openModal', onerooms.id)" >
    <h4>{{ onerooms.title}}</h4>
    <p>{{ onerooms.price }} 원</p>
  </div>
</template>

<script>
export default {
    name : "ProductCard",
    props : {
            onerooms : Object,
        }
}
</script>

<style>

</style>
```

상품 6개가 있어서 반복문으로 만들려고 함.

만들어 주면, `App.vue`에서 `import`등록하고 사용 해야 함.

```jsx
import ProductCard from './components/Card.vue';

export default {
  components : { 
    ProductCard : ProductCard,
  }
}
```

---

근데, 나는 코드를 `$emit`를 이용해서 바꿨지만, 

자식 컴포넌트가 부모가 가진 데이터를 바꿔주려고 할 때는 변경해달라는 메세지만 보내면 됨 → **custom event**

### Custom event 문법을 이용하여 부모가 가진 데이터 변경방법 알아보기

1. 자식은 **`$emit(이름, 전달할자료)`** 이렇게 부모에게 메세지 보내기
2. 부모는  **`@이름="데이터변경하는JS코드"`** 이렇게 메세지를 수신

```jsx
(Card.vue)

<template>
  <div>
    <img :src="a.image" class="room-img">
    <h4 @click="$emit('openModal')"> {{a.title}} </h4>
    <p>{{a.price}} 원</p>
   </div>
</template>
```

→ openModal이라는 이름으로 커스텀 이벤트를 전송

```jsx
(App.vue)

<Card @openModal="modalOpen = true"  />
```

→ openModal이라는 이름의 커스텀 이벤트를 통해 데이터를 수정

### 커스텀 이벤트로 부모에게 자료를 보내기

자식은 **`$emit(이름, 전달할자료)`** 이렇게 보낼 수 있기 때문에, 각각 다른 모달 창이 열리게 하려면 **그 상품의 id를 찾아서 바꿔줘야지** **그 자료가 부모까지 전달**이 된다.

```jsx
(Card.vue)

<template>
  <div>
    <img :src="a.image" class="room-img">
    <h4 @click="$emit('openModal', 원룸.id)"> {{a.title}} </h4>
    <p>{{a.price}} 원</p>
   </div>
</template>
```

```jsx
(App.vue)

<Card @openModal="modalOpen = true; clicked = $event"  />
```

`$even`라는 변수를 쓰면 그 보낸 자료가 담겨 있음