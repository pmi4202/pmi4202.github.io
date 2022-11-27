---
title: MariaDB Docker로 설치하고 실행하기
author: yerin
date: 2022-11-24 23:50:00 +0900
categories: [MariaDB]
tags: [server, docker, mariadb]
---

## 1. docker image pull해오기(이건 이미 있으므로 pass함)

```java
docker pull mariadb:[버전명]
```

- 버전명 미기입시 최신버전으로 다운로드
- 생성된 이미지 확인
  ```java
  docker image ls
  ```

<br>

## 2. docker run

```java
docker run --name mariadb-container -v $(pwd)/[db정보_저장할_폴더명]:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=비밀번호 -e MYSQL_DATABASE=DB이름 -d -p [외부포트]:3306 [이미지명] --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

//예시
docker run --name mariadb-container -v $(pwd)/mariadb:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mypw -e MYSQL_DATABASE=test -d -p 3310:3306 mariadb --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

- 옵션
  - —name 옵션: 컨테이너 이름 할당
  - -v 옵션: 볼륨 설정(볼륨 이름:컨테이너에 마운트되는 경로:옵션 목록(선택))
  - -e 옵션: 환경 변수 설정
  - -d 옵션: 컨테이너를 백그라운드에서 실행
  - -p 옵션: 컨테이너 포트를 호스트 포트로 접속할 수 있도록 함
  - —character-set-server, —collation-server 명령: 한글 인코딩
