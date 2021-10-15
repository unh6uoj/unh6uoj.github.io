---
title: "Flutter table_calendar 기본 사용법"
categories:
  - study
tags:
  - flutter
  - dart
toc: true
toc_sticky: true
---

Flutter에는 달력을 출력할 수 있는 여러가지 패키지가 있는데, 그 중 하나인 table_calendar에 대해서 알아보았다.

## 설치
> flutter pub add table_calendar  


```
dependencies:
  table_calendar: ^3.0.2
```

---

## 사용법

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
먼저, 생성자에 필수로 들어가는 항목은 달력의 첫 번째 날짜, 마지막 날짜, 선택 날짜가 있다.   dart의 DateTime을 사용해서 적절하게 넣어주면 된다.  
이 날짜를 넘어가는 항목들은 출력되지 않는다.

![table_calendar](/images/flutter/table_calendar.png)

그러면 이렇게 달력이 잘 출력된다.

#### 한글 사용하기  
공식 문서에서 언어 설정을 하기 위해선 locale을 설정하면 된다고 하는데, 그러면 에러가 발생한다.  
``` dart
TableCalendar(
    locale: 'ko-KR',
);
```

locale을 사용하기 위해선, intl이라는 패키지를 설치 해야한다.
intl은 i18n, 국제화를 위한 패키지라고 한다.
> flutter pub add intl

``` dart
import 'package:intl/date_symbol_data_local.dart';
```

해당 패키지를 import하면 locale 설정이 잘 되는것을 확인 할 수 있다.

#### 달력 형태 변경하기
table_calendar에는 1주, 2주 한달 세가지 종류의 달력이 제공되는데, 기본 설정은 한 달로 되어있다.  
CalendarFormat라는 enum타입을 제공해서 이 값으로 달력의 형태를 변경 할 수 있다.

``` dart
TableCalendar(
  firstDay: DateTime.utc(2010, 10, 16),
  lastDay: DateTime.utc(2030, 3, 14),
  focusedDay: DateTime.now(),

  calendarFormat: CalendarFormat.twoWeeks,
);
```  
이렇게 하면 2주가 출력되는 달력을 얻을 수 있다.

#### 달력 형태 버튼 눌러서 변경하기

달력을 출력 해보면 상단에 달력의 형태를 변경 할 수 있을 것 같은 버튼이 있는데, 따로 설정을 해줘야 작동한다.

``` dart
CalendarFormat _calendarFormat = CalendarFormat.month;
```

이렇게 출력할 달력의 종류를 변수로 만들어서 초기화 해주고,

``` dart
TableCalendar(
  firstDay: DateTime.utc(2010, 10, 16),
  lastDay: DateTime.utc(2030, 3, 14),
  focusedDay: DateTime.now(),

  calendarFormat: _calendarFormat,
  availableCalendarFormats: const {
    CalendarFormat.month: '한달',
    CalendarFormat.twoWeeks: '2주',
  },
  
  onFormatChanged: (format) {
    setState(() {
      _calendarFormat = format;
    });
  },
);
```

calendarFormat 에 해당 변수를,  
availableCalendarFormats에 사용할 CalendarFormat들을 Map형태로 넣어준다.  
그리고 onFormatChanged에서 setState선언 후 받은 format을 설정해주면 끝!

![change_format](/images/flutter/table_calendar_convert_format.gif)

formatAnimationCurve와 formatAnimationDuration 등을 활용하면 format 변경 시에 애니메이션을 수정 할 수도 있다.

``` dart
TableCalendar(
  formatAnimationCurve: Curves.easeInOutCirc,
  formatAnimationDuration: Duration(milliseconds: 300),
);
```