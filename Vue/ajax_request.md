# ajax요청

서버는 요청했을 때 데이터를 주는 것.

서버에게 데이터를 요청할 때는 GET/POST 요청을 써야함.

**GET** : **데이터를 가져올 때 사용**, 서버가 요구하는 URL을 적어야함.

**POST** : **서버로 데이터를 보낼 때 사용**, 서버가 요구하는 URL을 적어야함 

---

Ajax 요청을 하려면 `axios`나 fetch를 사용.

`npm install axois` 후,

```jsx
import axios from 'axios';

axios.get('서버URL').then( 결과 => {
  GET요청 성공시 실행할 코드~~
  console.log(결과);
}).catch(()=> {
실패시 실행할 코드
})
```

→ 이런 형식임.

```jsx
import axios from 'axios';

axios.post('서버URL', '보낼데이터').then( 결과 => {
  POST요청 성공시 실행할 코드~~
}).catch( ()=>{
  실패시 실행할 코드
})
```

→ post요청을 보낼 수 있음.

### 더보기 버튼을 누르면 데이터를 요청해서 `<Post>`에서 하나 더 보여주기

```jsx
  <template>
  <button @click="more">더보기</button>
  </template>
  
  
  <script>
  import axios from 'axios';
  
  export default {
  name: 'App',
  data() {
    return {
      인스타데이터 : instaData,
      더보기 : 0,
    }
  },
  methods :  {
    more(){
      // axios.post('URL', {name : 'kim'}).then().catch(()=>{
      // })
      axios.get(`https://codingapple1.github.io/vue/more${this.더보기}.json`)
      .then((result)=>{
        this.인스타데이터.push(result.data);
        this.더보기 ++;
      })
    }
  }
  </script>
```