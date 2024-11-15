# react bootstrap

리액트에서 bootstrap을 사용하려면 자바스크립트와 마찬가지로 몇 개의 작업이 필요함.

[https://react-bootstrap.netlify.app/docs/getting-started/introduction](https://react-bootstrap.netlify.app/docs/getting-started/introduction)

```jsx
npm install react-bootstrap bootstrap
```

이걸 터미널에 써주고 시작하면 된다. 그럼 설치 완료.

근데, 중요한 점은 bootstrap을 쓰고 싶다면 import를 해주는 것이 중요하다.

```jsx
import './App.css';
import 'bootstrap/dist/css/bootstrap.min.css';   // 필수
// function안에 있는 대문자로 된 html(?)들을 꼭 import 해줘야함
import { Navbar, Container, Nav } from 'react-bootstrap';

function App() {
  return (
    <div className="App">
      <Navbar bg="dark" data-bs-theme="dark">
        <Container>
          <Navbar.Brand href="#home">Navbar</Navbar.Brand>
          <Nav className="me-auto">
            <Nav.Link href="#home">Home</Nav.Link>
            <Nav.Link href="#features">Features</Nav.Link>
            <Nav.Link href="#pricing">Pricing</Nav.Link>
          </Nav>
        </Container>
      </Navbar>
    </div>
  );
}

export default App;
```