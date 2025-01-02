# watcher

사용자가 입력한 값을 감시하는 역할 →  **특정 데이터가 변경될 때마다 실행되는 코드**

```jsx
export default {
  data(){
    return {
      month : 1
    }
  },
  watch : {
    month(){
      //month가 변경될 때 실행할 코드
    }
  }
}
```

watch에서의 함수를 만들 때는 **내가 감시하고 싶은 데이터 명**으로 작성해야 판단 가능. (위에서는 month를 감시)

사용자가 입력한 값이 문자일 경우 alert메세지를 보내는 코드

(`isNaN()` 안에 숫자를 입력하면 false,

 글자를 입력하면 true가 나온다. )

```jsx
watch : {
    month(a){
      if (isNaN(a) == true){
        alert('문자입력하지마라');
        this.month = 1;
      }
    },
 },
```