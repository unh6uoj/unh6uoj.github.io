---
title: "React 함수형 컴포넌트에서 State사용법"
categories:
  - study
tags:
  - react
---

## React 함수형 컴포넌트에서 State사용법

최근 React에서는 클래스형 컴포넌트보단 함수형 컴포넌트를 사용하는 것을 권장하는 고있는 것 같습니다.  

이전에는 함수형 컴포넌트는 클래스형 컴포넌트에 비해 부족한 기능을 가지고 있었지만 리액트 16.8버전부터 Hook이라는 기능을 추가했는데, 이것을 통해 함수형 컴포넌트에서도 State같은 기능들을 사용할 수 있게 되었습니다.  

이 글에선 Hook을 통해 State를 관리하는 방법에 대해 작성 해보겠습니다.  

---

먼저 jsx에서 useState를 import해야합니다.

```jsx
import React, { useState } from 'react';
```

