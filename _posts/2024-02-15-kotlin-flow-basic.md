---
layout: post
title: 코틀린 Flow 기본 개념
date: 2024-02-15 21:13 +0900
author: woongyee
description:
image:
category:
- kotlin
- coroutines
tags:
- channel
- flow
published: false
sitemap: false
---

코틀린 Flow에 대해 이해하려면 먼저 Reactive Programming(반응형 프로그래밍)을 알고 넘어가야한다.

## Reactive Programming 
반응형 프로그래밍은 프로그래밍 패러다임 중 하나이다.
변화의 전파와 데이터의 흐름이 중요

## 비동기 데이터 스트림
코틀린에서는 Channel과 Flow를 통해 비동기 데이터 스트림을 쉽게 생성하고 관리할 수 있습니다

## Producer-Consumer 패턴
### Producer
### Consumer
프로듀서는 데이터를 생성하고, 컨슈머는 해당 데이터를 소비
 이 패턴은 1:1 관계를 가질 수도 있고, 여러 프로듀서와 여러 컨슈머를 가지는 1:n, n:1, n:m 관계를 가질 수도 있습니다.



## Flow란?

## Hot Stream 와 Cold Stream

CD Player와 Radio 비유

## Channel vs Flow


## 안드로이드 개발에서 Flow의 사용

## What's Next
- Flow 사용법
- Flow 처리 (중간 연산자)
  - Builder
  - Intermediate Operaters
  - Terminal Operator
- Concurrent Flows -> 버퍼 처리, backpressure, 
- StateFlow
- SharedFlow
- Flow Exception Handling, Cancellation


## 참고
[Flow 공식 문서](https://kotlinlang.org/docs/flow.html)
[Flow 인터페이스 공식 문서](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-flow/)

[Channel 인터페이스 공식 문서](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.channels/-channel/)

[[Coroutine Flow] 1.Flow란 무엇인가](https://kotlinworld.com/175)
- Flow에 대한 개념 잡기 좋은 글

[프로그래밍 패러다임과 반응형 프로그래밍 그리고 Rx](https://yozm.wishket.com/magazine/detail/1334/)
- 프론트엔드 개발자의 글이지만 반응형 프로그래밍에 대해 자세히 설명해둠.

[Flow와 Channel, Cold Stream과 Hot Stream](https://medium.com/@apfhdznzl/flow%EC%99%80-channel-cold-stream%EA%B3%BC-hot-stream-c42c64cf4996)
- CD Player와 Radio 비유