# 접근제어

```
다른 소스 파일이나 모듈에서 특정 코드로 접근하는 것을 제한
```

### 모듈과 소스 파일

* 모듈 (Module)
  * 코드를 배포하는 단일 단위
  * `import` 키워드를 사용해 다른 모듈에 import 될 수 있음
  * 각 빌드 타겟은 별도의 모듈로 취급
* 소스 파일 (Source file)
  * 모듈 내 단일 소스 코드 파일

### 접근 레벨 (Access Level)

| Open access       | Private access   |
| ----------------- | ---------------- |
| Highest           | Lowest           |
| Least restrictive | Most restrictive |

* `Open access` & `Public access`: 선언된 모듈이나 선언된 모듈을 import한 다른 모듈에서 사용될 수 있음
  * `Open access`: 다른 모듈에서 서브클래싱이나 오버라이드가 가능
    * 클래스나 클래스 멤버에만 적용 가능
  *  `Public access`: 다른 모듈에서 서브클래싱이나 오버라이드 불가능
* `Internal access`: 선언된 모듈 내 전체 소스 파일에서 사용될 수 있음 (기본 접근 레벨)
* `File-private access`: 선언된 소스 파일 내에서만 사용될 수 있음
* `Private access`: enclosing declaration (선언된 괄호) 및 **같은 파일**의 extension 내에서만 사용될 수 있음

### 접근 레벨 원칙 (Guiding Principle of Access Levels)

특정 엔티티를 그보다 더 낮은 접근 레벨을 가진 다른 엔티티에 선언해 사용할 수 없음

* `public` 변수는 `internal`, `file-private`, `private` 타입에서 선언될 수 없음
* 함수는 그 매개변수나 리턴 타입 보다 높은 접근 레벨이어선 안됨

### 왜 사용하는가

* 코드의 세부 구현을 감출 수 있음
* `private` 키워드 사용: 다이나믹 디스패치를 줄여 퍼포먼스 향상
  * 다이나믹 디스패치: 메소드 오버라이딩이 되어있는 경우 실행시점에 어떤 메소드를 실행할 지 결정되는 것 (출처: [위키백과](https://ko.wikipedia.org/wiki/동적_디스패치))
  * 다이나믹 디스패치는 언어의 표현성을 향상 시키지만 간접적으로 사용되는만큼 런타임 시 오버헤드도 증가시킴
  * `final` 키워드처럼 간주되어 메소드나 프로퍼티에 접근하기 위한 간접적 호출을 제거

### 참고 학습 자료

* [The Swift Programming Language - Access Control](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)
* [Swift Blog - Increasing Performance by Reducing Dynamic Dispatch](https://developer.apple.com/swift/blog/?id=27)

