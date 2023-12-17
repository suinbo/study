### 4. 네이티브 프로토타입

-   내장 네이티브 생성자는 각자의 .prototype 객체를 가진다

    -   ex. Array.prototype, String.prototype
    -   String.prototype.XYZ => String#XYZ
        -   String#indexOf : 문자열에서 특정 문자 위치 검색
        -   String#charAt : 문자열에서 특정 위치 문자를 반환
        -   String#substring : 문자열의 일부를 새로운 문자열로 추출
    -   모든 함수는 Function.prototype 에 정의된 apply(), call(), bind() 메서드 사용 가능

-   프로토타입은 `디폴트`다
    -   Function.prototype => 빈 함수, RegExp.prototype => 빈 정규식, Array.prototype => 빈 배열
