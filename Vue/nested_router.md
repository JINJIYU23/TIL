# nested routes

→ 특정 페이지 내에서 또 라우트를 나누는 경우

```jsx
const routes = [
  {
    path : '/detail/:id',
    component : Detail,
    children : [
      { path : 'author', component : Author },
      { path : 'comment', component : Comment },
    ]
  }
]
```

이런식으로 `children` 을 주면 

`/detail/:id/author`

`/detail/:id/comment`

이 경로로 접속했을 경우를 보여줌.

---

```jsx
<template>
  <div  v-for="(a, i) in blog" :key="i">
    <h4 @click="$router.push('/detail/' + i)" class="title">{{ a.title }}</h4>
    <p>{{ a.content }}</p>
    <p>{{ a.date }}</p>
  </div>
</template>
```

`$router.push('/detail/' + i)` 이거는 저 URL로 이동해 줌. (특별히 rounter-link 같은 것들 없이 페이지 이동 가능)

`$router.go(-1)` : 페이지 뒤로 가기(한칸), +로 바꿔주면 앞으로 이동 가능

 [https://next.router.vuejs.org/](https://next.router.vuejs.org/)    (참고)