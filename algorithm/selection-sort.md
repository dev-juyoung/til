# 선택정렬

`선택 정렬`은 특정한 기준에 따라 배열이나 리스트를 정렬하는 알고리즘 중 하나이다.

만약, 치킨 브랜드와 브랜드에 따른 선호도를 조사한 리스트가 있다고 가정해보자.  
~~(브랜드명과 선호도는 내 멋대로 입력한 것임...)~~

|브랜드명|선호도|
|:--:|:--:|
|교촌|97|
|네네치킨|83|
|BBQ|75|
|처갓집|100|
|지코바|34|
|옛날치킨|82|

위 리스트를 선호도가 **높은 순부터 낮은 순으로 정렬** 한다고하면, 어떻게 해야 될까?

가장 쉬운 방법 중 하나는, 해당 리스트의 **모든 항목을 하나씩 비교**해 본 후, 선호도가 높은 순서대로 **항목을 하나씩 추출하여 새로운 리스트**를 만들어 내는 방법이 있다.

위에서 언급 했듯이, 선택 정렬은 배열 또는 리스트의 모든 항목을 하나씩 비교하여, 정렬의 기준에 맞게 새로운 리스트를 만들어 내는 알고리즘이다.

그렇다면 위의 긴 문장을 `빅오 표기법`으로 표기해보자.

선택 정렬은, **하나의 항목**을 추출하기 위해 모든 항목을 읽고 점검해야 하므로 `O(n)` 시간이 걸린다.

이러한 `O(n)`시간이 걸리는 작업을 리스트의 크기 만큼인 `n`번을 실행하여야 한다.

그러므로, 선택 정렬은 빅오표기법으로 표기할 경우, `O(n x n)`의 시간, 즉 `O(n²)`으로 표기할 수 있다.

### \#. 시나리오
* 숫자로 이루어진 배열이 있을 경우, 해당 배열을 작은 값부터 큰 값 순으로 정렬하고자 한다.

### \#. 구현 (Kotlin)
``` kotlin
fun findSmallest(arr: List<Int>): Int {
    var smallest = arr[0]
    var smallestIndex = 0

    for (i in arr.indices) if (arr[i] < smallest) {
        smallest = arr[i]
        smallestIndex = i
    }

    return smallestIndex
}

fun selectionSort(arr: MutableList<Int>): List<Int> {
    val size = arr.size
    val newArr = ArrayList<Int>(size)

    for (i in 0 until size) {
        val smallest = findSmallest(arr)
        newArr.add(arr[smallest])

        arr.removeAt(smallest)
    }

    return newArr
}

fun main(args: Array<String>) {
    val source = arrayListOf<Int>(5, 3, 6, 2, 10)
    println("정렬 결과: ${selectionSort(source)}")
}
```

### \#. 결과값
```
> 정렬 결과: [2, 3, 5, 6, 10]
```

> 스터디에 사용 된 전체 코드는 [algorithm repository][repository]에서 확인 가능.

[repository]: https://github.com/dev-juyoung/algorithm-study