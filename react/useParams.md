# useParams

페이지를 여러개 만들 때 URL 파라미터라는 문법을 사용

```jsx
<Route path="/detail/:id" element={ <Detail shoes={shoes}/> }/>
```

하지만, 아무 문자를 넣어도 다 이동하기 때문에 유저가 특정 값을 입력했을 때만 페이지를 변환해주는 문법은 useParams를 사용하면 된다. 

그럼 비슷하지만 다른 내용의 제품을 보여줄 수 있음

```jsx
import { useParams } from 'react-router-dom'

function Detail(){
  let {id} = useParams(); // /detail 뒤에 1, 0,,,,값을 입력하면 그 값이 id에 저장됨
  console.log(id)
  
  return (
    <div className="container>
      <div className="row">
        <div className="col-md-6">
          <img src="https://codingapple1.github.io/shop/shoes1.jpg" width="100%" />
        </div>
        <div className="col-md-6 mt-4">
        <h4 className="pt-5">{props.shoes[id].title}</h4>
        <p>{props.shoes[0].content}</p>
        <p>{props.shoes[0].price}원</p>
        <button className="btn btn-danger">주문하기</button>
      </div>
    </div>
  </div>
  )
}
```

하지만, 자료의 순서가 변경되면 상세페이지도 엉킬 수 있음.

이때는 처음에 data.js의 자료에 id를 정해논 것을 이용해서 **현재 url에 입력한 번호와 같은 id를 가진 데이터**를 보여주라고 코드를 짜면 된다.

```jsx
function Detail(props) {

  let {id} = useParams();
  let idid = props.shoes.find( (x) => x.id == id);
    return (
      <div className="container">
        <div className="row">
          <div className="col-md-6">
            <img src={"https://codingapple1.github.io/shop/shoes.jpg"} width="100%" alt=''/>
          </div>
          <div className="col-md-6">
            <h4 className="pt-5">{idid.title}</h4>
            <p>{idid.content}</p>
            <p>{idid.price}원</p>
            <button className="btn btn-danger">주문하기</button> 
          </div>
        </div>
      </div> 
    )
  }
```