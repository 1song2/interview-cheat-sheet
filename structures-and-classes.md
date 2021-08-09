# Struct와 Class

<table>
  <tr>
    <td>Struct</td>
    <td>Class</td>
  </tr>
  <tr>
    <td colspan="2">값을 저장하기 위한 프로퍼티 선언<br>기능을 제공하기 위한 메서드 선언<br>서브스크립트로 접근할 수 있는 문법 지원<br>초기 상태를 위한 초기화 메서드 제공<br><br>기능 확장 가능 (extension)<br>특정 표준 기능을 제공하기 위해 프로토콜 순응 (conform)</td>
  </tr>
  <tr>
  	<td>상속 불가</td>
    <td>상속 가능<br>상위/하위 클래스 타입으로 형변환(type casting)</td>
  </tr>
  <tr>
  	<td>-</td>
    <td>소멸함수(deinitializer)에서 불필요한 리소스를 해제</td>
  </tr>
  <tr>
  	<td>의미있는 값 (Value semantic) (Direct)</td>
    <td>의미있는 레퍼런스 (Reference semantic) (Indirect)</td>
  </tr>
  <tr>
  	<td>-</td>
    <td>클래스 인스턴스에 하나 이상의 참조가 가능 (인스턴스별 참조 개수 관리 필요)</td>
  </tr>
  <tr>
  	<td>멤버와이즈 생성 함수 제공</td>
    <td>-</td>
  </tr>
</table>

### 값 타입 (Value Type)

* Call by value
* 구조체(Structure)와 열거형(Enumeration)
* 변수나 상수에 할당되거나 함수에 인자로 전달될 때 값이 복사가 됨
  ![../_images/sharedStateStruct_2x.png](https://docs.swift.org/swift-book/_images/sharedStateStruct_2x.png)
* Copy on Write: `Array`, `Dictionary`, `String`은 복사본에 변경이 생기기 직전 실제 복사가 일어남 (즉시 복사본이 생기는 것이 X)

### 참조 타입 (Reference Type)

* Call by reference
* 변수나 상수에 할당되거나 함수에 인자로 전달될 때 값이 복사되지 않고 참조됨
  ![../_images/sharedStateClass_2x.png](https://docs.swift.org/swift-book/_images/sharedStateClass_2x.png)
* 인스턴스를 저장하지 않고 참조하기 때문에 상수임에도 프로퍼티를 변경하는 것이 가능
* 식별 연산자(identity operators)로 상수나 변수가 같은 인스턴스를 참조하고 있는지 비교 (`===`, `!==`)
  * Class에만 사용 가능
* Cf. 비교 연산자(equivalence operators)는 인스턴스의 값이 같은 비교 (`==`, `!=`) → 커스텀 타입은 무엇을 기준으로 두 인스턴스가 같게 되는지 직접 정해줘야 함
  * Struct, Class 모두 사용 가능

### Value Types Reference

* Call by reference
* 값 타입을 참조 타입처럼 사용 (`inout`, `&`)
* 꼭 필요한 상황이 아니라면 사용하지 않는 것이 좋음

### 어떤 기준으로 선택해 사용할 것인가?

#### 구조체를 선택하는 경우

* 일단 구조체를 먼저 고려해라
  * 구조체는 값 타입이므로 변화가 변화가 일어난 부분만 보면 됨
* 데이터의 아이덴티티를 다루지 않는 경우는 구조체를 선택해라
  * 리모트 데이터 베이스 사용
* 프로토콜과 함께 구조체를 선택해라
  * 프로토콜 상속과 구조체를 사용함으로써 일종의 클래스 상속과 같은 효과

#### 클래스를 선택하는 경우

* Objective-C 호환성(상호운용성)이 필요한 경우 클래스를 선택해라
  * Objective-C API나 Objective-C framework
* 데이터의 아이덴티티를 다뤄야 하는 경우 클래스를 선택해라
  * 예시) 파일 처리, 네트워크 연결, CBCentralManager, 로컬 데이터 베이스 연결

### 참고 학습 자료

* [The Swift Programming Language - Structures and Classes](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html)
* [Apple Developer Documentation - Choosing Between Structures and Classes](https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes)