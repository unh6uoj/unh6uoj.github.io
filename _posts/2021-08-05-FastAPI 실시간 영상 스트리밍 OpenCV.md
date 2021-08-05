---
title: "FastAPI 실시간 영상 스트리밍 OpenCV"
categories:
  - study
tags:
  - fastAPI
  - http
  - openCV
---

## FastAPI와 OpenCV를 활용한 실시간 영상 스트리밍

실시간 영상을 스트리밍 하는 방법을 찾던 중 파이썬 FastAPI를 활용한 방법을 시도 해보았다.  

---

### 필수 라이브러리

필요한 것은  
> Python3.9버전 (애플 M1칩셋 맥북에어에서 3.8 버전으로 시도 해보니 OpenCV라이브러리 설치에서 문제가 발생했었다)  
> FastAPI  
> uvicorn  
> OpenCV  

정도면 될 것 같다.
라이브러리들은 모두 설치 되었다고 가정 하고,

---

### 예제 코드

```python
# main.py

# 라이브러리 import
# StreamingResponse를 가져와야함
from fastapi import FastAPI
from fastapi.responses import StreamingResponse

# cv2 모듈 import
from cv2 import get_stream_video

# FastAPI객체 생성
app = FastAPI()

# openCV에서 이미지 불러오는 함수
def video_streaming():
    return get_stream_video()

# 스트리밍 경로를 /video 경로로 설정.
@app.get("/video")
def main():
    # StringResponse함수를 return하고,
    # 인자로 OpenCV에서 가져온 "바이트"이미지와 type을 명시
    return StreamingResponse(video_streaming(), media_type="multipart/x-mixed-replace; boundary=frame")
```

```python
# cv2.py

import cv2

def get_stream_video():
    # camera 정의
    cam = cv2.VideoCapture(0)

    while True:
        # 카메라 값 불러오기
        success, frame = cam.read()

        if not success:
            break
        else:
            ret, buffer = cv2.imencode('.jpg', frame)
            # frame을 byte로 변경 후 특정 식??으로 변환 후에
            # yield로 하나씩 넘겨준다.
            frame = buffer.tobytes()
            yield (b'--frame\r\n' b'Content-Type: image/jpeg\r\n\r\n' +
               bytearray(frame) + b'\r\n')
```

### 실행

FastAPI를 사용해 웹 서버를 여는 main.py파일과, openCV로 영상 데이터를 얻는 cv2.py모듈을 만들었다.  

> 터미널  
> uvicorn main:app --reload

로 FastAPI서버를 실행 해보고 <http://localhost:8000>에 접속 해보면 OpenCV에서 불러온 영상들이 실시간으로 브라우저에서 잘 나오는것을 확인 할 수 있었다.  

![streaming_image](/images/streaming_image.jpeg)