# router

너무 너무 너무 헷갈리는 부분이다.

일단은 여러 페이지로 이동하기 위해서 router를 깔아야 한다.

```bash
npm install vue-router@4
```

다음 `router.js` 파일을 assets에 생성해준 후,

```jsx
import { createWebHistory, createRouter } from "vue-router";

const routes = [
  {
    path: "/~~",
    component: import 한 컴포넌트이름,
  }
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router; 
```

일단 `/list`로 이동하기 위해 `List.vue`를 import하고 컴포넌트도 받아왔다.

```jsx
import BlogList from '../components/List.vue';
    
     path: "/list",
     component: BlogList,
```

다음으로 `App.vue`에 가서 router을 실행해줘야 한다.

```jsx
<router-view :blog = "blog"></router-view>
```

`:blog = "blog"`  이 부분은 데이터를 전송해주는 것이다. (props)

근데, 처음에 오류가 계속 났다.. 그래서 어쩌지 어쩌지 하면서 구글과 chat gpt에 도움을 요청했다. 엄청난 검색 후, `<router-view>` 에는 반복문을 쓸 수 없다는 것을 알아냈다.

그 후 List.vue로 가서 거기서 반복문을 써줬다…. ㅎㄷㄷ 

---

`<router-link to="">` 는 HTML의 `<a>` 와 같은 기능이었는데, 조금 헷갈려서 일단 보류 해놨다. 

사실 헷갈리는게 하나 더 있는데 이게 `<router-view>` 를 여러개 써주면 뭐가 뭔지 어떻게 안다는건지…. 헷갈린다.

→ 아 하나만 그냥 써도 되는구나!

---

### 근데 , 상세페이지를 계속 만들기 위해서

파라미터 문법을 하나 알아보자.

```jsx
(router.js)
const routes = [
  {
    path: '/detail/:id',
    component: Detail,
  },
];
```

뒤에 `:이름` 이런식으로 작성해주면 무제한 홈페이지를 만들 수 있다.

근데 이제 컴포넌트 안에서 URL파라미터에 뭐가 써있는지 출력하고 싶으면

`{{ $route.params.id }}`   (위에서 :id라고 했기 때문에 id를 써줌)