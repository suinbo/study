### 1. 자바스크립트 내장타입

-   null, undefined, boolean, number, string, object, symbol(ES6)
-   object 를 제외한 나머지를 '원시 타입(Primitives)' 이라 함.
-   값 타입은 typeof 연산자로 알 수 있음.

    -   ex. typeof Symbol() === "symbol" // true
    -   ex. typeof null === "object" //true ("null" 을 반환하지 X)

    *   null 값을 정확히 확인하려면.

    ```
    const a = null
    (!a && typeof a === "object") //true
    ```

-   typeof 가 반환하는 문자열 하나 더 있음.

    -   ex. typeof function a() { ... } === "function" //true
    -   function은 object의 하위 타입 => '호출 가능한 객체'
        -   함수에 선언된 인자 개수 : a.length

-   배열은 객체다.
    -   ex. typeof [1,2,3] === "object" // true (역시 object의 하위타입)

### 2. 값은 타입을 가진다

-   타입이란 개념은 변수에 없다.

        -   변수 앞 typeof 연산자 = "이 변수에 들어있는 값의 타입은 무엇이니?"

-   타입은 값의 내재된 특성을 정의한다.

-   값이 없는 변수의 값 : undefined

    ```
    let a
    typeof a // "undefined"
    ```

    -   선언되지 않은 변수의 typeof 연산결과

        ```
        let a
        typeof a // "undefined"
        typeof b // "undefined" (선언조차 하지 않은 변수인데 브라우저는 오류 처리 X => typeof 만의 안전가드)
        ```

    -   여러 스크립트 파일의변수들이 전역 네임스페이스 공유할때 typeof 안전가드는 쓸모 있다!

        ```
        // DEBUG 라는 전역변수의 존재여부 체크
        if (typeof DEBUG !== "undefined") { ... }

        // 내장 API 기능 체크
        if (typeof atob === "undefined) {
            atob = function() { ... }
        }
        ```

        -   typeof 안전 가드 없이 전역 변수 체크하는 방법 (※ 삼가)

        ```
        // 어떤 깩체의 프로퍼티 접근 시 그 프로퍼티가 존재하지 않아도 ReferenceError 발생 X
        if (window.DEBUG) { ... }
        if (window.atob) {... }
        ```

        -   가져다 쓰는 프로그램에 유틸리티의 특정 변숫값이 정의되어 있는지 체크해야 할때 의존성 주입 설계 패턴

        ```
        function doSomethingCool (FeatureXYZ) {
            var helper = FeatureXYZ || function() { /* 기본 XYZ 기능 */ }

            var val = helper()
        }
        ```

-   undefined 는 "선언된 변수에 할당할 수 있는 값", undeclared 는 "변수 자체가 선언된 적이 없음"
    -   이 둘의 typeof 반환 값은 모두 "undefined" (typeof 안전가드)
