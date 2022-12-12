---
title: "[Setting] Github 소스트리 유효한 소스 경로/url 이 아닙니다"
date: 2022-12-12 23:30:00 +0900
categories: [Setting, Github]
tags: [Setting, Github, SourceTree, 소스트리]
---

소스트리에서 Clone 받을 때, 프로젝트 url을 입력하면 **"유효한 소스 경로/url이 아닙니다"**라는 메시지가 떴다.

이는 url이나 유저의 계정 정보를 제대로 인증하지 못했을 때 발생한다.

Github는 이제 비밀번호가 아닌 토큰방식으로 인증을 하기 때문에, 토큰을 만들어 넣어주도록 하자.

Github의 설정/Developer settings에 들어간다.

<img src="/assets/img/post/setting_github_token01.png"/>

"Generate new token (classic)"을 누르고 아래와 같이 설정한 후, 토큰 생성하기

<img src="/assets/img/post/setting_github_token02.png"/>
<img src="/assets/img/post/setting_github_token03.png"/>
<img src="/assets/img/post/setting_github_token04.png"/>
<img src="/assets/img/post/setting_github_token05.png"/>

sourcetree로 가서, Remote > github계정 오른쪽 클릭 > [계정 편집]

인증은 Basic, 비밀번호 새로고침을 눌러서 받은 토큰을 붙여넣기하고 [확인]을 누른다.

이제 다시 clone을 받으면 잘 받아오는 것을 확인할 수 있다.

<img src="/assets/img/post/setting_github_token06.png"/>
