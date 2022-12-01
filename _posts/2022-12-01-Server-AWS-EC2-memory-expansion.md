---
title: "[Server] AWS EC2 스왑 활용해서 메모리 영역 확장하기"
date: 2022-12-01 14:40:00 +0900
categories: [Server]
tags: [Server, AWS, EC2, memory, swap]
---
*메모리 상태 확인

```java
free
```

## 왜 메모리를 확장해야하는가?

---

- EC2 프리티어용 t2.micro 램은 1GB밖에 안된다.
- Spring boot를 gradle build하는 순간 서버가 폭발해버릴 것이다.
- 스왑파일을 만들어 메모리영역을 늘려보자

## Swap이란?

---

디스크의 일부를 메모리처럼 사용하는 것! 즉, RAM이 부족하기 때문에, HDD의 일부를 RAM처럼 사용하는 것이다.

**스왑 크기 계산**

| 물리적 RAM의 양 | 권장 스왑 공간 |
| --- | --- |
| RAM 2GB 이하 | RAM 용량의 2배(최소 32MB) |
| RAM 2GB 초과, 32GB 미만 | 4GB + (RAM - 2GB) |
| RAM 32GB 이상 | RAM 용량의 1배 |

참고 : 스왑 공간은 절대 32MB 미만이 되지 않아야 한다.

**EC2의 free tier**에서는 RAM 1GB이므로, 스왑은 RAM의 2배인 **2GB**로 잡자

## Swap 활용하기

---

1. Swap 메모리 할당
    
    ```java
    sudo dd if=/dev/zero of=/swapfile bs=128M count=16
    ```
    
    - 128MB씩 16개의 공간을 만든다. = 2GB정도 됨

1. 스왑 파일에 대한 읽기 및 쓰기 권한을 업데이트
    
    ```java
    sudo chmod 600 /swapfile
    ```
    
2. Linux 스왑 영역을 설정
    
    ```java
    //Linux 스왑 영역을 설정
    sudo mkswap /swapfile
    //swap 공간에 스왑 파일을 추가하여 스왑 파일을 즉시 사용할 수 있도록 한다.
    sudo swapon /swapfile
    //설정 확인
    sudo swapon -s
    ```
    
3. 스왑 파일 활성화
    파일을 열고

    ```java
    sudo vi /etc/fstab
    ```
    
    파일 끝에 다음 줄을 추가하고 저장한다.
    
    ```java
    /swapfile swap swap default 0 0
    ```
    

## 결과

---

<img src="/assets/img/post/aws_ec2_memory_expansion_result.png"/>
