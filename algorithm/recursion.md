# 재귀

사전적 의미에서의 `재귀(Recursion)`란, **원래 자리로 되돌아가거나 되돌아옴** 이라는 뜻을 가지고 있다고 한다.

사전적 의미에서도 알 수 있 듯,  
프로그래밍에서 자주 언급되는 `재귀함수(Recursion Function)`는 쉽게 말해 **자기 자신**을 호출하는 함수를 의미한다.

즉, 어떠한 일을 처리하는 함수를 만들었을 때, 그 함수 안에서 자기 자신을 다시 불러서 함수가 실행되도록 만든 것이다.

### \#. 재귀함수의 단계
재귀 함수는 자기 자신을 호출하는 함수이기 때문에, 자칫 잘못하면 `무한 루프`에 빠지기 쉽다.  

이러한 무한 루프를 방지하기 위해서는 재귀 함수를 작성할 때, 두 가지 상태 혹은 단계를 고려하여 작성하여야 한다.

* 기본 단계 (Base Case)
* 재귀 단계 (Recursive Case)

각 단계가 의미하는 명칭에서 알 수 있 듯,  
`기본 단계`는 해당 재귀 함수가 언제 재귀를 멈추는지 알 수 있도록 해당 함수의 `탈출 조건`을 정해주는 부분이며, `재귀 단계`는 말 그대로 해당 함수가 다시 `자기 자신을 호출`하는 부분이다.

### \#. 시나리오#1
> 사용자로부터 입력받은 숫자를 기준으로 카운트 다운하는 프로그램을 작성하고자 한다.

### \#. 구현#1 (Kotlin)
``` kotlin
fun countDown(i: Int) {
    print("$i...")
    // 프로그램이 너무 빨리 종료되지 않도록 1초동안 멈춤.
    Thread.sleep(1000)
    // 자기자신을 다시 호출한다.
    countDown(i - 1)
}

fun main(args: Array<String>) {
    countDown(5)
}
```

위의 코드를 언뜻 보면, 큰 문제가 없다고 생각할 수 있지만 잘못된 프로그램이다.

일반적인 사용자가 생각하는 카운트 다운 프로그램이라면,  
아마 0초가 되는 순간 프로그램이 종료되길 기대할 것이다.

하지만, 위의 코드는 0초가 되더라도 프로그램이 종료되지 않고, 음수의 영역으로 들어가며 영원히 종료되지 않는 프로그램이 될 것이다.

이러한 문제를 내재하고 있는 프로그램 또는 소스코드를 흔히 말해 `무한 루프`에 빠졌다라고 한다.

위의 재귀 함수를 일반적인 사용자가 기대하는 프로그램으로 소스코드를 수정하여 보자.

```kotlin
fun countDown(i: Int) {
    print("$i...")
    // 프로그램이 너무 빨리 종료되지 않도록 1초동안 멈춤.
    Thread.sleep(1000)

    if (i <= 1) {
        // 기본 단계
        return
    } else {
        // 재귀 단계
        countDown(i - 1)
    }
}
```
위의 코드에서 볼 수 있 듯 `if (i <= 1)`와 같은 `탈출조건`을 추가하여, 무한루프에 빠지지 않는 재귀함수를 완성할 수 있다.

### \#. 스택
`스택(Stack)`은 아주 단순한 자료구조의 하나이다.

스택이라는 자료구조는, 리스트의 한쪽 끝에서만 원소의 삽입과 삭제가 수행되는 제한 조건을 가진 `선형 자료 구조(Linear Data Structure)`이며, 새로운 원소를 삽입하는 동작을 `push`라 하고, 가장 최근에 삽입된 원소를 삭제하는 동작을 `pop`이라고 한다.

조금 어렵게 느껴질 수 있으나,  
실 생활과 접목하여 비교를 해본다면, 가장 일반적이고 대중적으로 예를 들 수 있는 권총(?) 혹은 탄알집(?)의 동작 원리를 생각해보면 쉽게 이해할 수 있다.

권총의 탄알집에 총알을 채운다고 생각해보자.  
탄알집에 총알이 비어있는 만큼, 위에서부터 하나씩 차곡차곡 총알을 채워 넣을 것이다. **`[PUSH]`**

그리고, 이렇게 채워진 탄알집을 권총과 결합하여 실제 사격을 실시 할 때에는 가장 최근에 채워진 총알이 먼저 발사된다. **`[POP]`**

### \#. 호출 스택
컴퓨터에서는 호출 스택이라고 불리는 스택을 사용한다.  
위에서 스택을 언급 했기 때문에, 간단한 소스코드를 이용하여 호출 스택이 무엇인지 알아보자.

``` kotlin
fun welcome(name) {
    println("Hello, $name!")
    greet(name)
    println("getting ready to say bye...")
    bye()
}

fun greet(name) {
    println("How are you, $name?")
}

fun bye() {
    println("Ok, Bye!")
}
```
위의 코드를 실행하면 컴퓨터는 내부적으로 다음과 같은 일이 일어난다.

1) `welcome("Cro")` 함수를 위한 메모리 할당 및 함수의 실행.
    > **[컴퓨터 메모리 영역 상태]**
    > <table>
    > <tr>
    > <td colspan="2" align="center">welcome (Stack#1)</td>
    > </tr>
    > <tr>
    > <td>name:</td>
    > <td>Cro</td>
    > </tr>
    > </table>
2) `Hello, Cro!`를 출력 한 후, `greet("Cro")` 함수를 위한 새로운 메모리 할당 및 함수의 실행. (이 때, 컴퓨터는 메모리를 스택으로 사용한다.)
    > **[컴퓨터 메모리 영역 상태]**
    > <table>
    > <tr>
    > <td colspan="2" align="center">greet (Stack#2)</td>
    > </tr>
    > <tr>
    > <td>name:</td>
    > <td>Cro</td>
    > </tr>
    > <tr>
    > <td colspan="2" align="center">welcome (Stack#1)</td>
    > </tr>
    > <tr>
    > <td>name:</td>
    > <td>Cro</td>
    > </tr>
    > </table>
3) `How are you, Cro?`를 출력한 후, 해당 `greet`함수는 더 이상 실행할 명령이 없으므로, 함수의 호출이 반환된다. 이 때 해당 함수를 위해 할당 되었던 메모리는 `POP` 연산. 즉, 메모리 영역에서 삭제된다.
    > **[컴퓨터 메모리 영역 상태]**
    > <table>
    > <tr>
    > <td colspan="2" align="center">welcome (Stack#1)</td>
    > </tr>
    > <tr>
    > <td>name:</td>
    > <td>Cro</td>
    > </tr>
    > </table>
4) 이 후, 남아있는 `출력문`과 `bye()`함수의 실행 과정도 위와 동일한 원리로 동작된다.

위의 예시와 같은 방식으로 여러 개의 함수를 호출하면서 함수에 사용되는 변수를 저장하는 스택을 `호출 스택(Call Stack)`이라고 한다.

### \#. 시나리오#2
> 호출 스택을 조금 더 명확하게 이해하기 위해 `팩토리얼 함수(Factorial Function)`를 구현해보자.  
> 만약, 팩토리얼 함수가 무엇인지 이해하고 싶다면, [해당문서][factorial]를 참고한다.

### \#. 구현#2 (Kotlin)
``` kotlin

fun fact(x: Int): Int = if (x == 1) 1 else x * fact(x - 1)

fun main(args: Array<String>) {
    println("팩토리얼 함수 결과: ${fact(3)}")
}
```

### \#. 결과값
```
> 팩토리얼 함수 결과: 6
```

> 스터디에 사용 된 전체 코드는 [algorithm repository][repository]에서 확인 가능.

[repository]: https://github.com/dev-juyoung/algorithm-study
[factorial]: http://terms.naver.com/entry.nhn?docId=2455042&cid=42346&categoryId=42346