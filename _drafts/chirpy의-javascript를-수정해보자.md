---
layout: post
title: Chirpy의 Javascript를 수정해보자
description: 
image: 
category: 
tags: 
---

### 도대체 어디서 자바스크립트를 수정할 수 있을까?
난 목차가 스크롤할때마다 바뀌는게 마음에 안들었다. 그걸 바꾸고 싶다.  접히지말고 항상 고정된 목차가 보이도록.

그런데 도대체 어디에 자바스크립트 코드가 들어가 있는가? 

_site 폴더 안에 js 파일들이 있는데 어디서 빌드되어서 들어가는거지..? 내가 커스텀 할 수는 없는건가? 

assets 안에 js 파일을 넣어서 커스텀하는건가? 그렇다면 그 js 파일은 어디에서 호출되는 것인가?  

공식 레포지토리에 가면 _javascript 폴더가 따로 있어서 그걸 가져와서 커스텀 해봤는데 전혀 반응이 없다. 애초에 그 폴더가 없어도 돌아가니까..

