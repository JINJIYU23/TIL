# custom hook으로 코드 재사용

일단 다른 파일로 hook을 모아 놓는다.

```jsx
(like.js)

import { useState } from "react"

export function useLike () {
    let [like, setLike] = useState(0)
    function addLike() {
      setLike(a => a + 1)
    }

    return [like, addLike];
}
```

함수안에 있는 변수는 함수 바깥에서 못 쓴다. → return 키워드를 사용해서 변수를 빼줘야한다.

```jsx
import { useLike } from '../hooks/like.js';

let [like, addLike] = useLike()
.
.
.
{like} <span onClick={() => addLike()}>❤️</span>
```

이렇게 하면 사용 가능

1. useState, useEffect 등의 코드를 담고 있는 함수 작명할 때는 **use를 붙여야함** 
2. useState, useEffect 이런걸 hook이라고 부르는데 useState, useEffect 등을 담고 있는 함수는 **custom hook**