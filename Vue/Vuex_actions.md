# Vuex - actions

Vuex에서 state를 수정할 때 mutations 함수를 만들어서 수정한다.

하지만, 서버에서 수정하고 싶을 때는 ajax요청을 보내서 수정하면 된다. 그때는 **actions**라는 항목에 적어야 함. 

```jsx
actions : {
  데이터가져오기(){
    axios.get('').then(()=>{ 
      성공시 실행할 코드 
    })
  }
}
```

이렇게 적어주고 `$store.dispatch('데이터가져오기')` 라고 했을 때 데이터를 가져와줌.

```jsx
actions : {
  데이터가져오기(context){
    axios.get('').then(()=>{ 
      context.commit('mutations함수명') 
    })
  }
}
```

데이터를 가져온 직후에 그걸로 state 변경하고 싶으면 위에 코드처럼 사용한다.

state 변경시에는 무조건 mutations 함수를 만들어 써야 하기 때문.

mutations함수를 사용할 땐 예외없이 `commit()` 라고 써줘야 함.

---

actions는 서버에 데이터를 요청할 때 쓰이는 것이기 때문에 살짝은 어려운 것 같다.