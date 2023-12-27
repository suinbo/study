1. ToString

    - `문자열 아닌 값 -> 문자열` 변환
    - 일반 객체는 기본적으로 Object.prototype.toString() 가 내부 [[Class]] 반환 (ex. "[oject Object]")
    - 자신의 toString() 메서드를 가진 객체는 Object.prototype.toString()을 대신함
        ```
        var a = [1,2,3]
        a.toString() // "1,2,3" => 모든 원소 값이 콤마로 분리
        ```
    - JSON.stringify()

        - JSON 안전 값은 모두 JSON.stringfy() 문자열화 가능
        - JSON 안전 값이 아닌 것(undefined, 함수, 심벌 등)들은 자동으로 누락시키며 배열로 포함되어 있을 경우 null로 바꿈

            ```
            JSON.stringify(undefined) // undefined
            JSON.stringify(function(){}) // undefined

            JSON.stringify([1, undefined, function(){}, 4]) // "[1,null,null,4]"
            JSON.stringify({ a:2, b:function(){} }) // "{"a":2}"
            ```

        - 환형 참조 객체는 JSON.stringify() 로 문자열 하려면 `toJSON()` 메서드를 따로 정의

            - toJSON() 의 역할은 '문자열화하기 적당한 JSON 안전 값으로 바꾸는 것'

            ```
            var o = {}

            var a = {
                b: 42,
                c: o,
                d: function(){}
            }

            o.e = a // 'a' 를 환형 참조 객체로 만들기

            JSON.stringify(a) // 에러 발생

            a.toJSON() = function() {
                return { b: this.b } // 직렬화에 프로퍼티 'b' 만 포함
            }

            JSON.stringify(a) // "{"b":42}"
            ```

        - JSON.stringify() 의 두번째 인자로 **배열 또는 함수(= 대체자)**를 전달하면, 객체를 재귀적으로 직렬화하며 필터링 함

            - 대체자가 배열이라면 (1)전체 원소는 문자열, (2)각 원소는 객체 직렬화의 대상 프로퍼티 명

                ```
                var a = {
                    b: 42,
                    c: "42",
                    d: [1,2,3]
                }

                JSON.stringify(a, ["b", "c"]) // "{"b": 42, "c": "42"}"
                ```

            - 함수면 처음 한 번은 객체 자신에 대해, 그 다음은 객체 프로퍼티별로 한 번씩 실행 => 문자열화가 재귀적으로 이루어짐
                ```
                JSON.stringify(a, function(k,v) {
                    if (k !== "c") retun v
                })
                // "{"b":42, "d": [1,2,3]}"
                ```

2. ToNumber

    - `숫자 아닌 값 -> (수식 연산 가능한) 숫자` 변환

        - true -> 1, false -> 0, undefined -> NaN, null -> 0
        - 객체(배열)은 동등한 원시 값으로 변환 후 그 결과값을 ToNumber 규칙에 의해 강제변환

            ```
            var a = {
                valueOf: function() {
                    return "42"
                }
            }

            var b = {
                toString: function() {
                    return "42"
                }
            }

            var c = [4,2]
            c.toString = function() {
                return this.join("")
            }

            Number(a)  // 42
            Number(b)  // 42
            Number(c)  // 42
            Number("") // 0
            Number([]) // 0
            Number(["abc"]) // NaN
            ```

3. ToBoolean

    - Falsy 값 : 불리언으로 강제변환했을 때 false 인 값

        - `undefined`, `null`, `false`, `+0, -0, NaN`, `""`
        - Object -> true (강제변환)
