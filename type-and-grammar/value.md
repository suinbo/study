### 1. 배열

-   배열 자체도 하나의 객체여서 키/프로퍼티 문자열 추가 가능 (\* length 증가 X)

    ```
    var a = []
    a[0] = 1
    a["foobar"] = 2

    a.length //1
    a["foobar"] //2
    a.foobar //2
    ```

    -   키로 넣은 문자열 값이 표준 10진수 숫자로 타입 바뀌면, 숫자 키를 사용한 것과 같은 결과

    ```
    var a = []
    a["13"] = 42
    a.length = 14
    ```

-   문자열은 불변 값(Immutable) 이지만 배열은 가변 값(Mutable)

    -   문자열은 문자 배열과 같지 않다.
    -   문자열 또한 배열과 같이 length 프로퍼티, indexOf() 메서드, concat() 메서드 가짐

    ```
    var a = "foo"
    a[1] = "o" // IE 구버전은 문법 에러로 인식 => a.charAt(1) 로 접근하는 것이 맞음
    ```

    -   문자열에 대해 불변 배열 메서드를 빌려쓸 수 있다

    ```
    a.join // undefined (배열 메서드는 문자열에 쓸수 X)
    a.map  // undefined
    a.reverse // undefined

    var c = Array.prototype.join.call(a,"-")
    var d =Array.prototype.map.call(a, function(v){
        returnv.toUpperCase()+  "."
    }).join("")

    c // "f-o-o"
    d // "F.O.O"
    ```
