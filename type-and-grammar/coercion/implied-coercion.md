1.  암시적 강제변환

    -   문자열 <-> 숫자

        -   `+` 연산자는 (1)숫자의 덧셈, (2)문자열 접합의 목적으로 오버로드 됨  
            => (2)한쪽 피연산자가 문자열이면 + 는 문자열 붙이기 연산

            ```
            // 암시적 강제변환의 예시
            var a = 42
            var b = a + ""

            a + b // "42"
            ```

            -   ToPrimitive 연산과정에서 a + "" 는 a 값을 `valueOf()` 메서드에 전달하여 호출하고,  
                그 결괏값은 `ToString()` 추상 연산을 하여 최종적인 문자열로 변환

            ```
            var a = [3]
            var b = [1]

            a - b // 2
            ```

            -   두 배열 a,b 는 우선 문자열로 강제변환된 뒤(toString() 로 직렬화) 숫자로 강제변환 (- 연산자는 뺄셈 기능만 가짐)

    -   불리언 -> 숫자

        -   불리언 값을 0 또는 1 로 변환

        ```
        function onlyOne() {
            var sum = 0
            for (var i = 0; i < arguments.length; i ++) {
                // falsy 값은 건너뛰기
                if (arguments[i]) {
                    sum += arguments[i]  // 암시적 강제변환, 인자 중 딱 하나만 true 일때 sum 은 1
                }
            }

            return sum == 1
        }

        var a = true
        var b = false
        onlyOne(b,a) // true
        onlyOne(b,b,a,b,b,b) // true
        onlyOne(b,b) // false
        onlyOne(b,a,b,b,a,a) // false
        ```

    -   \* -> 불리언

        -   불리언으로 암시적 강제변환이 일어나는 표현식

            -   (1) if () 문의 조건식
            -   (2) for ( ; ; ) 에서 두 번째 조건 표현식
            -   (3) while() 및 do..while() 루프의 조건 표현식
            -   (4) ? : 삼항 연삭 시 첫 번째 조건 표현식
            -   (5) || 및 && 의 좌측 피연산자

            ```
            var a = 42
            var b = "abc"
            var c;
            var d = null

            if (a) {
                console.log("출력됨")
            }

            while(c) {
                console.log("실행 안됨")
            }

            c = d ? a : b
            c // "abc"

            if ((a && d) || c) {
                console.log("출력됨")
            }
            ```

    -   && 와 || 연산자 (피연산자 선택 연산자)

        -   결괏값은 **두 피연산자 중 한 쪽 값** (반드시 불리언 타입인 것은 아님)

            ```
            var a = 42
            var b = "abc"
            var c = null

            a || b // 42
            a && b // "abc"

            c || b // "abc"
            c && b // null
            ```

            -   첫 번째 피 연산자의 불리언 값 평가 => 피 연산자가 비 불리언 타입이면 ToBoolean 으로 강제변환 후 평가

                -   || 연산자: 그 결과가 true 면 첫번째 피연산자 값을, false 면 두번째 피연산자 값을 반환 ( ex. `a ? a : b` )
                -   && 연산자: 그 결과가 true 면 두번째 피연산자 값을, false 면 첫번째 피연산자 값을 반환 ( ex. `a ? b : a` )

        -   && 연산자를 "가드 연산자" 라고도 함 => 첫 번째 표현식이 두 번째 표현식의 "가드" 역할

            ```
            var a = 42

            function foo() {
                console.log(a)
            }

            a && foo() // 42
            ```

            -   a 평가 결과가 truthy 일때만 foo() 호출, falsy 면 a && foo() 는 실행 멈춤

    -   심벌의 강제변환
        -   심벌 -> 문자 명시적 강제변환은 허용, 암시적 강제변환 에러
        -   심벌 -> 불리언 값 명시적/암시적 강제변환 가능
