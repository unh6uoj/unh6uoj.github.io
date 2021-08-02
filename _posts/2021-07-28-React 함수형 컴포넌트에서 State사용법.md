---
title: "React 함수형 컴포넌트에서 State사용법"
categories:
  - study
tags:
  - react
---

## React 함수형 컴포넌트에서 State사용법

![react_logo](/images/react_logo.svg){: width="50%" height="50%"}

### Functional Component
🙇 최근 React에서는 클래스형 컴포넌트보단 함수형 컴포넌트를 사용하는 것을 권장하는 고있는 것 같다.

이전에는 함수형 컴포넌트는 클래스형 컴포넌트에 비해 부족한 기능을 가지고 있었지만 리액트 16.8버전부터 Hook이라는 기능을 추가했는데, 이것을 통해 함수형 컴포넌트에서도 State같은 기능들을 사용할 수 있게 되었다고 한다!  

### ❓State란??  
State는 React 컴포넌트 내부에서 관리되는 변수라고 볼 수 있는데, State의 특징은 값이 변경되었을 때 화면이 다시 render가 되면서 화면을 업데이트 해준다는 점이다.  
이 때, State에 직접 접근하여 값을 변경하면 re-render가 되지 않고, 꼭 setter함수 (set~())를 사용해서 값을 변경 해야한다.

이 글에선 Hook을 통해 State를 관리하는 방법에 대해 작성 해보면 좋을 것 같다.

---

먼저 jsx에서 useState를 import해야한다.

```jsx
import React, { useState } from 'react';
```

그리고, useState()라는 함수를 이용해 State를 정의하는 방식이다.

```jsx
const [time, setTime] = useState("2021-08-02");
```  

해당 함수는 배열을 반환하는데, 배열의 첫 번째 변수는 State를 반환하고, 두 번째 는 함수를 반환하는데, State를 변경해주는 함수이다. (class형 컴포넌트의 setState()함수와 같은 기능)  
그리고 useState의 인자로 들어가는 값으로 State를 초기화 시켜 줄 수도 있다.  

```jsx
import React, {useState} from 'react';

function App() {
  const [name, setName] = useState("홍길동");

  return (
    <div>
      {name}

      <button onClick={() => setName("고길동")}>변경!</button>
    </div>
  )
}

export default App;
```

이렇게 간단한 페이지에 State를 뿌려주고, State를 변경할 수 있는 setter함수를 onClick으로 가지고 있는 버튼을 만들었다.  
해당 버튼을 눌러보면 그 즉시 State가 변경되고, 화면이 re-render 되면서 view에서도 변경을 확인할 수 있다.

![react_홍길동](/images/react_홍길동.png){: width="50%" height="50%"}
![react_고길동](/images/react_고길동.png){: width="50%" height="50%"}