---
title: "Python FastAPI 알아보고 설치하고 초기 설정 해보기"
categories:
  - study
tags:
  - python
  - fastAPI
---

## Python FastAPI, 설치하고 초기 설정 해보기

![fastapi_logo](/images/fastapi_logo.png)  

파이썬 웹 서버를 만들어야 하는 일이 생겼늗데, 최대한 빠르고 안정적인 서버를 선택 해야했다.  
그래서 기존에 사용하던 Flask보다 훨씬 빠르다고 하는 FastAP를 사용해보기로 했다.

<br>
---
<br>

### ❓ FastAPI란?
👉 FastAPI 공식 한국어 페이지
<https://fastapi.tiangolo.com/ko/>  


> FastAPI는 현대적이고, 빠르며(고성능), 파이썬 표준 타입 힌트에 기초한 Python3.6+의 API를 빌드하기 위한 웹 프레임워크입니다.

FastAPI는 파이썬에서 사용 가능한 웹 프레임워크 중 하나인데, Flask나 Django보가 훨씬 빠른 속도를 보여준다고 하고, 확인 해봐야 하겠지만 Go언어와도 비슷한 속도를 보여준다고 한다.  

또, 쉽고 간결한 코드, 200% ~ 300% 까지 증가하는 개발 속도를 기대할 수 있다고 하는데, 시작 해보자! 👏  

<br>
---
<br>

### FastAPI 설치
먼저 공식 사이트에선 pip를 이용해 설치 하라고 나와있는데, 나는 anaconda를 이용해서 설치를 했다.

> bash  
> $ pip install fastapi
  

> anaconda 사용 시  
> $ conda install fastapi

<br>

그리고 ASGI서버도 필요해서 같이 설치하라고 하는데, Univorn을 설치 해보자.

> bash
> $ pip install uvicorn[standard]


> anaconda 사용 시
> $ conda install uvicorn

<br>

### FastAPI 예제

설치가 완료되면 이렇게 vscode에서 FastAPI() 클래스가 자동 완성 되는걸 확인할 수 있다.  
![fastapi_import](/images/fastapi_import.png)

그리고 정말 간단히 API를 만들 수 있는데,  
main.py 파일을 만든 후에
```python
from typing import Optional

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello" : "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    return {"item_id": item_id, "q": q}
```

이렇게 작성하고 터미널에 하단의 명령어를 작성하면
> $ uvicorn main:app ---reload  

이 명령어 뒤에 붙은 ---reload는 코드가 변경 되었을 때 자동으로 서버를 재 실행하라는 명령어란다.  

![fastapi_run](/images/fastapi_run.png)

이렇게 뜨면서 FastAPI로 만든 첫 웹 서버가 실행 된다.  

FastAPI의 기본 포트는 8000으로 되어 있는 것 같으므로,  
<http://127.0.0.1:8000>  
또는  
<http://localhost:8000>  

으로 접속 하면  
![fastapi_root](/images/fastapi_root.png){: width="100%" height="100%}  
이렇게 root경로가 잘 나오는걸 확인 할 수 있다.  

그리고, <http://127.0.0.1:8000/items/123?q=coffee>  
이쪽으로 접속하게 되면 GET 메소드도 쉽게 활용할 수 있는걸 확인할 수 있다.
![fastapi_coffee](/images/fastapi_coffee.png){: width="100%" height="100%}

<br>
---
<br>

### 예제 코드 뜯어보기
상단의 코드를 하나씩 살펴보면  


```python
from typing import Optional
from fastapi import FastAPI
# 이 부분은 함수에 None이 혀용되는 매개변수에 대한 타입을 명시할 때 사용되는 Optional을 import하고

#FastAPI를 import 하는 부분
```

```python
app = FastAPI()
# 그냥 FastAPI()클래스 객체 생성
```

```python
@app.get("/")
def read_root():
    return {"Hello" : "World"}

# @app.get("/") 부분에서 루트 경로인것과 GET이란걸 명시했다는 것을 쉽게 알 수 있다.
# return 하는 부분에 해당 경로의 response를 작성하면 된다.
```

```python
@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    return {"item_id": item_id, "q": q}

# 여기선 /items/item_id 경로를 명시했다는걸 알 수 있는데, 마지막 {}에 감싸져 있는 부분은 변수라고 볼 수 있는 것 같다.

# item_id로 들어간 값은 int형이라고 명시하고, q라는 GET방식의 query 또한 있는 것을 알 수 있다.
```

여기서 int라고 해놓은 item_id에 str을 넣게 되면 422에러를 return하게 되므로 나중에 잘 체크 해야한다.  
<http://127.0.0.1/items/밥?q=coffee>

![fastapi_type_error](/images/fastapi_type_error.png)

<br>
---
<br>

FastAPI 설치와 기본 사용 방법에 대해 알아봤는데, 이렇게 간단한 예제에서는 Flask역시 정말 간단한 코드로 웹 서버를 구현할 수 있어서 Flask와는 큰 차이를 느낄 수 없었다.  
나중에 더 많은 테스트를 해봐야지 얘가 얼마나 빠른지 알 수 있을 것 같은데, 기대된다😊