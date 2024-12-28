# import/export

외부 파일에 있는 변수나 자료를 가져와서 사용하고 싶은 경우 import/export 문법을 쓴다.

- `post.js`에 있는 변수를 `App.vue`에서 쓰고 싶을 때

```jsx
(post.js)
var apple = 10;
export default apple

(App.vue)
import 이름 from './post.js파일경로'
이름
```

- export 해야 될 게 많으면 `export{}`문법을 사용한다.

```jsx
(post.js)
var apple = 10;
var apple2 = 100;
export { apple, apple2 }

(App.vue)
import { apple, apple2 } from './post.js파일경로'
```

그래서 원래 하려고 했던 것은 6개의 데이터를 가져와서 보여주는 것이다.

```jsx
import postData from './assets/post.js';

  data(){
    return {
      onerooms : postData,
```

→ 이렇게 해주면 일단 데이터를 가져온 것임.

```jsx
  <!-- 상품 설명 반복문 -->
  <div v-for="(a, i) in onerooms" :key="i">
    <img :src="onerooms[i].image" class="room-img" @click="modalOpen = true">
    <h4>{{onerooms[i].title}}</h4>
    <p>{{ onerooms[i].price }}</p>
    <p>{{ onerooms[i].content }}</p>
    <button v-on:click="신고수[i]++">허위 매물 신고</button>
    <span>신고수 : {{ 신고수[i] }}</span>
  </div>
```

→ 반복문을 이용해서 바로 데이터 바인딩까지 완료.