---
title: "TypeScript 사용해보기"
categories:
  - study
tags:
  - TypeScript
toc: true
toc_sticky: true
---

![table_calendar](/images/logo/typescript_logo.png)

## 🤔 TypeScript?
기존 자바스크립트는 정적 타이핑 언어가 아니기 때문에, 유지보수적인 면에서 많은 어려운 부분이 있었다.

그래서 마이크로 소프트에서 자바스크립트에 정적 타입을 명시할 수 있는 새로운 언어를 만들었는데, 그게 바로 타입 스크립트이다.

정적 타이핑 언어이기 때문에, IDE상에서 에러를 잡아내기 쉽고, 자바 스크립트 특성 상 변수 타입의 자유도?가 굉장히 높기 때문에 개발자가 예상하기 어려운 문제들을 빠르게 찾아내기 쉽다는 장점도 있다.

예를 들어,  
``` js
function add(a, b) {
  return a + b;
}
```  
라는 두 숫자를 더하는 자바 스크립트 함수가 있을 때,  
a에 10, b에 20 -> 30이라는 결과가 나올 수도 있지만

a에 "10", b에 "20"이 들어간다면 1020이라는 결과가 나온다.  
이렇게 개발자가 미처 처리하지 못한 여러 타이핑 관련 에러를 타입 스크립트는 쉽게 찾아낼 수 있다.

``` ts
function add(a:number, b:number): number {
  return a + b;
}
```

이렇게, 타입 스크립트에선 각 매개변수와 함수의 반환값도 정적 타입을 명시할 수 있기 때문에, 개발자가 add()함수에 string값을 넣으려고 할 때 에러를 발생할 것이다.

## 🐣TypeScript 설치하기
타입 스크립트를 설치 하려면 nodejs가 설치되어 있어야 한다.  
node의 패키지 매니저인 npm을 사용하여 타입 스크립트를 설치 할 수 있다.

타입 스크립트는 결국 자바스크립트로 컴파일을 해야하기 때문에, 타입스크립트를 자바 스크립트로 컴파일 해주는 패키지가 필요하다.

> npm install typescript  

만약 typescript를 전역적으로 사용 하고싶다면 global 옵션을 주면 된다.  
> npm install -g typescript

설치가 끝나면 tsc --version 명령어로 잘 설치가 되었는지 확인한다.  
> tsc --version  


![table_calendar](/images/tsc_version.png)

이제 설치가 잘 되었으니, 타입 스크립트를 사용할 수 있다! 😆