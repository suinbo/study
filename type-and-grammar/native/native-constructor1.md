### 3-1. 네이티브는 생성자다

-   (1) Array( )

    -   Array(1,2,3) 과 new Array(1,2,3) 은 결과적으로 같다
    -   Array 생성자는 인자로 숫자를 하나만 받으면 **배열의 크기를 미리 정한다**

        ```
        const a = Array(1,2,3)
        a // [1,2,3]

        var b = new Array(3)
        b.length //3 (빈 슬롯)
        ```

        -   빈 슬롯 배열과 undefined 로 채워진 배열

            ```
            var a = new Array(3)
            var b = [undefined, undefined, undefined]
            var c = []
            c.length = 3

            a // [empty x 3]  ※chrome기준, 브라우저별로 출력형태가 모두 다름
            b // [undefined, undefined, undefined]
            c // [empty x 3]

            a.join("-") // "--"
            b.join("-") // "--"

            a.map((v,i) => { return i })  // [empty x 3] => a에 슬롯이 없기 때문에 map() 함수가 순회할 원소가 없다
            b.map((v,i) => { return i })  // [0,1,2]
            ```

            -   join() : 슬롯이 있다는 가정 하에 length 만큼 루프 반복
            -   map() : 슬롯 유무를 가정하지 않고 원소 순회

            -   리터럴이 아닌 undefined 로 채워진 배열

                ```
                var a = Array.apply(null, { length:3 })
                a // [undefined, undefined, undefined]

                var b = Array(3).fill(undefined)
                a // [undefined, undefined, undefined]
                ```
