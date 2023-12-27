1. 명시적 강제변환

    - 문자열 <-> 숫자

        - String(), Number()
        - toString()
            - ex. 원시 값 42 에는 toString() 메서드가 없으므로 엔진은 이를 사용할 수 있게 자동으로 42를 객체 래퍼로 `박싱` 한다!
        - 단항 연산자 +

            ```
            var a = "3.14"
            var b = +a

            b // 3.14
            ```

    - 날짜 -> 숫자

        - 단항 연산자 +
            ```
            var c = new Date("Mon, 18 Aug 2014 08:53:06 CDT")
            +c // 1408369986000
            ```
        - Date.now() (현재 타임스탬프)

    - 틸드 (~) 연산자

        - (1) 2의 보수 연산
        - ★ 숫자 값에 ~연산을 할 경우 입력 값이 -1 이면 falsy한 0, 그 외에는 truthy한 숫자 값 산출

            - ex. indexOf() 로 검색 결과 실패시 -1, 이를 ~ 연산하면 0 으로 변환

                ```
                var a = "Hello, World"
                ~a.indexOf("lo") // -4 (truthy)

                if (~a.indexOf("lo")) {  // true
                    console.log("찾음")
                }

                ~a.indexOf("ol") // 0 (falsy)

                if (!~a.indexOf("lo")) {  // true
                    console.log("못찾음")
                }
                ```

        - (2) 비트 잘라내기
            - ~~ : 정수로 상위 비트를 잘라냄
              (불리언의 패리티 이중부정 !! 과 유사)
                ```
                Math.floor(-49.6) // -50
                ~~-49.6 // -49
                ```

    - 숫자 형태의 문자열 파싱

        - 문자열로부터 숫자 값의 파싱은 비 숫자형 문자 허용: 좌 -> 우 방향으로 파싱 후 숫자 아닌 문자 만나면 멈춤
        - 강제변환은 비 숫자형 문자를 허용 X -> NaN

            ```
            var a = "42"
            var b = "42px"

            Number(a) // 42
            parseInt(a) // 42

            Number(b) // NaN
            parseInt(b) // 42
            ```

    - \* -> 불리언
        - !! (이중 부정 연산자)
