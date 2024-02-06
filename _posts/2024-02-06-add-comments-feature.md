---
layout: post
title: 블로그 댓글 기능 추가하기
#add comments feature
date: 2024-02-06 15:30 +0900
author: woongyee
description:
image:
category:
- blogging
tags:
- giscus
published: true
sitemap: false
---
## 라이브러리 선택하기
Chripy 테마는 기본적으로 disqus, utterances, giscus 3가지를 지원한다. 간단하게 비교해보자.

#### Disqus  
- 광고가 표시될 수 있다.   
- disqus 서버에 댓글이 저장된다.
- 페이지 로딩 속도가 느려질 수 있다.

#### Utterances
- Github Issue로 댓글을 관리한다.
- 광고 없이 사용할 수 있다. 

#### Giscus
- Github Discussions로 댓글을 관리한다.
- 광고 없이 사용할 수 있다.
- utterances보다 더 많은 기능, 테마를 가지고 있다.

댓글 때문에 광고가 표시되거나 로딩 속도가 느려지는 것은 용납할 수가 없기에 Github로 관리하는 방식을 사용하려한다. 현 시점에서 Giscus가 Utterances보다 더 많은 기능과 테마를 제공하기에 선택하였다.

## Giscus로 댓글 연동하기

### Giscus App 설치
[giscus](https://github.com/apps/giscus) 여기에 접속하여 설치하자.   
필자는 블로그 repository를 찾아서 거기에만 giscus를 설치해주었다.

### Discussion 활성화
블로그 repository의 settings - general - features에서 discussion을 활성화해주자.  
상세한 내용은 [여기](https://jojoldu.tistory.com/704)를 참고하자.

### Giscus 설정하기
[Giscus App](https://giscus.app/)에서 임베딩 시킬 수 있는 JS 코드를 생성할 수 있다.  
하지만 필자는 Chripy 테마를 사용하고 있고 _config.yml에서 기본적인 설정을 할 수 있다.

#### _config.yml로 기본 설정하기
_config.yml의 comments에 active : giscus로 설정한 후 giscus부분에 repo, repo_id 등 위의 사이트에서 생성한 JS코드를 참고하여 작성하자. 

#### 추가 설정하기
추가적인 설정을 하기위해서는 _includes/comments/giscus.html을 수정하면 된다.   
자세한 내용은 [여기](https://da-in.github.io/posts/Blog-Comments)를 참고하자. 

## 의문점
#### Reactions만 위치 옮기기가 가능할까?  
html에서 Reactions만 위치를 옮길 수는 없다.
Giscus 옵션 중에 reactions 끄고 켜는 설정은 있다. 



## 참고
[Utterances에서 Giscus로 마이그레이션하기](https://jojoldu.tistory.com/704)

[[Gihub Blog] 댓글 Giscus 설정](https://jihwan98.github.io/posts/giscus-%EC%84%A4%EC%A0%95/)


[[Blog] Git Blog에 댓글 기능 추가하기 (Jekyll, Chirpy, 400, 404 Error 정리)](https://da-in.github.io/posts/Blog-Comments/)  