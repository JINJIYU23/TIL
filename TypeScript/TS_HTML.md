# 타입스크립트로 HTML변경 & 조작

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <h4 id="title">Hello</h4>
    <a href="http://naver.com">네이버</a>
    <button id="button">버튼</button>
    <img id="image" src="test.jpg">

    <a class="naver" href="http://naver.com">링크</a>
    <a class="naver" href="http://naver.com">링크</a>
    <a class="naver" href="http://naver.com">링크</a> 

    <script src="newfile.js"></script>
</body>
</html>
```

html 파일과 ts파일을 연결.

`id`, `class` html을 찾고 연결 할 때는,

1. narrowing

```tsx
let 제목 = document.querySelector('#title');

if(제목 != null) {
    제목.innerHTML = '반가워';
}
```

1. instanceof

```tsx
let 제목 = document.querySelector('#title');
if(제목 instanceof Element) {
    제목.innerHTML = '반가워';
}
```

instanceof 오른쪽에 HTMLElement를 입력하면 됨.

1. assertion

```tsx
let 제목 = document.querySelector('#title');
let 제목 = document.querySelector('#title') as HTMLElement;
제목.innerHTML = '반가워'
```

별로 좋지 않은 임시 방법.

1. optional chaining

```tsx
let 제목 = document.querySelector('#title');
if(제목?.innerHTML != undefined) {
    제목.innerHTML = '반가워';
}
```

왼쪽에 있는 object자료 안에 `.innerHTML` 이 존재하면 if문 실행이고, 없으면 `undefined`

### a태그의 href 속성 바꾸기

```tsx
let 링크 = document.querySelector('.link');

if(링크 instanceof HTMLAnchorElement) {
    링크.href = 'http://kakao.com';
}
```

`a` 태그는 `HTMLAnchorElement`

`img` 태그는 `HTMLImageElement`

`h4` 태그는 `HTMLHeadingElement`

…

각 속성 별로 맞는 타입으로 narrowing해줘야 함.

### 이벤트 리스너

```
let 버튼 = document.querySelector('#button');
	버튼?.addEventListener('click', function () {
	console.log('안녕');
})

// or

let 버튼 = document.getElementById('button');

if (버튼) {
  버튼.addEventListener('click', function () {
    console.log('안녕');
  });
}
```

- 버튼 누르면 이미지 바꾸기

```tsx
let 사진 = document.querySelector('#image');

if(사진 instanceof HTMLImageElement) {
    사진.src = 'new.jpg';
}
```

- 많은 html 요소 바꿔주기

```
let 카카오 = document.querySelectorAll('.naver')
카카오.forEach((a) => {
    if(a instanceof HTMLAnchorElement) {
        a.href = 'http://kakao.com';
    }
});
```