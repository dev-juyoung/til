# 배열과 딕셔너리

모든 프로그래밍 언어에는 연관된 데이터를 보다 효율적으로 저장하고 관리할 수 있도록 제공되는 자료형이 존재한다.

`Swift`에서는 `배열(Array)`과 `딕셔너리(Dictionary)`를 제공하고 있다.

간략한 코드를 통하여 Swift에서의 배열과 딕셔너리에 대해 알아보자.

``` swift
// 배열은 다음과 같이 생성할 수 있다.
var language: [String] = ["Swift", "Kotlin", "Go"]
// 타입추론을 이용하면 아래와 같이 코드를 축약할 수 있다.
// var language = ["Swift", "Kotlin", "Go"]

// 딕셔너리는 다음과 같이 생성할 수 있다.
var capitals: [String: String] = [
  "korea": "seoul",
  "japan": "tokyo",
  "china": "beijing"
]
// 타입추론을 이용하면 아래와 같이 코드를 축약할 수 있다.
// var capitals = [
//  "korea": "seoul",
//  "japan": "tokyo",
//  "china": "beijing"
//]

// 배열의 값을 읽어오거나, 변경하는 경우에는 index값을 이용하여 접근할 수 있다.
language[0] // Swift라는 값을 읽어온다.
language[2] = Python // Go라는 값을 Python으로 변경한다.
language.append("Node.js") // language 배열에 새로운 값 "Node.js"를 추가한다.

// 딕셔너리는 "key": "value" 형태의 자료를 저장하는 자료형이다.
// 그러므로, "key" 값을 이용하여 접근할 수 있다.
captials["korea"] // seoul 이라는 값을 읽어온다.
captials["japan"] = "도쿄" // tokyo라는 값을 도쿄로 변경한다.
captials["usa"] = "워싱턴 D.C" // captials에 "usa"라는 key 값을 가진 워싱턴 D.C라는 데이터를 추가한다.
```