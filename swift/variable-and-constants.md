# 변수와 상수

프로그래밍을 함에 있어 가장 기본은 `변수(variable)`와 `상수(constant)`를 선언하는 것이다.

그렇다면 변수와 상수는 무엇을 뜻하는 것인지 알아야 될 필요가 있다.
* `변수(variable)`: 언제 어디서나 수시로 값을 변경할 수 있다.
* `상수(constant)`: 한번 값이 정해지면 변경이 불가능하다.

`Swift`언어에서는 언제 어디서 변경될 지 알 수 없는 변수보다는 상수를 사용하길 권장한다고 한다.

간략한 코드를 이용하여 `Swift`에서의 변수와 상수의 선언법을 알아본다.

``` swift
// 변수는 다음의 형태로 선언한다.
// var variableName: Type = init value
var name: String = "Juyoung Lee"

// 상수는 다음의 형태로 선언한다.
// let constantName: Type = init value
let birthyear: Int = 1990

// 변수는 언제 어디서나 값을 변경할 수 있다.
name = "이주영"

// 상수는 값을 변경하려 할 경우, 컴파일러에 의해 차단된다.
birthyear = 2018 // 이 코드는 실제 컴파일이 되지 않고 에러가 표출된다.

// 변수 또는 상수를 선언함과 동시에 값을 초기화할 경우, Type을 생략할 수 있다.
// 이러한 동작을 컴파일러가 타입을 추론한다라고 표현한다.
var height = 170.5 // 이 코드는 Float 타입으로 추론된다.

// Swift는 엄격한 언어이므로, 타입이 다른경우 연산이 불가능하다.
// 그러므로, 연산을 위해 타입을 동일하게 변환하여야 한다.
// let sum = age + height // 이 코드는 실제 컴파일 되지 않는다.
let sum = Float(age) + height
```