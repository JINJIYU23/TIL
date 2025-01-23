# 멀리 있는 컴포넌트에 데이터를 전송 : mitt

- mitt 설치

```jsx
npm install mitt
```

- `main.js`

```jsx
import { createApp } from 'vue'
import App from './App.vue'

import mitt from 'mitt'
let emitter = mitt();
let app = createApp(App);
app.config.globalProperties.emitter = emitter;

app.mount('#app') 
```

- mitt 사용법

데이터를 보내고 싶은 곳에서

```jsx
this.emitter.emit('이벤트명이름', '데이터')
```

데이터를 수신하고 싶은 곳에서 (보통 mounted 안에 적음)

```jsx
  mounted() {
		this.emitter.on('이벤트명작명', (a)=>{
		  데이터수신시 실행할 코드
		  a는 출력해보면 데이터나옴 
		})
  },
```

---

`FilterBox.vue`에서

```
    methods : {
      onfilter(){
        this.emitter.emit('필터입히기', this.filter)
      }
    },
```

`App.vue`로

```
  mounted() {
    this.emitter.on('필터입히기', (a)=>{
      this.필터 = a;
    })
  },
```