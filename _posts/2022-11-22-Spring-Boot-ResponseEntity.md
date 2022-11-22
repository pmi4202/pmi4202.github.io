---
title: Spring Boot ResponseEntity
author: yerin
date: 2022-11-22 16:34:00 +0900
categories: [SpringBoot]
tags: [spring, SpringBoot, ResponseEntity, restapi]
---

# ResponseEntity란?

- ***HttpEntity**를 상속 받아서, response용으로 만든 클래스
- 결과 데이터와 HTTP 상태 코드를 이 클래스에 담아 보내면, HTTP 아키텍처 형식에 맞추어 보낸다.
- @ResponseEntity : 객체와 status를 함께 보내줄 수 있다.
    - @ResponseBody : 객체를 넣으면, 알맞은 header, body, status를 만들어준다.
    - @ResponseStatus(HttpStatus.OK) : 직접 상태를 만들어 줄 수 있다.

***HttpEntity**

- HTTP요청 또는 응답을 모두 처리하는 클래스
- HttpHeader와 HttpBody를 포함하고 있다.
- HttpEntity클래스를 상속 받아 구현한 클래스가 RequestEntity, ResponseEntity로, 응답 전용& 요청 전용으로 더 정교하게 구현된 클래스를 사용할 수 있다.

```java
public class HttpEntity<T> {
    public static final HttpEntity<?> EMPTY = new HttpEntity();
    private final HttpHeaders headers;
    private final T body;
    ...
}
```

<br>
# ResponseEntity 구조

총 3가지 속성을 설정할 수 있고, 구체적으로는 공식문서의 생성자를 참고해서 작성하면 된다.

- HttpStatus
- HttpHeaders
- HttpBody

*[spring 참고문서]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/http/ResponseEntity.html
<img src="./assets/img/post/springboot_response_entity_docs.jpg" width="200" height="200"/>