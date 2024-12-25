# click 이벤트

### `@click`

버튼을 누르면 허위 매물 신고의 신고수가 1씩 증가하는 이벤트를 만들어보자.

```jsx
<div>
  <h4>{{products[0]}}</h4>
  <p>50만원</p>
  <button>허위매물신고</button>
  <span>신고수 : {신고수}</span>
</div>

//밑 
data(){
  return {
    신고수 : 0,
  }
}
```

자바스크립트는 onclick이지만, Vue에서는 `@click` 혹은 `v-on:click` 으로 가능.

```jsx
<div>
  <h4>{{products[0]}}</h4>
  <p>50만원</p>
  <button @click="신고수++">허위매물신고</button>
  <span>신고수 : {신고수}</span>
</div>
```

---

### 함수

코드가 길 때는 함수를 만들어서 쓰자.

```jsx
data(){
  return {
    신고수 : 0,
  },
}

methods : { 
  increase(){ 
    this.신고수 += 1 
  } 
}
```

→ `methods`가 함수. 이때 주의할 점은 신고수는 위에서 가져와서 쓰는 것이기 때문에, 

꼭 **this.**을 붙여줘야 함. 

함수를 가져다가 쓸 때는 

```jsx
<div>
  <h4>{{products[0]}}</h4>
  <p>50만원</p>
  <button @click="increase">허위매물신고</button>
  <span>신고수 : {신고수}</span>
</div>
```