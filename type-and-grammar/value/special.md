### 3. 특수 값

-   타입과 값이 같은 특수 값

    -   Undefined 타입의 값은 undefined, Null 타입의 값은 null

    -   Undefined

        -   느슨한 모드에서는 전역 스코프에서 undefined 란 식별자에 값 할당이 가능함
        -   모든 모드에서 undefined 란 이름을 가진 지역 변수 생성 가능

        ```
        function foo() {
            undefined = 2
        }

        var undefined = 2
        console.log(undefined) // 2
        ```

        -   undefined는 void 연산자로도 얻을 수 있다. (void 는 어떤 값이든 '무효로 만들어' 결괏값을 undefined 로 만든다)

        ```
        var a = 42
        console.log(void a, a) // undefined 42
        ```

        ```
        if (!APP.ready) {
            return void setTimeout( ... , 100)

            // setTimeout() 함수는 숫자 값(타이머 취소할 때 사용할 타이머의 고유 식별자) 을 반환함
            // 이 문장에서는 숫자 값을 무효로 만들어 if 문에서 긍정 오류가 일어나지 않게 함
        }

        ```

-   특수 숫자

    -   NaN : '유효하지 않은 숫자', 경계 값의 일종, 숫자 집합 내 특별한 종류읭 에러 상황

        ```
        var a = 2 / "foo" // NaN
        typeof a === "number" // true (※ 타입은 number)
        ```

        -   NaN 은 '===' 로 식별되지 않는다. 자기 자신과도 같지 않다. (비교 불능)
        -   NaN 여부 확인: `isNaN()`

            ```
            var a = 2 / "foo"
            var b = "foo"

            a // NaN
            b // "foo"

            window.isNaN(a) // true
            window.isNaN(b) // true ※ "foo"는 당연히 숫자가 아니지만, 그렇다고 NaN 은 아니다! (일종의 버그)
            ```

            -   ES6 의 `Number.isNaN()`

            ```
            Number.isNaN(a) // true
            Number.isNaN(b) // false
            ```