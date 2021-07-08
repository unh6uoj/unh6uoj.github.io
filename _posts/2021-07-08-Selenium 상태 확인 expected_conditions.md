---
title: "Selenium 상태 확인 expected_conditions"
categories:
  - study
tags:
  - python
  - selenium
---

## Selenium expected_conditions의 종류

요즘 대부분의 웹 사이트들은 데이터들을 동적으로 받아와서 화면에 뿌려준다.

그래서 웹 사이트가 데이터를 받아오기까지 시간이 필요한데, 흔히 selenium으로 웹 크롤링을 진행 하면서 이런 로딩 시간 때문에 에러가 많이 발생하곤 한다.



selenium에선 WebDriverWait이라는 모듈을 통해 로딩을 대기하는 방법을 제공해주고 있다. 

https://selenium-python.readthedocs.io/waits.html 👈 공식 문서 참조!



WebDriverWait에선 크게 두 가지의 대기 방법을 제공하고 있는데,

1. Explicit Waits (명시적 대기)와
2. Implicit Waits  (암시적? 대기)인데, 이 둘의 차이점에 대해선 많이 알려져 있으니,

이 글에선 Explicit Waits가 제공해주는 expected_conditions에 대해서 소개를 해보려고 한다.

expected_conditions는 특정 element가 어떤 상태를 가지는 것?에 대한 함수이다. 이 함수를 이용하면 찾고자하는 element가 지정한 condition이 됐다는 것을 알 수 있다.

먼저, 아래 내용을 코드에 추가하면 import를 할 수 있다. (Python3 기준)

```python
from selenium.webdriver.support import expected_conditions as EC
```



```python
wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID, 'someid')))
```

그리고 이렇게 함수를 실행하는데, webDriverWait()에는 webdriver와 최대 대기 시간(초)가 인자로 들어가고, until()에는 expected_conditions객체가, EC.element_to_clickable()이 어떤 상태를 가리키는 함수인데, 흔히 속성이름과 값이 튜플 형태로 들어간다.

By는 속성을 참조할 때 사용하는데,

```python
from selenium.webdriver.common.by import By
```

이걸 import하면 된다.



공식 문서를 보니 expected_conditions는 총 17가지를 제공한다고 나와있는데, 하나하나 살펴보자

- title_is(**title**)

  - 페이지 제목을 확인하기 위한 함수다. 인자로 들어간 제목과 현재 페이지 제목이 같다면true를, 아니라면 false를 반환한다.

- title_contains(**title**)

  - 페이지 제목을 확인하는데, 대/소문자를 구분한다. 같으면 true, 다르면 false

  

- presence_of_element_located(**locator**)

  - locator로 들어간 element가 DOM에 있는지 확인한다. element가 존재하면 true, 없다면 false

- presence_of_all_elements_located(**locator**)

  - locator로 들어간 element가 하나 이상 존재하는지 확인하고, 찾는 element들을 리스트로 반환

  

- visibility_of(**locator**)
  - locator로 들어간 element가 보이는지 확인한다. DOM에는 있지만 hidden등의 속성 값으로 보이지 않는 element들을 체크하는데 사용. 해당 element가 보인다면 True, 그렇지 않다면 False를 반환.
  - 주의! width나 height 등의 속성값이 0이 돼서 보이지 않는 element들 또한 보이지 않는 것으로 취급 (visibility~~ 함수들 모두 해당)
- visibility_of_element_located(**locator**)
  - locator로 들어간 element가 보이는지 체크하고, DOM에도 있는지 체크한다.
- invisibility_of_element_located(**locator**)
  - locator로 들어간 element가 보이지 않다면 true를 반환, 보인다면 false를 반환한다.



⚠️text_to_be~ 는 정확하지 않습니다...

- text_to_be_present_in_element(**locator, text_**)

  - text_가 locator에 존재하는지 확인. 존재하면 true, 없다면 false를 반환

- text_to_be_present_in_element_value

  - locator로 들어간 element에 text와 text_를 비교, 같다면 true, 다르면 false를 반환한다.

  

- frame_to_be_available_and_switch_to_it(**locator**)

  - locator로 frame이 들어가고 해당 frame을 사용할 수 있다면 그 frame을 반환한다.

  

- element_to_be_clickable(**locator**)

  - locator로 들어간 element가 클릭할 수 있는지 확인하고 클릭할 수 있으면 해당 element를 반환한다.

  

- staleness_of(**locator**)

  - ❓️ 확인 필요함

  

- element_to_be_selected(**locator**)

  - locator가 선택 가능한 element일 때, 선택이 되었는지 확인.

  

- element_located_to_be_selected(**locator**)

  - locator가 DOM에 존재하는지 확인하고, 선택이 되었는지 확인.
  - ⚠️정확하지 않습니다.

  

- element_selection_state_to_be(**element, is_selected**)

  - element가 bool형의 is_select와 같은 상태인지(select 되었는지) 확인한다.

- element_located_selection_state_to_be(**locator, is_selected**)

  - locator로 들어간 element가 존재하고 선택(select) 가능한지 확인하고, bool형의 is_selected와 비교한다.

  

- alert_is_present

  - alert창이 존재하는지 확인한다.



이런 expected_conditions를 잘 활용하면 time.sleep()등을 활용한 크롤링보다 더 빠르고 안정적으로 데이터를 수집할 수 있다.

