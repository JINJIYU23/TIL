# 상품 정렬 기능 & 데이터 원본 보존

- 가격순 정렬

```jsx
<button @click="priceSort()">가격순정렬</button>

    // 정렬 함수
    priceSort(){
      this.onerooms.sort(function(a,b){
        return a.price - b.price;
      });
    },
```

여기 a.price - b.price 음수 : 오름차순 정렬 (1,2,3)

a.price - b.price 양수 : 내름차순 정렬 (3,2,1)

- 되돌리기

```jsx
<button @click="sortBack()">되돌리기기</button>

data(){
  return {
    oneroomsOriginal :[...postData],
    onerooms : postData,
  }
}
    sortBack(){
      this.onerooms = [...this.oneroomsOriginal];
    },
```

오리지널 원본(oneroomsOriginal)을 하나 만들어두고 되돌리기 버튼을 oneroomsOriginal을 가져와서 집어 넣는 것.

array 자료를 복사하거나, 

값 공유가 일어나지 않게 집어 넣고 싶으면,

**`[…array자료]`**로 사용하기.