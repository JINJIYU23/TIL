# input태그 사용하기

### input : 유저의 입력을 받을 수 있는 박스

```jsx
<input type="text"></input>
<input type="range"/>
<input type="date"/>
<input type="number"/>
<textarea></textarea>
<select></select>
```

다양한 input box가 많음

- 유저가 input에 입력한 값에 이벤트를 주고 싶을 땐

```jsx
<input onChange={()=>{ 실행할코드 }}/>
// 이벤트핸들러는 매우 많음
```

- 유저가  입력한 값을 가져 올 때 → e.target.value

```jsx
      <input type='text' onChange={(e) => {
        // e는 내가 지금 입력한 것을 받아와 줌 
        // e.target.value는 내가 입력한 text...등을 가져와서 보여줌
        setInput(e.target.value);
        console.log(input);
      }}></input>
```

뒤에 value말고 다른 값들도 가져올 수 있음

e.preventDefault() : 이벤트 기본 동작 막아줌

e.stopPropagation() : 이벤트 버블링 막아줌

- 사용자가 input에 저장한 데이터를 저장 → 변수나 state사용 가능

```jsx
let[input, setInput] =useState('');
//<생략>

      <input type='text' onChange={(e) => {
        // e는 내가 지금 입력한 것을 받아와 줌 
        // e.target.value는 내가 입력한 text...등을 가져와서 보여줌
        setInput(e.target.value);
        console.log(input);
      }}></input>
```