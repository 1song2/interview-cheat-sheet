# `flatMap(_:)`과 `compactMap(_:)`

Question: *4.1 버전 미만과 최신버전에서의 배열의 메소드인 flatMap의 차이는 무엇인가요?*

### 정의

* [`flatMap(_:)`](https://developer.apple.com/documentation/swift/sequence/2905332-flatmap)

  ```swift
  func flatMap<SegmentOfResult>(_ transform: (Self.Element) throws -> SegmentOfResult) rethrows -> [SegmentOfResult.Element] where SegmentOfResult : Sequence
  ```

  * 시퀀스의 각 요소에 대해 특정 변환을 적용한 **연결된** 결과를 포함하는 배열을 반환
  * 복잡도: O(*m* + *n*) (n: 시퀀스의 길이, m: 결과의 길이)

* [`flatMap(_:)`](https://developer.apple.com/documentation/swift/sequence/2907182-flatmap)(_Deprecated_)

  ```swift
  func flatMap<ElementOfResult>(_ transform: (Self.Element) throws -> ElementOfResult?) rethrows -> [ElementOfResult]
  ```

  * 시퀀스의 각 요소에 대해 특정 변환을 적용한 **`nil`**이 아닌 결과를 포함하는 배열을 반환
  * 복잡도: O(*m* + *n*) (n: 시퀀스의 길이, m: 결과의 길이)

* [`compactMap(_:)`](https://developer.apple.com/documentation/swift/sequence/2950916-compactmap)

  ```swift
  func compactMap<ElementOfResult>(_ transform: (Self.Element) throws -> ElementOfResult?) rethrows -> [ElementOfResult]
  ```

  * 시퀀스의 각 요소에 대해 특정 변환을 적용한 **`nil`**이 아닌 결과를 포함하는 배열을 반환
  * 복잡도: O(*m* + *n*) (n: 시퀀스의 길이, m: 결과의 길이)

### Swift 4.1 미만에서의 `flatMap(_:)`

* 세가지 오버로드

  ```swift
  1. Sequence.flatMap<S>(_: (Element) -> S) -> [S.Element]
      where S : Sequence
  2. Optional.flatMap<U>(_: (Wrapped) -> U?) -> U?
  3. Sequence.flatMap<U>(_: (Element) -> U?) -> [U]
  ```

* 3번 오버로드: 두가지 방식으로 잘 못 사용될 수 있음

  * 추가적인 래핑과 언래핑

    ```swift
    struct Person {
      var age: Int
      var name: String
    }
    
    let flatMappedAges = people.flatMap { $0.age } // prints: [21, 17, 20]
    let mappedAges = people.map { $0.age } // prints: [21, 17, 20]  
    ```

    * `flapMap(_:)`  대신 `map(_:)`을 사용해 불필요한 래핑과 언래핑을 피할 수 있음

  * `Collection` 프로토콜을 순응하는 `String`

    ```swift
    let names = people.flatMap { $0.name }
    // 4.0 이전 버전에서의 동작: ["Osame", "Masoud", "Mehdi"]
    // 4.0 버전부터의 동작: ["O", "s", "a", "m", "e", "M", "a", "s", "o", "u", "d", "M", "e", "h", "d", "i"]
    ```

    * Swift 4.0부터 `String`이 `Collection` 프로토콜 순응하게 되면서 3번 오버로드 대신 1번 오버로드로 동작
      * `Collection` 프로토콜은 `Sequence` 프로토콜을 상속

* 이렇듯 논란의 여지가 많은 `flatMap(_:)`의 세번째 오버로드(`Sequence.flatMap`)를 deprecated

* 같은 기능을 수행하지만 함수의 의도를 더 잘 설명하는 새로운 이름 `compactMap(_:)`으로 재도입됨

### 참고 학습 자료

* [Apple Developer Documentation - flatMap(_:)](https://developer.apple.com/documentation/swift/sequence/2905332-flatmap)
* [Apple Developer Documentation - flatMap(_:) (Deprecated)](https://developer.apple.com/documentation/swift/sequence/2907182-flatmap)
* [Apple Developer Documentation - compactMap(_:)](https://developer.apple.com/documentation/swift/sequence/2950916-compactmap)
* [Swift Programming Language Evolution - Introduce Sequence.compactMap(_:)](https://github.com/apple/swift-evolution/blob/master/proposals/0187-introduce-filtermap.md)
* [Stack Overflow - Difference between flatMap and compactMap in Swift](https://stackoverflow.com/questions/49291057/difference-between-flatmap-and-compactmap-in-swift)