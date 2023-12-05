### 2. 숫자

-   자바스크립트의 number은 IEEE 754 표준을 따름 (Double Precision 64 bit binary)

-   숫자 리터럴에서 바로 접근 가능한 메서드

    -   toFixed() : 소수점 이하 자릿수까지 숫자 값을 문자열 형태로 반환
    -   toPrecision() : (위와 동일) 유효 숫자 개수 지정
    -   . (소수점) 을 사용하는 경우, 숫자 리터럴의 일부로 해석하여 구문 에러 날 수 있음

    ```
    var a = 42.59
    a.toFixed(0) // "43"
    a.toFixed(1) // "42.6"
    a.toFixed(2) // "42.59"

    a.toPrecision(1) // "4e+1"
    a.toPrecision(2) // "43"
    a.toPrecision(3) // "42.6"
    a.toPrecision(6) // "42.5900"

    // 잘못된 구문
    42.toFixed(3) // SyntaxError (42. 의 .을 리터럴 일부로 해석하여 메서드 접근 불가)

    // 올바른 구문
    (42).toFixed(3) // "42.000"
    0.42.toFixed(3) // "0.420"
    42..toFixed(3)  // "42.000" => 숫자 리터럴 일부, 프로퍼티 연산자
    42 .toFixed(3)  // "42.000"
    ```

    -   숫자 리터럴의 2진수, 8진수, 16진수

    ```
    0xf3 // 243 16진수
    0Xf3 // 243 16진수
    0363 // 243 8진수

    /* ES6*/
    0o363 // 243 8진수
    0b11110011 // 243의 2진수
    ```

-   이진 부동 소수점 숫자

    -   부동 소수점(floating point, 지수 값에 따라 소수점이 이동하는 모양이 마치 떠다니는 듯 함) 의 표현 방식
        ![Alt text](image.png)

    -   `0.1 + 0.2 === 0.3  // false (실제로는 0.300000000000000004 에 가까움)`

        -   0.1 + 0.2 와 0.3 두 숫자 비교하는 방법: Number.EPSILON

            -   반올림 오차를 허용 공차로 처리

            ```
            /* ES6 이전 브라우저 */
            if (!Number.EPSILON) {
                Number.EPSILON = Math.pow(2,-52) // 2의 -52승은 자바스크립트 숫자의 임계 값(가장 작은 수, 머신 입실론)
            }

            /* ES6 */
            function numberCloseEnoughToEqual (n1,n2) {
                return Math.abs(n1-n2) < Number.EPSILON
            }

            var a = 0.1 + 0.2
            var b = 0.3
            numberCloseEnoughToEqual(a,b) // true
            ```

    -   부동 소수점 숫자 최댓값 : Number.MAX_VALUE
    -   부동 소수점 숫자 최솟값 : Number.MIN_VALUE

-   정수는 안전값의 범위가 정해져 있다.

    -   안전값이란 '표현한 값과 실제 값이 정확하게 일치한다고 말할 수 있는 값'
    -   `Number.MAX_SAFE_INTEGER`, `Number.MIN_SAFE_INTEGER`
    -   안전한 정수 여부 확인: Number.isSafeInteger()

    -   정수의 안전 범위: Math.pow(-0,31) ~ Math.pow(2,31)-1

        -   정수의 '안전 범위' 는 대략 9천 조에 이르지만 비트연산처럼 32비트 숫자에만 가능한 연산이 있으므로 실제 범위는 훨씬 적음

    -   64비트 숫자는 숫자 타입으로 정확하게 표시할 수 없으므로 string 타입으로 저장
