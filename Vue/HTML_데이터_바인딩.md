# HTML에 데이터 바인딩

Vue를 처음 봤는데 일단 `<template>`라는게 보여서 굉장히 당황스러웠지만 당황하지 말고 html코드는 `<template>`안에 하던대로 쓰면 된다.

vuedongsan (부동산) 페이지는 원룸을 소개하는 페이지.

```jsx
<template>
  <div>
    <h4>XX 원룸</h4>
    <p>XX 만원</p>
  </div>
  <div>
    <h4>XX 원룸</h4>
    <p>XX 만원</p>
  </div>
</template>
```

---

- Vue의 데이터 바인딩 문법

```jsx
<script>

export default {
  name: 'App',
  data(){
    return {
		  price1 : 60,
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      // 스타일 : 'color : red',
    }
  },
  components: {

  }
}
</script>
```

`data(){return {}}`을 넣고 데이터를 object 형식으로 저장하면 됨! (매우간단)

```jsx
<p>{{ price1 }} 만원</p>
```

이걸  html에 넣고 싶다면, `{{ price1 }}`이라고 적어주기만 하면 데이터 바인딩 끝!

참고로 html 속성도 데이터 바인딩이 가능 (style, class…)

### 데이터 바인딩을 해주는 이유

- 변동되는 데이터를 관리
- 실시간 렌더링 기능을 쓰기 위해
    
    **Vue는 data가 변경되면 데이터와 관련된 html이 실시간으로 변동됨 → web-app**