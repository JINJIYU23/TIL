# slot 문법

자식이 부모데이터를 사용하고 싶을 때 좀 더 간단히 쓸 수 있는 문법 (props 대신)

1. 자식은 `<slot></slot>`  이라는 html태그를 사용해서 데이터가 쓰일 곳에 써놓기
2. 부모는 `<자식컴포넌트명>데이터</자식컴포넌트명>` 이렇게 작성

→ 등록이나 보내주는 것 없이 자동으로 사용가능

---

부모가 전해줄 데이터가 많은 경우

**named slot**

- 자식 컴포넌트

```jsx
<slot name="a"></slot>  
```

→ name 설정

- 부모

```jsx
<자식컴포넌트명>
  <template v-slot:a>데이터</template>
</자식컴포넌트명>
```

이렇게 하면 a라는 이름의 slot에만 해당 데이터를 보내줌

---

부모가 slot으로 데이터를 전해줄 때 자식의 데이터를 사용하고 싶을 때

1. 자식컴포넌트 

```jsx
<slot :데이터="데이터"></slot>
```

이렇게 하면 자식이 가진 데이터를 보내줄 수 있음

1. 부모

```jsx
<자식컴포넌트명>
  <template v-slot:default="이름"> {{이름.데이터}}</template>
</자식컴포넌트명>
```

---

```jsx
// 부모
<FilterBox :image = "image" v-for="filter in filters " :key="filter"
:filter = "filter">{{ filter }}</FilterBox>
```

```jsx
// 자식
<template>
  <div @click="onfilter" :class="[`${filter}`, 'filter-item']" :style="`background-image: url(${image})`">
    <slot></slot>
  </div> 
</template>
```