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

        - JSON.stringify() 의 두번째 인자로 **배열 또는 함수(대체자)**를 전달하면, 객체를 재귀적으로 직렬화하며 필터링 함

            - 배열이라면 전체 원소는 문자열이여야 함

2. ToNumber

3. ToBoolean

    - Falsy 값
    - Falsy 객체
    - truthy 값
