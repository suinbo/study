### 3-2. 네이티브는 생성자다

-   (2) Object( ), Function( ), RegExp( )

    -   Object() 보다는 리터럴 형태가 효율적
    -   Function() 는 매우 드문 경우에 함수의 인자나 내용을 동적으로 정의

    -   정규 표현식은 리터럴 형태(/^a\*b+/g) 일 때, **자바스크립트 엔진이 실행전 정규 표현식을 미리 컴파일한 후 캐시**하여 성능상 이점 있음

        ```
        // 리터럴 형태 => 동일한 정규 표현식을 여러 번 사용해도 한 번만 컴파일
        const regexLiteral = /^a*b+/g

        // new RegExp를 사용한 형태 => 새로운 객체 생성
        const regexConstructor = new RegExp("^a*b+", "g")
        ```

-   (3) Date( ), Error( )

    -   이 둘은 리터럴 형태 X
    -   Unix timestamp : `new Date().getTime()`
    -   error 객체의 주 용도는 현재 **실행 스택 컨텍스트**를 포착하여 객체에 담는 것  
        => 실행 스택 컨텍스트는 함수 호출 스택, error 객체가 만들어진 줄 번호 등 디버깅에 도움되는 정보 담고있음

        ```
        const error = new Error("error occured!!")
        error.message //"error occured!!"
        ```

-   (4) Symbol( )

    -   ES6(ECMAScript 2015)에서 도입된 새로운 기본 데이터 타입

    -   객체 아니고 **스칼라 원시 값** 이며 **유일하고 변경 불가능한 값**

    -   Symbol은 보통 객체의 프로퍼티 키로 사용되어 해당 프로퍼티를 다른 식별자들과 충돌하지 않게 만들기 위해 활용  
        => Symbol의 실제 값을 보거나 접근하는 것은 불가

        ```
        const mySymbol = Symbol('description') // new 가 앞에 붙으면 에러
        const obj = {
            [mySymbol]: 'This is a symbol property'
        }

        console.log(obj[mySymbol]) // 'This is a symbol property'
        ```

    -   Symbol 직접 정의: `Symbol()`

        -   `Object.getOwnPropertySymbols(a)` : a 객체의 심볼 프로퍼티를 배열로 반환

            ```
            var mysym = Symbol("my own symbol")
            mysym // Symbol(my own symbol)

            var a = {}
            a[mysym] = "foobar"
            Object.getOwnPropertySymbols(a) // [Symbol(my own symbol)]
            ```

    -   ES6 에서의 Symbol (Symbol 함수 객체의 정적 프로퍼티)
        -   `Symbol.create`
        -   `Symbol.iterator`
