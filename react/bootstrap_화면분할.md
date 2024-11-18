
# Bootstrap을 이용해서 화면 분할

```jsx
    <Container>
      <Row>
        <Col>
          <div>
            <img src="https://codingapple1.github.io/shop/shoes1.jpg" alt='' style={{width : "80%" }}/>
            <h4>상품명</h4>
            <p>상품설명</p>
          </div>
        </Col>

        <Col>
        </Col>
        
        <Col>
        </Col>
      </Row>
    </Container>
```

container와 row를 이용하면 화면 분할 가능.

중간에 이미지 넣을 때는 경로 써 주고 alt='' 이거 필수.(리액트 Col일때만 인듯…?)

 style={{width : "80%" }} 이것도 간단해 보이지만 고민 고민 하며 작성한 것. 80%만 썼다가 자꾸 오류나서 “” 감싸고 넣어줌.