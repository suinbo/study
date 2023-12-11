### 1. 네이티브

-   네이티브는 내장 함수다

    -   String(), Number(), Boolean(), Array(), Object(), Function(), RegExp(), Date(), Error(), Symbol() (ES6)
    -   네이티브는 생성자처럼 사용할 수 있다.

        ```
        var a = new String("abc")

        typeof a // "object"
        a instanceof String // true
        Object.prototype.toString.call(a) // "[object String]"
        ```

-   내부 [[Class]]

    -   typeof 가 "object" 인 값에는 **[[Class]]** 라는 **내부 프로퍼티**가 붙는다

        -   [[Class]] 는 `Object.prototype.toString(...)` 호출로 확인 가능

            ```
            Object.prototype.toString.call([1,2,3])
            // [object Array] => 내부 [[Class]] 값: Array

            Object.prototype.toString.call(/regex-literal/i)
            // [object RegExp] => 내부 [[Class]] 값: RegExp
            ```

        -   원시 값의 내부 [[Class]]

            ```
            Object.prototype.toString.call(null)
            // [object Null] => 내부 [[Class]] 값: Null

            Object.prototype.toString.call(undefined)
            // [object Undefined] => 내부 [[Class]] 값: Undefined
            ```
