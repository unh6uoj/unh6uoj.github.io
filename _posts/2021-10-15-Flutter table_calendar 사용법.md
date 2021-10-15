---
title: "Flutter table_calendar 사용법"
categories:
  - study
tags:
  - flutter
  - dart
toc: true
toc_sticky: true
---

## Flutter table_calendar 사용법
Flutter에는 달력을 출력할 수 있는 여러가지 패키지가 있는데, 그 중 하나인 table_calendar에 대해서 알아보았다.

### 설치
> flutter pub add table_calendar  


```
dependencies:
  table_calendar: ^3.0.2
```

### 사용법

``` dart
import 'package:table_calendar/table_calendar.dart';
```

``` dart
TableCalendar(
  firstDay: DateTime.utc(2010, 10, 16),
  lastDay: DateTime.utc(2030, 3, 14),
  focusedDay: DateTime.now(),
);
```  
먼저, 생성자에 필수로 들어가는 항목은 달력의 첫 번째 날짜, 마지막 날짜, 선택 날짜인데, dart의 DateTime을 사용해서 적절하게 넣어주면 된다.  
이 날짜를 넘어가는 항목들은 출력되지 않는다.

![requests_install](/images/flutter/table_calendar.png)

그러면 이렇게 달력이 잘 출력된다.

#### 한글 사용하기  
공식 문서에서 언어 설정을 하기 위해선 locale을 설정하면 된다고 하는데, 그러면 에러가 발생한다.  
``` dart
TableCalendar(
    locale: 'ko-KR',
);
```

한글 달력을 사용하기 위해선, intl이라는 패키지를 설치 해야한다.
> flutter pub add intl

``` dart
import 'package:intl/date_symbol_data_local.dart';
```

해당 패키지를 import하면 locale 설정이 잘 되는것을 확인 할 수 있다.