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
published: true
sitemap: false
---

코틀린 Flow에 대해 이해하려면 먼저 Reactive Programming(반응형 프로그래밍)을 알고 넘어가야한다.

## Reactive Programming 
> 데이터 스트림과 변경사항 전파가 핵심인 선언형 프로그래밍 패러다임

데이터의 변화가 발생하면 이벤트가 생성되고, 이 변경된 값을 데이터 스트림을 통해 전달한다. 
이렇게 비동기적으로 전달된 데이터는 선언적으로 작성된 코드에 따라 처리된다.

#### 선언형 프로그래밍
> '어떻게 해야 하는가'보다는 '무엇을 원하는가'에 초점을 맞춘 프로그래밍 방식


예를 들어, SQL 쿼리를 작성하는 경우를 생각해보자. 
우리는 DB에서 데이터를 가져오는 과정에 대한 코드가 아니라 원하는 결과에 대한 코드를 작성한다. 
또, HTML로 웹 페이지를 만드는 경우에는 HTML 태그를 통해 보여질 요소들에 대한 코드를 작성하고 브라우저가 이를 해석해 웹페이지를 렌더링한다.

구체적인 예제는 이 [블로그](https://yozm.wishket.com/magazine/detail/2083/)를 참고하자.

## 비동기 데이터 스트림
반응형 프로그래밍에서는 비동기 데이터 스트림이 중요한데, 코틀린에선 Channel과 Flow를 통해 이를 쉽게 생성하고 관리한다. 
두 개념에 대해 설명하기 전에 먼저 Producer-Consumer 패턴을 알아보자.

## Producer-Consumer 패턴
멀티스레딩 디자인 패턴 중 하나로 동시성을 다루는 상황에서 자주 사용된다. 
> Producer(생산자) : 데이터를 생산하고 보내는 역할  

> Consumer(소비자) : 프로듀서가 생산한 데이터를 받아서 소비하는 역할

이 패턴은 한 곳에서 생산하고 한 곳에서 소비하는 1:1 관계를 가질 수도 있고, 1:n, n:1, n:m 관계를 가질 수도 있다.

## Channel vs Flow
Channel과 Flow는 기본적으로 Producer-Consumer 패턴을 따르고 있다.  
그렇다면 둘의 차이는 무엇인가?
Channel은 Hot Stream, Flow는 Cold Stream이다. 

### Hot Stream 와 Cold Stream
이 둘의 차이를 흔히 Radio와 CD Player로 비유를 들어 설명하곤 한다.  
필자는 조금 새로운 비유를 생각해보았다. 우리가 일본에 온천여행을 갔다고 해보자.   

Hot Stream은 공중목욕탕, Cold Stream은 료칸의 개인온천이다.  
목욕탕을 운영하는 사람이 Producer, 목욕을 하는 우리는 Consumer이다.
공중목욕탕은 개업하면 손님이 없더라도 목욕탕에 계속 물을 공급해야하며, 한 번에 많은 사람들이 같이 목욕을 할 수도 있다. 하지만, 료칸의 개인온천은 개업 이후 예약한 손님이 있는 경우에 물을 공급하고, 각 온천은 해당 손님만을 위해 독립적으로 운영한다. 

> Hot Stream  
> - Producer가 데이터를 생산하기 시작한 이후부터 모든 Consumer에게 같은 데이터를 발행한다.
> - Consumer는 언제든지 들어와서 데이터를 소비할 수 있다.  
> 즉, Consumer가 들어오는 시점에 따라 소비하는 데이터가 달라진다.

> Cold Stream  
> - Producer가 데이터를 생산한 이후 Consumer가 소비하기 시작하면 데이터를 발행한다.
> - Consumer가 들어올 때마다 데이터를 처음부터 발행한다.  
> 즉, 다른 Consumer가 얼만큼 소비했는지와 관련없이 독립적으로 데이터를 소비할 수 있다.

### 간단한 사용 방법
Channel의 send, Flow의 emit 등의 방법으로 데이터를 생산하고 Channel의 consumeEach, Flow의 collect 등의 방법으로 데이터를 소비한다.

```kotlin
val channel = Channel<Int>()
// Producer
GlobalScope.launch {
    for (i in 1..5) {
        channel.send(i * i)
    }
    channel.close()
}
// Consumer
GlobalScope.launch {
    for (i in channel) {
        println(i)
    }
}
```

```kotlin 
// Producer
val flow = flow {
    for (i in 1..5) {
        emit(i)
    }
}
// Consumer
GlobalScope.launch {
    flow.collect { value ->
        println(value)
    }
}
```
---

Flow의 기본이 되는 개념들을 Channel과 함께 알아보았다. Flow를 사용, 활용하는 방법 등은 이미 많이 다루고 있으니 더 알아보기의 링크를 참고하자. 

## 더 알아보기
- [Flow 기본 사용법](https://two22.tistory.com/16)
- [Flow 처리 - Intermediate Operaters](https://two22.tistory.com/17)
- [Flow 예외 처리](https://two22.tistory.com/19)
- [안드로이드 개발에서 Flow 기본 활용](https://heegs.tistory.com/89)
- Concurrent Flows - 버퍼 처리, [backpressure](https://aroundck.tistory.com/7992)
- [StateFlow](https://kotlinworld.com/232?category=973477), [SharedFlow](https://everyday-develop-myself.tistory.com/306)
- [Channel 타입, 버퍼 오버플로 전략 등](https://huisam.tistory.com/entry/coroutine-channel)

## 참고
[Flow 공식 문서](https://kotlinlang.org/docs/flow.html)
 / [Flow 인터페이스 공식 문서](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-flow/)
 / [Channel 인터페이스 공식 문서](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.channels/-channel/)

[[Coroutine Flow] 1.Flow란 무엇인가](https://kotlinworld.com/175) - Flow에 대한 개념 잡기 좋은 글

[Flow와 Channel, Cold Stream과 Hot Stream](https://medium.com/@apfhdznzl/flow%EC%99%80-channel-cold-stream%EA%B3%BC-hot-stream-c42c64cf4996) - CD Player와 Radio 비유

[프로그래밍 패러다임과 반응형 프로그래밍 그리고 Rx](https://yozm.wishket.com/magazine/detail/1334/)
- 프론트엔드 개발자의 글이지만 반응형 프로그래밍에 대해 자세히 설명해둠.