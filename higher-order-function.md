# 고차 함수 (Higher-order function)

* 함수를 다루는 함수
* 다른 함수를 전달 인자로 받거나 함수 실행의 결과를 함수로 반환하는 함수
* 스위프트의 함수는 1등 시민 (first-class citizen)
  * 함수를 **타입**으로 지정하거나,
  * **인자값**으로 넘기거나,
  * **리턴값**으로 받을 수 있다

# Swift Standard Library에서 제공하는 고차함수의 예

### [`map(_:)`](https://developer.apple.com/documentation/swift/array/3017522-map)

```swift
func map<T>(_ transform: (Element) throws -> T) rethrows -> [T]
```

* 시퀀스의 요소들을 주어진 클로저로 매핑한 결과를 포함하는 배열을 반환

### [`flatMap(_:)`](https://developer.apple.com/documentation/swift/array/3126947-flatmap)

```swift
func flatMap<SegmentOfResult>(_ transform: (Element) throws -> SegmentOfResult) rethrows -> [SegmentOfResult.Element] where SegmentOfResult : Sequence
```

* 시퀀스의 각 요소에 대해 특정 변환을 적용한 **연결된** 결과를 포함하는 배열을 반환

### [`compactMap(_:)`](https://developer.apple.com/documentation/swift/array/2957701-compactmap)

```swift
func compactMap<ElementOfResult>(_ transform: (Element) throws -> ElementOfResult?) rethrows -> [ElementOfResult]
```

* 시퀀스의 각 요소에 대해 특정 변환을 적용한 **`nil`이 아닌** 결과를 포함하는 배열을 반환

### [`reduce(_:_:)`](https://developer.apple.com/documentation/swift/array/2298686-reduce)

```swift
func reduce<Result>(_ initialResult: Result, _ nextPartialResult: (Result, Element) throws -> Result) rethrows -> Result
```

* 시퀀스의 요소들을 주어진 클로저를 사용해 결합한 결과를 반환

* 전체 시퀀스의 요소들로부터 하나의 값을 생성

* 예시)

  ```swift
  let numbers = [1, 2, 3, 4]
  let numberSum = numbers.reduce(0, { x, y in
      x + y
  })
  // x: 0, y: 1
  // x: 1, y: 2
  // x: 3, y: 3
  // x: 6, y: 4
  // numberSum == 10
  ```

* 시퀀스가 아무 요소를 가지고 있지 않으면 `nextPartialResult`는 실행되지 않고 `initialResult`가 결과로 반환

* [`reduce(into:_:)`](https://developer.apple.com/documentation/swift/array/3126956-reduce)

  ```swift
  func reduce<Result>(into initialResult: Result, _ updateAccumulatingResult: (inout Result, Element) throws -> ()) rethrows -> Result
  ```

  * 예시)

    ```swift
    let numbers = [1, 2, 3, 4]
    let numberSum = numbers.reduce(into: 0, { x, y in
        x += y
    })
    // x: 0, y: 1
    // x: 1, y: 2
    // x: 3, y: 3
    // x: 6, y: 4
    // numberSum == 10
    ```

  * 결과값이 배열이나 딕셔너리 같은 copy-on-write 타입일 시 효율면에서 `reduce(_:_:)` 보다 선호됨

  * 예시) 인접한 동일 항목 필터링

    ```swift
    let numbers = [1, 1, 2, 2, 2, 3, 4, 4, 5, 4, 3]
    let filtered = numbers.reduce(into: [Int]()) { newArray, number in
        if newArray.last != number { newArray.append(number) }
    }
    // filtered == [1, 2, 3, 4, 5, 4, 3]
    ```

  * 예시) 빈도 카운트

    ```swift
    let letters = "abracadabra"
    let letterCount = letters.reduce(into: [:]) { counts, letter in
        counts[letter, default: 0] += 1
    }
    // letterCount == ["a": 5, "b": 2, "r": 2, "c": 1, "d": 1]
    ```

### [`forEach(_:)`](https://developer.apple.com/documentation/swift/array/1689783-foreach)

```swift
func forEach(_ body: (Element) throws -> Void) rethrows
```

* `for-in`문처럼 시퀀스의 각 요소에 대해 순서대로 주어진 클로저를 호출
* `for-in`문과의 차이점
  * 현재 호출에서 빠져나가거나 다음 호출들을 스킵하기 위해 `break`나 `continue`를 사용할 수 없음
  * `body` 클로저 안에서 `return` 사용 시 오직 `body`에 대한 현재 호출에서만 탈출
* `for-in`과 `forEach(_:)`의 성능 차이
  * `forEach(_:)`는 `for-in`으로 구현되어 있음 (링크: [애플 소스 코드](https://github.com/apple/swift/blob/1bae49950e9b4934b6fd4abecf68a10181e60736/stdlib/public/core/Sequence.swift#L1058))
  * 디버그 빌드에서는 눈에 띄는 성능 차이가 있으나 릴리즈 빌드에서는 성능 오버헤드가 미미

### [`filter(_:)`](https://developer.apple.com/documentation/swift/sequence/3018365-filter)

```swift
func filter(_ isIncluded: (Self.Element) throws -> Bool) rethrows -> [Self.Element]
```

* 주어진 predicate(술부: 문장 속에서 주어에 대해 진술하는 동사 이하 부분)를 만족하는 시퀀스의 요소들을 순서대로 포함하는 배열을 반환

### 참고 학습 자료

* [Stack Overflow - When to use forEach(_:) instead of for in?](https://stackoverflow.com/questions/45333177/when-to-use-foreach-instead-of-for-in)