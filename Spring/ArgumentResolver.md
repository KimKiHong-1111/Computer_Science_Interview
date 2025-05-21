# 스프링 ArgumentResolver와 커스텀 어노테이션 활용 정리

---

## 1. 기존 방식의 한계

- **HttpServletRequest, @CookieValue, @SessionAttribute 등**을 직접 컨트롤러 파라미터로 받아서 값을 꺼내오는 방식은 코드가 장황해지고, 여러 컨트롤러에서 반복적으로 사용될 수 있음.
- 예시:
    - `request.getAttribute("test")`로 직접 값 추출
    - `@CookieValue`로 쿠키를 직접 받아서 로그인 상태 판별
    - `HttpSession`을 직접 받아 세션에서 값 추출

---

## 2. ArgumentResolver란?

- 스프링 MVC가 컨트롤러의 파라미터를 자동으로 주입해주는 기능의 핵심.
- 우리가 흔히 사용하는 `@RequestParam`, `@PathVariable`, `@SessionAttribute` 등도 모두 내부적으로 ArgumentResolver를 사용함.
- **핵심 개념:**  
  컨트롤러 메서드 파라미터에 어노테이션을 붙이면, ArgumentResolver가 동작하여 해당 값을 자동으로 주입해줌.

---

## 3. 커스텀 ArgumentResolver 만들기

- **커스텀 어노테이션**(예: `@CustomSessionAttribute`, `@CustomRequestParam`, `@CustomPathVariable`)을 정의하고,
- **HandlerMethodArgumentResolver**를 구현하여 원하는 방식으로 값을 추출, 변환해서 파라미터에 주입할 수 있음.
- WebMvcConfigurer의 `addArgumentResolvers` 메서드에서 등록하여 사용.

---

## 4. JWT 인증과 AuthArgumentResolver

- JWT 기반 인증에서는 토큰에서 사용자 정보를 추출해 컨트롤러 파라미터로 넘기는 작업이 필요함.
- **AuthArgumentResolver**와 `@Auth` 어노테이션을 만들어,
    - JwtFilter가 JWT에서 userId를 추출해 request attribute에 저장
    - AuthArgumentResolver가 이 값을 읽어 `AuthUser` 객체로 만들어 파라미터에 주입
- 컨트롤러에서는 단순히 `@Auth AuthUser authUser`만 선언하면 인증된 사용자 정보를 바로 사용할 수 있음.

---

## 5. 주요 장점

- 반복 코드를 줄이고, 컨트롤러 코드가 간결해짐
- 인증, 세션, 요청 파라미터 등 다양한 값을 일관된 방식으로 주입 가능
- 스프링의 확장성과 유연성을 적극 활용

---

## 6. 결론

- 스프링에서는 이미 많은 ArgumentResolver가 내장되어 있고, 필요에 따라 커스텀하게 구현할 수 있음.
- 실제로 `@RequestParam`, `@PathVariable`, `@SessionAttribute` 등은 모두 ArgumentResolver의 구현체임.
- JWT 인증, 세션, 커스텀 파라미터 등 다양한 상황에서 ArgumentResolver를 활용하면 코드의 재사용성과 유지보수성이 크게 향상됨.

---

> **TIP:**  
> 컨트롤러 파라미터에 어떤 값이 어떻게 주입되는지 궁금하다면, 직접 커스텀 ArgumentResolver를 만들어보고, 디버깅이나 로그 출력을 통해 동작 원리를 확인해보세요!
