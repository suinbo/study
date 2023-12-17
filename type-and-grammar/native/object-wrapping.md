### 2. 래퍼 박싱과 언박싱

-   자바스크립트는 원시 값을 감싸는(박싱) 객체 래퍼(네이티브)를 제공한다

    -   원시 값엔 프로퍼티나 메서드가 없지만 자바스크립트가 알아서 박싱하여 `.length`, `.toUpperCase()` 로 접근 가능

        ```
        var a = "abc"

        a.length // 3
        a.toUpperCase() // "ABC"
        ```

    -   `new Boolean(false)` 의 경우, `false를 객체 래퍼로 래핑했다` 고 함
        => 객체는 "truthy"

        ```
        var a = new Boolean(false)

        if(!a) {
            console.log("hi")  // 실행 X
        }
        ```

-   언박싱

    -   객체 래퍼의 원시 값은 `valueOf()` 메서드로 추출

    ```
    var a = new String("abc")
    var b = new Number(42)
    var c = new Boolean(true)

    a.valueOf() // "abc"
    b.valueOf() // 42
    c.valueOf() // true
    ```
