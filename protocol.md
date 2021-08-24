# Protocol

특정 태스크나 기능에 필요한 메소드, 프로퍼티 등 요구사항의 청사진을 정의

### Adopt vs. Conform

* Adopt(채택): 타입 이름 뒤 콜론(:)과 프로토콜 이름을 기재 (마치 상속처럼)
* Conform(순응, 준수): 어떤 타입이 프로토콜의 요구 사항을 충족하는 것을 프로토콜을 따른다, 순응한다고 이야기 함

### 프로토콜 문법

```swift
protocol SomeProtocol {
    // protocol definition goes here
}
```

```swift
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}
```

### 프로퍼티 요구사항 (Property Requirements)

* 프로퍼티 이름, 타입,  gettable 혹은 gettable and settable한지 명시
* 프로퍼티 요구사항은 항상 변수로 선언됨 (`var`)
* `{ get set }`: 상수 저장 프로퍼티(constant stored property)나 읽기 전용 연산 프로퍼티(read-only computed property)로는 만족되지 않음
* `{ get }`: 어떤 종류의 프로퍼티든 상관 없이 만족됨 (settable한 프로퍼티도 가능)
* 타입 프로퍼티 요구사항은 `static` 키워드와 함께 기재

### 메소드 요구사항 (Method Requirements)

* 함수명, 파라미터, 리턴 타입을 명시 (메소드 바디는 작성하지 않음)
* 가변 매개변수(variadic parameters)는 허용되지만 매개변수 기본값은 프로토콜 정의부에서 사용할 수 없음
* 타입 메소드 요구사항은 `static` 키워드와 함께 기재
* 변경 가능한 메소드 요구사항 (Mutating Method Requirements)
  * 메소드가 자신이 속한 인스턴스를 변경할 수 있음을 `mutating` 키워드로 표시
  * 프로토콜을 채택한 클래스에서 메소드를 구현할 때는  `mutating` 키워드를 생략

### 초기자 요구사항 (Initializer Requirements)

* 클래스에서 초기자 요구사항을 구현할 땐 `required` 수식어를 붙여주어야 함

  ```swift
  class SomeClass: SomeProtocol {
      required init(someParameter: Int) {
          // initializer implementation goes here
      }
  }
  ```

### 타입으로서의 프로토콜

* Cf. 프로토콜을 타입으로 사용하는 것을 *existential type*이라고 하기도 함

* 함수, 메소드, 이니셜라이저의 매개변수 타입이나 리턴 타입

* 상수, 변수, 프로퍼티의 타입

* 배열, 딕셔너리 등 컨테이너 내 아이템의 타입

* `is`, `as?`, `as!` 등 사용해 프로토콜 준수를 체크할 수 있음

* 프로토콜 합성(Protocol Composition): 여러 프로토콜을 동시에 따르는 타입을 임시의 로컬 프로토콜처럼 사용할 수 있음 (새로운 프로토콜 타입을 정의하는 것은 아님)

  ```swift
  protocol Named {
      var name: String { get }
  }
  protocol Aged {
      var age: Int { get }
  }
  func wishHappyBirthday(to celebrator: Named & Aged) {
      print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
  }
  ```

### 위임 (Delegation)

* 클래스 혹은 구조체의 책임을 다른 타입의 인스턴스에 위임할 수 있게 하는 디자인 패턴
* 위임된 책임을 캡슐화하는 프로토콜을 정의함으로써 구현

### 프로토콜 채택으로 Synthesized Implementation 사용

* `Equatable`, `Hashable`, `Comparable`를 위한 프로토콜 순응을 자동으로 제공
* 프롵토콜 요구사항을 구현하기 위한 반복적인 보일러플레이트 코드를 작성할 필요가 없음 (`==`, `hash(into:)`, `<`)
* 조건을 만족하는 경우에 한함

### 프로토콜 확장 (Protocol Extensions)

* 기본 구현 제공: 메소드나 연산 프로퍼티의 요구사항을 구현하기 위해 사용 가능
  * 타입 내에서 따로 자체 구현한 내용이 있으면 기본 구현 대신 자체 구현을 사용

### 프로토콜 네이밍 (Protocol Naming Convention)

* 명사형: 어떤 것인지 기술하는 프로토콜 (e.g. `Collection`)
* 접미사형(`able`, `ible`, `ing`): 능력을 기술하는 프로토콜 (e.g. `Equatable`, `ProgressReporting`)

### 참고 학습 자료

* [The Swift Programming Language - Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)
* [API Design Guidelines - Strive for Fluent Usage](https://swift.org/documentation/api-design-guidelines/#strive-for-fluent-usage)