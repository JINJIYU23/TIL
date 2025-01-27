# Vuex-mutations

`Vuex`에 있는 `state`를 변경하려면 `store.js`파일에서만 할 수 있게 코드를 짜 놓자.

`mutations`라는 `object`항목을 만들고 거기에 `state` 수정 방법을 함수로 정의하기.

```jsx
const store = createStore({
  state () {
    return {
      name : 'kim',
      age : 20,
    }
  },
  mutations :{
    한살더하기(state){
      state.age++
    }
  },
}
```

이런 식.

mutations안에 미리 어떻게 수정할 지 정의해 놓고 html에서 호출해서 쓰는 식으로

```jsx
(App.vue)

<button @click="$store.commit('한살더하기')">버튼</button>
```

---

### 인스타그램에 사진 한번 누르면 좋아요 + 1, 다시 누르면 좋아요 취소 기능

1. 좋아요를 눌렀는지 안 눌렀는지 state로 저장
2. 사진을 클릭하면 이미 좋아요를 눌렀으면 -1, 좋아요를 누르지 않았으면 + 1

일단 좋아요를 눌렀는지 안눌렀는지를 `onLikes`로 저장

```jsx
  state(){
    return {
      likes : [30, 40, 50],
      onLikes : [false, false, false]
    }
  },
```

그래서 좋아요를 눌렀으면 좋아요 1을 증가하고 `onLikes` 상태를 true로 변경

`onLike`s가 true면 이미 눌렀다는거니까 -1을 해주고 다시 false로 변경

각각 따로 작동되게 해야 하므로(특정항목의 index를 바탕으로 변경해야함.), i라는 데이터를 받아서 

```jsx
 <div :class="필터" class="post-body" @click="$store.commit('likesChange', i)"
     :style="{ backgroundImage : `url( ${a.postImage})` }"></div>
    <div class="post-content">
      <p>{{ $store.state.likes[i] }} likes</p>
```

```jsx
 mutations : {
    likesChange(state, i) {
      if (!state.onLikes[i]){
        state.likes[i] ++;
        state.onLikes[i] = true;
      } else {
        state.likes[i] --;
        state.onLikes[i] = false;
      }
    }
  }
```

이렇게 해준다면 다른 항목으로 작동함.

---

근데 , 만약에 `likes`와 `onLikes`가 사용자 수 만큼 생기게 하려면 어떻게 해야될 지 잘 모르겠다.