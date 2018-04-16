# 이진탐색

`n개`의 원소를 가진 리스트에서 특정한 원소를 찾는 것을 `탐색(Search)`라고 한다.

탐색에서는 두가지 방법이 존재한다.
* 단순 탐색 (Simple Search)
  * 첫번째 원소부터 마지막 원소까지 차례로 값을 비교하는 방법.
* 이진 탐색 (Binary Search)
  * 리스트의 전체 길이의 반을 기점으로 검색하는 방법.

### \#. 시나리오
> 1 ~ 100까지의 숫자 중 57라는 숫자를 찾고자 한다.

* 단순 탐색의 경우 1부터 순차적으로 57번의 숫자 비교로 값을 찾을 수 있다.
  > 1 == 57 => `false`  
  > 2 == 57 => `false`  
  > 3 == 57 => `false`  
  > ...  
  > 57 == 57 => true
* 이진 탐색의 경우 매 탐색 시마다 범위를 반씩 좁힐 수 있으므로, 4번의 숫자 비교로 값을 찾을 수 있다.
  > 50 == 57 => `false`이며, `50`은 너무 작다.  
  > 75 == 57 => `false`이며, `75`는 너무 크다.  
  > 63 == 57 => `false`이며, `63`은 너무 크다.  
  > 57 == 57 => `true`

### \#. 전제 조건.
* 입력 값으로 `정렬된 원소 리스트`를 받는다.
* 출력 값으로 `해당 원소의 위치` 또는 `null`을 반환한다.

### \#. 구현 (Kotlin)
``` kotlin
fun binarySearch(list: Array<Int>, item: Int): Int? {
    var low = 0
    var high = list.size - 1

    while(low <= high) {
        val mid = (low + high) / 2
        val guess = list[mid]

        if (guess == item) {
            return mid
        }

        if (guess > item) {
            high = mid - 1
        } else {
            low = mid + 1
        }
    }

    return null
}

fun main(args: Array<String>) {
    val source = arrayOf(1, 3, 5, 7, 9)

    println("탐색 결과: ${binarySearch(source, 3)}")
    println("탐색 결과: ${binarySearch(source, -1)}")
}
```

### \#. 결과값
```
> 탐색결과: 1
> 탐색결과: null
```

> 스터디에 사용 된 전체 코드는 [algorithm repository][repository]에서 확인 가능.

[repository]: https://github.com/dev-juyoung/algorithm-study