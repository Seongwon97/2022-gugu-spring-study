# Chapter 5 - 컴포넌트 스캔

### 컴포넌트 스캔

- : 스프링이 직접 클래스를 검색해 빈으로 등록해주는 기능
- `@Component`로 등록 가능
    - 어노테이션에 값을 주면 빈으로 등록 시 사용할 이름 지정 가능
    - 값이 없을 경우 클래스 이름의 첫 글자를 소문자로 바꾼 이름으로 지정
- 기본 스캔 대상
    - `@Component`
    - `@Controller`
    - `@Service`
    - `@Repository`
    - `@Configuration`

> 💥 p137 ~ p138  
> `@Aspect` 어노테이션도 컴포넌트 스캔 대상에 포함되는데 실제로는 동작하지 않는다.  
> 이 부분에 대해서는 별도로 공부해보겠다.

### @ComponentScan

- `basePackages`: 스캔 대상 패키지 목록 지정 (하위 패키지까지 스캔 대상임)
- `excludeFilters`: 스캔 대상에서 제외하기

```java

@Configuration
@ComponentScan(basePackages = {"wooteco"},
        excludeFilters = @Filter(type = FilterType.ASPECTJ))
public class AppContext {

    // ...
}
```

> Spring Boot를 이용하는 프로젝트를 보면 `@ComponentScan` 사용 안하는데 자동으로 빈 등록이 된다.  
> main 메서드가 포함되어있는 클래스를 보니 `@SpringBootApplicaion`이 붙어있었다.  
> `@SpringBootApplication`에 `@ComponentScan`이 포함되어 있다.

### 컴포넌트 스캔 충돌 처리

1. 빈 이름 충돌
    - 컴포넌트 스캔 과정에서 발견 가능
    - 👉 둘 중 하나를 명시적으로 빈 이름 지정
2. 수동 등록한 빈과 충돌
    - 수동 등록 빈이 우선 순위 (2.1부터는 Exception 발생)
    - 👉 필요 시 자동 주입하는 코드에서 `@Qualifier`를 이용해 알맞은 빈 선택
