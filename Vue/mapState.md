# mapState

state를 vue파일에서 꺼내쓸 때 `$store.state.name` 이런 식으로 썼지만, 

`mapState` 를 써주면 더 간편하게 쓸 수 있다.

---

함수를 만들 때, `computed{}` 안에 만들 수 있다.

```jsx
computed : {
  now2(){
    return new Date()
  }
}, 
methods : {
  now(){
    return new Date()
  }
}
```

두 함수의 차이점은 **methods**안에 있는 함수는 호출할 때마다 안의 코드가 실행됨.

**computed**함수는 함수를 호출해도 코드가 실행되지 않음. → 컴포넌트 로드시 한번 실행되고 그 값을 계속 저장하고 있음. **계산 결과 저장 공간**

return 꼭 써주기, 가져다 쓸 때는 소괄호 없이 함수명만 (`now2` 이런식) 

만약 데이터가 길고 복잡한 state를 computed안에 쓰면 짧게 사용 가능.

```jsx
computed : {
  name(){
    return this.$store.state.name
  }
}
```

필요할 때 `name` 으로 호출해서 사용 가능

---

```jsx
import {mapState} from 'vuex'

computed : {
  ...mapState(['state이름1', 'state이름2'])
}
```

이런식으로 쓴다면 state가 1만개 일때 computed도 1만개를 만들어야 하는 수고를 덜어줌.

```jsx
import {mapState} from 'vuex'

computed : {
  ...mapState({ 작명 : 'state이름1'})
}
```

object자료형을 쓰면 state 가져올 때 이름 변경도 할 수 있음.

```jsx
import {mapState, mapMutations} from 'vuex'

computed : {
  ...mapState(['state이름1', 'state이름2']),
  ...mapMutations([ '좋아요', 'setMore' ])
}
```

`mapMutations`도 가져와서 `$store.commit('좋아요')` 이런식이 아니라 `좋아요()` 이렇게 써줄 수 있음.

`mapActions`도 있음.