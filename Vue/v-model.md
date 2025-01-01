# v-model

`<input @input = "month = $event.target.value">`

이렇게 코드를 짜게 된다면,

1. `@input`이거는 `@clicked`랑 똑같음. (이벤트 핸들러)
2. `$event`는 event object → 자바스크립트의 `e`랑 똑같은 기능

`$event.target.value` 는 `<input>`에 입력한 값을 가져오란 뜻.

```jsx
<template>
  (생략)
  <input @input="month = $event.target.value">
</template>
<script>
export default {
  data(){
    return {
      month : 0
    }
  }
}
</script>
```

---

이렇게 말고도 

```jsx
<input @input="month = $event.target.value">
<input v-model="month"> 
```

두 개는 같은 의미 → month에 있는 값을 바로 저장