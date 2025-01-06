# UI 애니메이션

- `<Transition>` 태그를 이용할 때

```jsx
.이름-enter-from { 애니메이션 동작 전 상태 }
.이름-enter-active { 애니메이션 동작 중 상태, 대부분 transition 이런거 }
.이름-enter-to { 애니메이션 동작 후 상태 }

  <!-- 모달 및 애니메이션 -->
  <Transition name="fade">
    <FirstModal  @openModal="modalOpen = false"
    :onerooms="onerooms" :clicked="clicked" :modalOpen="modalOpen"/>
  </Transition>

/* 시작스타일 */
.fade-enter-from {
  opacity: 0;
}

.fade-enter-active{
  transition: all 1s;
}

/* 끝스타일 */
.fade-enter-to{
  opacity: 1;;
}
```