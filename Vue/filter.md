# 사진 필터 기능 만들기

`FilterBox.vue`파일을 하나 만들고, 필터 기능을 사용할때마다 불러와서 사용할 것임.

- 인스타 필터명

```jsx
[ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
"inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
"reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"]
```

- cssgram 설치

cssgram은 인스타그램 필터를 흉내낼 수 있음.

`filter`, `linear-gradient` 속성으로 인스타그램 필터를 재현한 라이브러리

```jsx
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cssgram/0.1.12/cssgram.min.css" integrity="sha512-kr3JaEexN5V5Br47Lbg4B548Db46ulHRGGwvyZMVjnghW1BKmqIjgEgVHV8D7V+Cbqm/VBgo3Rcbtv+mGLoWXA==" crossorigin="anonymous" />
```

`link`태그를 `index.html` 안에 넣어주기

---

`Container.vue` 안에는

```jsx
    <!-- 필터선택페이지 -->
    <div v-if="step == 1">
      <div :class="필터" class="upload-image" :style="`background-image: url(${image})`"></div>
        <div class="filters">
          <FilterBox :image = "image" v-for="filter in filters " :key="filter"
          :filter = "filter">{{ filter }}</FilterBox>
        </div>
    </div>
    
    
    data() {
      return {
        filters :
        [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
          "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
          "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
        //필터 : '',
      }
    },
```

- `FilterBox.vue`

```jsx
<template>
  <div @click="onfilter" :class="[`${filter}`, 'filter-item']" :style="`background-image: url(${image})`">
    <slot></slot>
  </div> 
</template>

<script>
export default {
    name : 'FilerBox',
    props : {
        image : String,
        filter : String,
    },
    methods : {
      onfilter(){
        this.emitter.emit('필터입히기', this.filter)
      }
    },
}
</script>
```