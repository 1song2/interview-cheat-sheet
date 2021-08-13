# 스토리보드를 이용했을 때의 장단점

### 장점

* 비주얼라이제이션
  * 결과물 예측이 쉬움
  * 많은 양의 코드 작성 없이 디자인 및 플로우를 목업으로 볼 수 있음
* 비기너도 비교적 쉽게 사용할 수 있음 (= 직관적이다)
  * Attributes inspector 등으로 속성값을 외울 필요 없이 편하게 선택 가능
  * 드래그 앤 드랍으로 엘리먼트를 배치하거나 씬을 연결
  * 사실 코드로 커스텀 UI나 Constraint를 짜는 것은 상당히 지치는 일
* 프로토타이핑이 간단

### 단점

* 협업이 어려움
  * merge 시 충돌 (스토리보드 분리로 약간을 줄일 수 있겠으나 완전한 해결책은 아님)
  * 코드 리뷰가 어려움: diff로 파악이 힘듦
* View controller간 데이터 전달이 용이하지 않음
  * `prepareForSegue()`에 의존
* 화면 로딩이 무거움 (스토리보드 분리로 약간은 해결 가능)
* 앱의 사이즈가 증가할수록 가독성이 떨어짐
* 재사용성이 떨어짐

### 결론

* 스토리보드는 프로젝트 규모가 작고, 비교적 간단한 앱을 개발할 때, 개발자 수가 많지 않을 때 사용할 수 있겠다.

### 참고 학습 자료

* [Mobindustry Blog - Pros and Cons of Working with Storyboards](https://www.mobindustry.net/pros-and-cons-of-working-with-storyboards/)