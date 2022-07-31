# 😡 불편함

Spring 내에서 컨트롤러를 만들고 이를 활용해야 한다면, 어떻게 할까? 

엑셀로 정의하는 멋진 방법이 있겠지만, 게으른 개발자들이 이를 매번 업데이트하기란 여간 어려운 일이 아닐 수 없을 것이다.

또한 버전별로 이를 나누어 엑셀 목록을 유지하는 것도 어려울 것이다.
> 물론 깃을 이용해 프로젝트파일과 동일하게 형상관리를 할 수는 있겠지만, 컨트롤러가 추가되거나, 바뀔 때마다 이를 추가해야 하는 번거로움이 있는 것은 피할 수 없다.

이런게 있으면 좋지 않을까? 내가 추가하거나, 수정하거나, 삭제한 컨트롤러의 명세를 저절로 가독성 좋은 페이지로 만들어 주는 도구 말이다.

그렇다 오늘 소개할 이 멋진 친구는 바로, OpenAPI Specfication `Swagger`이다.

# Swagger
![image](https://user-images.githubusercontent.com/59782504/182016157-91b73c08-2bf9-412c-b2a2-6a636aebdfd7.png)

Swagger은 앞서 설명한 불편함에서 비롯되어 탄생한 도구이다.

`Swagger`를 사용하면 `Query Parameter`, `Path Variable`, `Request/Response Body` 등, 우리가 불편하게 명세해야 했던 API 내역을 보기 좋게 웹 페이지의 형식으로 나타낼 수 있다.

이런 도구적인 특성은 여러가지 면에서 장점이 있다.

1. 백엔드 개발자로 하여금, 해당 서비스의 개략적인 내용을 파악하게 돕는다.
2. Open API, B2B 등 여러 비즈니스 환경에서 API 문서를 관리하지 않아도, 변경된 사항들을 그 때 그 떄 반영하여 확인할 수 있다.
3. IOS, Android, Frontend 개발자들이 해당 내용을 토대로 구체적인 작업을 하도록 돕는다.
4. 간단한 테스트 도구를 제공하기 떄문에 `postman`, `Talend API Tester` 등 기타 API 테스터를 사용하지 않고, 실제 요청, 응답에 대한 테스트를 진행할 수 있다.


# 적용
실제 적용하는 것은 굉장히 쉽고 어렵지 않다.

이전에는 springfox-starter라는 의존성을 등록함으로써 Swagger를 추가하였으나, 최근에는 Spring Docs를 활용하고 있다.

결과는 동일하나, Spring Docs을 활용하는 것이 훨신 직관적이며 간단하다.

## Dependency

먼저 `build.gradle`파일에 아래와 같이 의존성을 추가한다.
```gradle
..
dependencies {
    ..
    implementation 'org.springdoc:springdoc-openapi-ui:1.6.9'
    ..
}
..
```

`applications.yml` 파일을 다음과 같이 설정한다.

```yaml
springdoc:
    default-consumes-media-type: application/json
    default-produces-media-type: application/json
    swagger-ui:
        path: /swagger-ui.html
        disable-swagger-default-url: true
        display-query-params-without-oauth2: true
```

이것만 해도 설정은 끝이나 Swagger에서는 더욱 많은 옵션을 제공한다.  
