---
title: MariaDB root계정 정보 변경하기
author: yerin
date: 2022-11-27 23:40:00 +0900
categories: [MariaDB]
tags: [server, docker, mariadb]
---

## 왜 변경해야 하는가?

DB보안을 위해서 해야하는 것이다. default로 설정된 값 혹은 흔히 사용하는 값은 탈취될 위험이 크다.
DB의 root계정명 뿐만 아니라 DB포트를 3306을 권장하지 않는 것도 같은 맥락이다.

<br>

## root계정 사용자명 변경하기

1. mariadb container 진입

```java
  docker exec -it mariadb /bin/bash
```

- 여기서 mariadb는 컨테이너명
- 초기 비밀번호를 설정한 적이 없다면, 안 적어도 되는 것 같다.

<br>

2. username 변경하기

```java
  mysql -uroot -p초기_비밀번호
  use mysql
  select Host,User,Password from user;
  rename user 'root'@'localhost' to 'test'@'localhost';
```

- 위의 예시에서는 root 계정을 test로 바꾸고 있다.
