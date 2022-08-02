# 테스트
테스트란 프로그램의 개발에 있어서 해당 프로그램이 명세대로 구현되었는지 알아보기 위해서 실행하는 것을 의미한다.

테스트는 단위테스트, 통합테스트, 인수테스트 등 여러가지가 있으나, 해당 챕터에서는 JUnit을 알아보기 위한 것을 목표로 함으로 단위 테스트에 대한 설명으로 한정한다.

# 단위테스트?
단위 테스트는 프로그램의 여러 부분을 독립적인 단위(모듈, 메서드, 클래스 등)으로 나누어 각각 테스트하는 것을 의미한다.

단위 테스트는 개발자가 의도한 값과 메서드의 반환값, 결과 등이 같은지를 확인하는 루틴을 거치며, 만약 변경 등으로 특정 모듈이 영향을 받아 결과값이 다르게 나타난다면 해당 단위 테스트 값 역시 불일치하게 되며, 개발자에게 테스트 코드의 변경 혹은 개발 코드의 변경을 의도하게 된다.

결과적으로 위에 기술된 대로 단위테스트는 안정적인 프로그램을 구현하는데에 기여한다.

# JUnit
JUnit은 이름에서 정직하게 명시하고 있듯, Java로 구현된 프로그램에 단위 테스트를 하기 위해 작성된 프레임워크라 할 수 있다.

해당 챕터에서는 Spring Framework에서 JUnit가 어떤 방식으로 사용되는지를 중점으로 기술한다.

## 왜 쓰는가?
단위 테스트가 꼭 JUnit과 같은 도구가 필요한 것은 아니다. 

그저 함수의 결과값이 맞는지 체크하는 과정이 있다면, 그것 역시 일종의 단위테스트라고 볼 수 있다.

다만 해당 과정은 개발자에게 수많은 입출력코드, 표준화 되지 않은 포맷 등으로 인해 최악의 경우 협업 상황에서 팀원이 구현된 코드 뿐 아니라 단위 테스트에 대한 코드도 이해하게 만드는 경우가 생길 수도 있다.


이에 JUnit은 프레임워크라는 말에 알맞듯, 많은 부분이 모듈화, 표준화 되어 있어 일관적인 테스트 패턴을 만들 수 있도록 개발자에게 유도하며, 결과 값, 테스트 통계 등을 쉽게 확인할 수 있는 기능까지도 포함하고 있다. 



# 프로젝트 구조
Spring에서 특정 `@Component`, `@Controller`등의 모듈에 Test를 사용하기 위해서는 일반적으로 `src` 디렉토리를 기준으로 `test` 디렉토리와 `main` 디렉토리의 구조를 동일하게 하며 테스트 대상 클래스에 `Test`키워드를 붙여 명명한다.

예를 들어 아래와 같은 느낌으로 생성하는 것이다.

```
...
src
  |-- main
      |-- com.java.somepackage.controller
          |-- HelloWorldController
  |-- test
      |-- com.java.somepackage.controller
          |-- HelloWorldControllerTest
...
```

# `spring-boot-starter-test`
Spring에서는 `spring-boot-starter-test` 라는 의존성을 추가해줌으로써 테스트를 쉽게 할 수 있는 스타터를 제공하고 있다. 이 모듈에는 단위테스트를 위한 JUnit, Mockito 뿐 아니라 웬만한 Java계열에서 사용하는 테스트 라이브러리들이 모여있다.


## Annotations
Spring에서 테스트를 쉽게 사용할 수 있도록 `spring-boot-starter-test`에서는 위에서 설명했던 일부 어노테이션을 포함한 아래의 어노테이션을 제공한다.
* `@SpringBootTest`
* `@WebMvcTest`
* `@DataJpaTest`
* `@RestClientTest`
* `@JsonTest`

#  `@SpringBootTest` vs `@WebMvcTest`

테스트 관련된 스타터도 알아보았으니, 이제 테스트에서 자주 사용되는 두 어노테이션에 대해 알아볼 것이다.

컴포넌트 등을 만들고 테스트 준비가 되었다면 해당 테스트할 클래스에 `@WebMvcTest` 어노테이션이나, `@SpringBootTest` 어노테이션을 추가한다.

두 어노테이션 간에는 용도에서 서로간 차이가 있다.

* `@WebMvcTest`는 클래스에서 사용하는 것 중 `@Controller`, `@ControllerAdvice`, `@JsonComponent` 등 Web MVC에서 사용하는 의존성만을 가져온다.
  * 추가적으로 해당 어노테이션의 경우 `MockMvc`에 대한 설정을 저절로 하기 위해서 `@AutoConfigureMockMvc` 어노테이션을 소급하고 있다. `MockMvc`는 이후 Mock 부분에서 더욱 자세히 알아본다.
* `@SpringBootTest`는 사용자가 추가한 모든 의존성을 로드한다. `@Component`, `@Service`,  `@Repository` 등의 어노테이션을 추가한 클래스의 인스턴스를 테스트하거나, 테스트 클래스에서 사용해야 할 경우, 해당 어노테이션을 사용한다.

# `@Test`
`@Test`어노테이션은 메서드에 붙는 어노테이션으로 해당 메서드가 단위 테스트 메서드임을 알려주는 어노테이션이라 볼 수 있다. 

```java
@SpringBootTest
public HelloWorldTest {
    @Test
    @DisplayName("A+B = 3 인가")
    void AplusBequal3(){
        ...
    }
}
```

# `assertXXX`
테스트 프레임워크에서 결과값을 실제 값이랑 비교하기 위한 여러 방법론으로 assert키워드가 붙어있는 메서드들을 활용할 수 있다.
메서드에서 해당 `assertXXX` 와 같은 메서드를 호출하면, 해당메서드의 결과값이 곧 테스트의 결과값으로 되어 산출된다.

해당 메서드들은 `org.junit.jupiter.api.Assertions`에 포함되어 있으며, 필요에 따라 아래와 같은 메서드들을 통해 테스트를 수행할 수 있다.

|메서드 명|설명|
|-----|---|
|`assertTrue(bool condition)`|`condition` 값이 참인지를 검사한다.|
|`assertFalse(bool condition)`|`condition` 값이 거짓인지 검사한다.|
|`assertEquals(expected, actual)`|`actual` 값이 `expected` 값과 동일한지 검사한다.| 
|`assertArrayEqual(expected[], actual[])`|`actual` 배열과, `expected` 배열이 동일한지 검사한다.|

```java 
@WebMvcTest
class HelloWorldTest {

    @Test
    @DisplayName("1은 1과 같은지 테스트")
    void test1() {
        assertEquals(1, 1, "1은 1과 다릅니다.");
    }
}
```

# given-then-when
흔히 작성되는 테스트 코드는 권장되는 패턴이 있다.

바로 given, then, when에 따라 작성하는 것인데

* `given`은 테스트를 하기 위해 사용되는 인스턴스의 초기화, 테스트 할 값들을 명시한다.
* `when`은 `given`단계에서 주어진 인스턴스에서 메서드를 호출하는 단계로, 값을 얻어내는 단계이다.
* `then`은 `when`단계에서 얻은 값을 개발자가 의도한 값과 일치하는지 매칭하는 단계이다.

해당 패턴에 따라 작성하면 깔끔하고 알아보기 쉽게 테스트를 작성할 수 있다.

Description: [https://mangkyu.tistory.com/145](https://mangkyu.tistory.com/145)

# 테스트 메서드의 작명
테스트 메서드의 코드 자체가 알아보기 힘들어지는 경우가 필연적으로 많이 떄문에, 테스트 메서드의 이름은 최대한 서술적으로 테스트의 내용을 알아보기 쉽도록 작성하는 것이 일반적이며, 권장되고 있다.
>  언어셋에 따라, 프레임워크에 따라 띄어쓰기를 언더바로 구분하고, 한글로 메서드를 명명하기도 한다.

JUnit에서는 `@DisplayName`이라는 어노테이션을 제공하며, 해당 메서드명을 통해 화면에 노출되는 테스트의 이름을 보다 자세하고 상세하게 표현할 수 있다. (이모지의 활용 등)


# Mock
테스트를 할 떄 테스트하기 애매한 객체들이 있다. 
대표적인 예가 특히 API나 DB 관련된 부분인데, 만약 API 호출에 따라 금액이 산정되는 번역 API 같은 경우 테스트에 활용하는 것은 개발자에게 부담이 될 수 있다.

DB의 경우 특정 메서드가 조회하거나 가져오는 시간이 굉장히 오래 걸리는 경우, 시간적으로 이를 테스트하는 것을 기다리기에 부담스러울 수 있을 것이다.

이 떄 테스트에서는 테스트하기 애매하지만, 정해진 값, 즉 개발자가 의도한 결과값을 담는 Mock(가짜, 모의 객체라고도 한다)객체를 활용할 수 있다.

또한 위에 설명한 것처럼 기존 메서드가 있음에도 이를 호출하지 않고, 대신 호출하게 되는 메서드를 Stub라고 한다. 

## Mockito
실제 프로젝트 시 단위 테스트를 적용하기 위해 Mock, Stub 객체를 만들어 사용하는 것은 매우 번거로울 것이다. 때문에 Java 진영에서는 Mockito라는 테스트 프레임워크를 통해 편리하게 Mock객체와 Stub객체를 작성할 수 있도록 돕는다.

> Description: [https://gocheat.github.io/spring/spring_test-1/](https://gocheat.github.io/spring/spring_test-1/)

# `MockMvc`
Spring Test의 강력한 장점 중 하나는 Spring을 구동하지 않아도, 사용할 수 있다는 점이다.

하지만 Controller를 테스트한다고 가정하면 어떻게 테스트 될 지 의문이다.

왜냐하면 널리 알려진 것처럼, Controller는 요청(`request`)이 있어야 응답(`response`)를 하기 때문이다. 

이런 문제를 해결하기 위해 `MockMvc`라는 객체를 사용한다. 이는 내부에 구현된 컨트롤러 메서드를 읽어서, 실행한 것처럼 응답을 하게 할 수 있다.


```java
package com.example.springtoy.controller;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@WebMvcTest // Controller를 테스트 하기 떄문에 해당 어노테이션을 붙인다
class HelloWorldTest {

    @Test // 단위테스트라면 붙인다.
    @DisplayName("/hello/world로 요청을 보냈을 때 "Hello World"라고 잘 반환하는지 테스트")
    void test1(@Autowired MockMvc mvc /* 파라미터에 의존성을 주입한다. */) throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/hello/world")) // 만약 /hello/world로 요청을 보낸다면
                .andExpect(status().isOk()) // status는 200으로 표현되는가?
                .andExpect(content().string("Hello World")); // 실제 내려오는 Response Body에는 문자열 "Hello World"가 내려오는가?
    }
}
```

이는 개발자가 각 용도에 맞게 사용하면 된다.




# Reference
* https://blog.neonkid.xyz/218
* [MangKyu's Diary - JUnit과 Mockito 기반의 Spring 단위 테스트 코드 작성법 (2/3)](https://mangkyu.tistory.com/144)
* [MangKyu's Diary - JUnit과 Mockito 기반의 Spring 단위 테스트 코드 작성법 (3/3)](https://mangkyu.tistory.com/145)
