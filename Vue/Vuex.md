# Vuex

- props와 custom event로 데이터를 주고 받는게 힘들 때

→ Vuex를 설치하면 js파일에 모든 데이터를 저장할 수 있음.

→ props같은 것 없이 모든 컴포넌트가 데이터에 직접 접근 가능.

- `.vue`파일과 데이터가  너무 많을 때

---

설치 :  [https://next.vuex.vuejs.org/](https://next.vuex.vuejs.org/)

`store.js`파일 만들고 코드 작성

```jsx
import { createStore } from 'vuex'

const store = createStore({
  state(){
    return {
      
    }
  },
})

export default store
```

`store.js`파일을 `main.js`에 등록

```jsx
import store from './store.js'
app.use(store).mount('#app')
```

이제 모든 컴포넌트가 데이터를 편하게 쓸 수 있다.

출력은 `{{ $store.state.데이터명 }}` 

함수나 mounted같은 곳에서 `this.$store.state.`