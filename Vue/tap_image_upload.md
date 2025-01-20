# 탭으로 사진 업로드 페이지 만들기

자꾸 까먹는게 새로 UI를 만드려고 하면 현재 상태를 data로 저장해주어야 한다는 걸 자꾸 까먹는다.

일단, 

메인 화면에는 `Post.vue`로 각각의 피드를 보여주고, 

사진을 업로드 하는 화면, 

업로드한 사진과 글을 입력하는 화면

이러한 레이아웃이 필요하다.

그래서 필요한 화면이 각각 다른 상황에서 적용되도록 코드를 짜주면 된다.

---

1. `step`이라는 데이터로 화면에 따라 달라질 상태 저장해두기

```jsx
(App.vue)

  data() {
    return {
      step : 0,
    }
  },
  com
```

1. `step = 1`이면 이미지를 업로드 하고 필터를 선택할 페이지로 변경해주기.

```jsx
(Container.vue)
    <!-- 필터선택페이지 -->
    <div v-if="step == 1">
      <div class="upload-image" :style="`background-image: url(${image})`"></div>
        <div class="filters">
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
      </div>
    </div>
```

1. `step = 2` 이면 글작성 페이지 보여주기

```jsx
  (Container.vue)
  <!-- 글작성페이지 -->
  <div v-if="step == 2">
    <div class="upload-image" :style="`background-image: url(${image})`"></div>
    <div class="write">
      <textarea class="write-box"
      @input="$emit('write', $event.target.value)">
      write!</textarea>
    </div>
  </div>
```

---

근데 업로드할 사진과 멘트를 사용자가 원하는대로 하려면

```jsx
  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
 </div>
```

`<input>` 안에 있는 것을 file로 업로드 한다는 것을 일단 정의해주고, `upload` 함수를 이용해서 기능을 구현하는데

```jsx
    upload(e){
      let 파일 = e.target.files;
      let imgURL = URL.createObjectURL(파일[0]);
      this.image = imgURL
      this.step++;
    },
```

일단 `파일` 은 사용자가 가져온 이미지 파일이고

`imgURl` 은 파일의 URL을 가져온다.

위에서 선언한 데이터 `image` 를 `imgURL` 로 변경해주고, 

step 0에서 step 1으로 넘어갈 수 있는 기능을 구현해준다.

그리고 이미지를 `props`로 전송해줘서 `Container.vue`에서 `background-image` 기능으로 넣어주면 된다.

---

글작성 페이지로 넘어가서 기능 구현을 하려면

데이터를 저장한 `Instadata.js`의 형식인 아래와 같아야 한다.

```jsx
[
    {
      name: "Kim Hyun",
      userImage: "https://picsum.photos/100?random=3",
      postImage: "https://picsum.photos/600?random=3",
      likes: 36,
      date: "May 15",
      liked: false,
      content: "오늘 무엇을 했냐면요 아무것도 안했어요 ?",
      filter: "perpetua"
    },]
```

따라서

step1에서 step2로 바뀌면 `publish` 함수를 실행해 달라고 짰다.]

`unshift()` 는 array에 데이터 하나를 추가해주는 자바스크립트 문법

```jsx
    publish(){
      var myFeed = {
      name: "Kim Hyun",
      userImage: "https://picsum.photos/100?random=3",
      postImage: this.image,
      likes: 36,
      date: "May 15",
      liked: false,
      content: this.word ,
      filter: "perpetua"
      };
      this.인스타데이터.unshift(myFeed);
      this.step = 0;
    },
```

이미지도 업로드 한 이미지로 변환해줘야 하기 때문에 `this.image`로 변경해주고,

멘트도 사용자가 작성한 것으로 변경해줘야 하기 때문에 `this.word` 로 바꿔주는데, 

`word` 를 새로운 data로 선언해주고,

 `Container.vue`에서 `App.vue` 로 보내주는 것이기 때문에 (자식 → 부모) `$emit` 를 써줘야한다.

```jsx
      <textarea class="write-box"
      @input="$emit('write', $event.target.value)">
      write!</textarea>
```

```jsx
@write = "word = $event"
```

이걸 써줌으로 사용자가 입력한 멘트가 전달되어 바뀌게 된다.

아.. 어렵다..