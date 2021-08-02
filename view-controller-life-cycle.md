# View Controller의 Life Cycle

### UIViewController 주요 콜백

```
❓왜 콜백 메소드라 부를까?
: 내가 직접 호출하는 것이 아니라 시스템이 호출하는 것이기 때문
```

![View Controller Life Cycle Image](https://camo.githubusercontent.com/5845ad0978a51a2fc4c385c171bf316d66a3c3951415df9bea3a72869175fd93/687474703a2f2f692e737461636b2e696d6775722e636f6d2f67313966772e706e67)

cf. `func loadView()`: Creates the view that the controller manages.
`You override this method only in case you want to build the whole interface for the view controller from code.`

* `func viewDidLoad()`: Called after the controller's view is loaded into memory.
  * view controller의 lifetime 중 한번만 불림!
  * Usually override this method to perform additional initialization on views.
  * 이 단계에서 view bounds는 아직 최종 결정되지 않음 (`viewWillLayoutSubViews`에서 결정됨)
* `func viewWillAppear(Bool)`: Notifies the view controller that its view is about to be added to a view hierarchy.
* `func viewDidAppear(Bool)`: Notifies the view controller that its view was added to a view hierarchy.
* `func viewWillDisappear(Bool)`: Notifies the view controller that its view is about to be removed from a view hierarchy.
* `func viewDidDisappear(Bool)`: Notifies the view controller that its view was removed from a view hierarchy.

뷰가 나타나고, 사라지고라고 표현할 수도 있지만 뷰계층에 추가되고, 뷰계층에서 제거되고라고 표현하면 좀 더 팬시하지 않을까 😇

### [View 관련 상태 변화](https://developer.apple.com/documentation/uikit/uiviewcontroller)

![Valid State Transitions](https://docs-assets.developer.apple.com/published/f06f30fa63/UIViewController_Class_Reference_2x_ddcaa00c-87d8-4c85-961e-ccfb9fa4aac2.png)

### 참고 학습 자료

* [Apple Developer Documentation - UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller)
* [CodePath iOS guides - View Controller Lifecycle](https://github.com/codepath/ios_guides/wiki/View-Controller-Lifecycle)

