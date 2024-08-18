---
layout: single
title: "security 설정 요약"
typora-root-url: ../
---





### Security 초기화 과정 요약



HttpSecurityConfigration에서 HttpSecurity()를 통해 HttpSecurity 객체를 초기화하고 생성.

(WebSecurityConfigration 설정 과정 중간 포함)

SpringbootWebSecurityConfigration의 defaultSecurityFilterChain(HttpSecurity http)에 인자로 전달.

defaultSecurityFilterChain 메서드는 httpSecurity의 추가 보안 설정을 구성하고 build()를 실행.

build()를 실행하면 httpSecurity가 가지고 있는 configurer들의 init()과 configure()를 호출하게 되고 필터들이 생성되어 httpSecurity에 추가됨.

그 후  build() 안에 포함된 performBuild()가 실행되며 DefaultSecurityFilterChain를 반환함.





===>  추가 내용



### Security 초기화 과정 요약

1. **`HttpSecurity` 초기화**
   - `HttpSecurityConfiguration`에서 `HttpSecurity` 객체를 초기화한다.
   - `HttpSecurity`는 웹 애플리케이션의 보안을 설정하는 데 필요한 다양한 설정을 관리한다.
2. **`defaultSecurityFilterChain` 메서드**
   - `SpringBootWebSecurityConfiguration`의 `defaultSecurityFilterChain(HttpSecurity http)` 메서드가 `HttpSecurity` 객체를 인자로 전달받음
   - 이 메서드는 `HttpSecurity`의 기본 보안 설정을 구성하고, `build()` 메서드를 호출하여 최종 `SecurityFilterChain` 객체를 생성한다.
3. **`build()` 메서드**
   - `build()` 메서드는 `HttpSecurity`에 설정된 `Configurer`들을 사용하여 `SecurityFilterChain`을 구성.
   - 이 과정에서 HttpSecurity는 내부적으로 설정된 Configurer들의 init()과 configure() 메서드를 호출하여 초기화한다.
     - `init()`: `Configurer`의 초기화 작업을 수행
     - `configure()`: `HttpSecurity`에 보안 설정을 적용
4. **`Configurer`의 역할**
   - `Configurer`는 `HttpSecurity`의 특정 측면을 설정하는 데 사용된다. 예를 들면 인증, 권한 부여, 세션 관리 등.
   - `HttpSecurity`는 여러 `Configurer`를 내부적으로 관리하며, `configure()` 메서드를 통해 이들을 사용하여 최종 보안 필터 체인을 구성.
5. **보안 필터 체인 생성**
   - `build()` 메서드는 `HttpSecurity`의 설정을 바탕으로 `SecurityFilterChain`을 생성.
   - `SecurityFilterChain`은 웹 요청을 처리하는 필터 체인으로, 설정된 `Configurer`에 따라 다양한 보안 작업을 수행한다.

### 요약

- `HttpSecurityConfiguration`에서 `HttpSecurity` 객체를 초기화하고, `SpringBootWebSecurityConfiguration`의 `defaultSecurityFilterChain` 메서드에서 이 객체를 사용해 보안 설정을 구성한다.
- `defaultSecurityFilterChain` 메서드는 `HttpSecurity`의 설정을 바탕으로 `build()` 메서드를 호출하여 `SecurityFilterChain`을 생성한다.
- `build()` 메서드는 `HttpSecurity`에 설정된 `Configurer`들의 `init()`과 `configure()` 메서드를 호출하여 설정을 적용하고, 최종적인 보안 필터 체인을 만든다.







### 인증 상태 영속성

---

ScurityContextRepository & SecurityContextHolderFilter



1. ScurityContextRepository 

   - 스프링 시큐리티에서 사용자가 인증을 한 이후 요청에 대해 계속 인증을 유지하기 위해 사용되는 클래스

   - 인증 상태의 영속 메커니즘은 사용자가 인증을 하게 되면 해당 사용자의 인증 정보와 권한이

     SecurityContext에 저장되고 HttpSession을 통해 요청간 영속이 이루어지는 방식이다.

