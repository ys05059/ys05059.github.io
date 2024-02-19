---
layout: post
title: Chirpy 테마 업데이트
date: 2024-02-19 18:40 +0900
author: woongyee
description: 
image:
category:
- blogging
tags:
- jekyll
published: true
sitemap: false
---
## 개요
Chirpy 테마를 최신 버전으로 업데이트하며 발생했던 오류와 해결법을 공유하고자 한다.

[Getting Started](https://chirpy.cotes.page/posts/getting-started/) 공식 문서에서는 두 가지 방법으로 Chirpy 테마를 사용해 블로그를 만드는 방법을 알려준다. 
필자는 chirpy-starter 방식으로 블로그를 만들었다. 선택한 이유는 하나하나 커스텀하는 것보다 새로운 버전을 쉽게 업데이트해서 사용하고 싶었기 때문이다.

이 방식을 사용하면 새로운 버전이 릴리즈 될 때마다 Gemfile에서 버전을 올려줌으로써 쉽게 버전을 업데이트할 수 있다. 자세한 내용은
[공식 Upgrade Guide](https://github.com/cotes2020/jekyll-theme-chirpy/wiki/Upgrade-Guide)를 참고하자.


하지만 오류가 계속 발생했고 도저히 이유를 알 수 없었기에 삽질을 계속했다.
![](/assets/img/chirpy-theme-update/error.png){: width="400" } _처음 발생한 오류_

2주 만에 블로그 포스트를 올렸는데 [Git Actions](https://github.com/ys05059/ys05059.github.io/actions/runs/7917101925/job/21612448974)에서 위와 같은 오류가 발생했다.

_site 폴더는 .gitignore에 포함되어 있어 github에 올라가지도 않았고 수정한 부분도 없었다. jekyll이 빌드한 파일이기 때문이다._config.yml에서 건드린 것도 없는데 왜 빌드한 내용이 달라진건지 알 수 없었다. 그리고 app.js가 존재하지 않는다는데 그게 무엇인지 전혀 감이 오지 않았다.

### app.js가 뭐지?
결론만 말하자면, 웹앱으로 만들기 위한 기능인 PWA 때문이다. PWA에 대한 설명은 [여기](https://yozm.wishket.com/magazine/detail/1969/)를 참고하자.

app.js가 기존에는 있었는데 갑자기 없다길래 어디에서 사용되는지 찾아보았다. _includes/js-selector.html에서 해당 코드를 사용하고 있었다.

## 무엇이 문제였는가?
5일전 [6.5.0 버전이 릴리즈](https://github.com/cotes2020/jekyll-theme-chirpy/releases/tag/v6.5.0) 되면서 PWA 캐싱 관련 기능이 추가되었다. 이로 인해 js-selector.html 코드가 변경되었던 것이다. 
![](/assets/img/chirpy-theme-update/pwa-cache-commit.png)
_[커밋](https://github.com/cotes2020/jekyll-theme-chirpy/commit/1127c43823aac4db7fd80d5bb706ae7b1e129dc6#diff-175dfa201468748f22e1b760fc4ab51525c0d70cfa6f4356ad793db8401d65ce) 참고_


필자는 chirpy-starter로 시작했지만 따로 _includes 폴더를 로컬에 만들어두었었다. 그렇기에 chirpy-theme를 적용하는 과정에서 로컬에 있는 _includes 폴더를 우선으로 빌드한다. 따라서 includes에 대해서는 이전 버전의 chirpy-theme가 적용되고 있었다.

## 해결하기
1. Gemfile 안에 있는 jekyll-theme-chirpy 버전 올리기
2. gem으로최신 버전의 jekyll-theme-chirpy 업데이트 하기
```console
bundle update jekyll-theme-chirpy
```
아래의 코드를 통해 실제로 적용될 파일들의 위치를 알 수 있다.
```console
bundle info --path jekyll-theme-chirpy
```
3. 로컬에 있는 _includes 폴더를 삭제하기
4. _config.yml에 업데이트 내용 적용하기   
    [update critical file](https://github.com/cotes2020/chirpy-starter/commit/b160f258a0fc8150e5113f37b001ecb8aeb7c309)를 참고해 _config.yml 파일의 내용을 직접 수정했다.


## 그 외의 문제들
#### 이미지 경로 에러
이번 업데이트를 진행하며 갑자기 이미지를 불러오지 못해 오류가 발생했다. path에 한글이 섞여있어 발생한 문제였다.
![](/assets/img/chirpy-theme-update/image-path-error.png)
_해당 [workflow run](https://github.com/ys05059/ys05059.github.io/actions/runs/7957215342/job/21719482122) 참고_


#### sass-embedded 관련 에러
이 오류로 인해 app.js가 생기지 않는가 했는데 관련 없었다. 아직 무엇이 문제인지, 어떻게 해결하는지 찾지 못했다. 혹시 아는 분이 있으시다면 댓글로 알려주시면 감사하겠습니다.
![](/assets/img/chirpy-theme-update/sass-error.png)


## 소감
해당 업데이트 부분을 따로 추가해서 사용할 수 있었지만 앞으로 계속 유지보수 해야하기에 커스텀을 최소화하고자 하였다. 결론적으로
해결하는 방법은 정말 간단했지만 원리를 이해하고 문제 부분을 찾아내는 과정은 쉽지 않았다. 나름 재미있었지만 관련 자료가 거의 없었기에 답답했다. 누군가 이 글을 보고 도움을 얻었으면 한다.

## 참고

> 원리를 이해하는데 도움이 되었던 블로그  
> [gem 기반으로 jekyll 블로그 만들기(chirpy 테마, windows)](https://a3magic3pocket.github.io/posts/jekyll-theme-chirpy-with-gem/)  
