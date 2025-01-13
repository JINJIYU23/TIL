# Vue의 라이프사이클

1. 컴포넌트를 보여줄 때 creat → mount 단계로 생성

(creat는 생성, mount는 `index.html` 파일에 장착)

1. 데이터가 바뀌면서 컴포넌트가 재렌더링 될 때는 update
2. 다른 페이지로 이동하면서 컴포넌트가 삭제될 때는 unmount 

이때, 이 단계들 사이에 코드를 실행시키고 싶을 때는

`beforeCreate(), created(), beforeMount(), mounted(), beforeUpdate(), updated(), beforeUnmount(), unmounted()`

등 등..

홍보 컴포넌트를 2초후에 사라지게 하고 싶다면

```jsx
  <!-- 홍보 컴포넌트 -->
  <DiscountBanner v-if="showDiscount == true" />
  
  data(){
  return {
  
  }
},
    mounted(){
    setTimeout(()=>{
      this.showDiscount = false;
    },2000);
  },
```

1초당 할인율이 1씩 감소하고 할인율이 0이 되면 팝업 숨기기

```jsx
mounted(){
    // setTimeout(()=>{
    //  this.showDiscount = false;
    // },2000);
    var timer = setInterval(()=>{
      this.amount--;
      if(this.amount == 0){
        clearInterval(timer)
        this.showDiscount = false;
      }
    },1000);

```

데이터가 변경되면 컴포넌트가 재렌더링 되는데, 이게 update임.

모달에 input칸에 2를 입력했을 때 alert 창 띄우기

```jsx
        beforeUpdate(){
            if(this.month == 2){
                alert("2개월은 판매하지 않습니다.")
            }
            
```