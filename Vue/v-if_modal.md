# v-if와 modal

자꾸 하는 건데, 할 때마다 어렵고 까먹는 동적인  UI만들기는

1. 현재 html UI의 상태를 저장해두기 (Vue에서는 data로 저장하더라)
2. 상태에 따른 구현

모달 창 만들기는 이제 껌인듯?(개인적으로는,,,,)

1. 모달창 html + css 로 만들기
2. 모달의 상태를 `data()`에 저장하기

```jsx
<div class="black-bg">
  <div class="white-bg">
    <h4>상세페이지</h4>
    <p>상세페이지내용임</p>
  </div>
</div>
```

```jsx
body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
} 
```

그 담에, `modalOpen`이라는 변수로 모달의 상태를 정의함

```jsx
modalOpen : false,
```

`modalOpen == true` 이면 모달 창 오픈,

나는 상품의 사진을 클릭했을 때 `modalOpen`을 `true`로 설정해뒀기 때문에, 이미지를 클릭함과 동시에 상황이 바뀐다.

```jsx
<img :src="require('./assets/room' + i +'.jpg')" class="room-img" @click="modalOpen = true">
```

그 담엔 

```jsx
 <!-- 모달창 -->
  <div class="black-bg" v-if="modalOpen == true">
    <div class="white-bg">
      <h4>상세 페이지</h4>
      <p>상세 페이지 내용</p>
      <button @click="modalOpen = false">닫기</button>
  </div>
```

닫기 버튼을 만들어서 버튼을 누르면 닫힐 수 있는 기능도 만듬.

% 참고 %

```jsx
  <div v-if="1 == 2">
    안녕하세요
  </div>  
  <div v-else-if>
    안녕하세요23
  </div>
  <div v-else>
    안녕하세요23
  </div>

```

---

💡 `data(){}` 이 부분을 리액트에서는 `state`라고 부른다.