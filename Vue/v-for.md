# v-for 반복문

1. 원하는 태그에 `v-for=”이름 in 반복할 횟수”`
2. 뒤에 `:key=”이름”` 꼭 붙여주기

```jsx
<div class="menu">
  <a v-for="이름 in 3" :key="이름">Home</a>
</div>
```

→ 이러면 Home이 3번 반복됨.

array/object자료형을 반복하려면

`<script>`태그 안에 `data()`에 일단 자료를 넣고

```jsx
data(){
    return {
      메뉴들 : ['Home', 'Products', 'About'],
       }
}
```

html안에 반복할 태그에 반복문 써주면 됨.

```jsx
  <div class="menu">
    <a v-for="(a, i) in 메뉴들" :key="i">{{ a }}</a>
  </div>

```

이렇게 반복문 안에 변수를 2개 써 넣을 수 있는데,

2개를 넣었을 경우에는 **a 는 반복할 값이고 i는 1씩 증가하는 정수**가 됨.

그러면  a에는 메뉴들에 있는 값('Home', 'Products', 'About')이 됨.