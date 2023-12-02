


### 사용자와의 인터렉션과정
1. 사용자로부터 입력/이벤트를 받는 과정
2. 내부적으로 이 이벤트에 대한 처리를 하는 과정
3. 처리된 정보를 사용자에게 보여주는 과정

디자인 패턴 -> 이 과정을 어떤 식으로 처리할 것인가에 대한 고민.

전통적인 MVC 패턴


![Traditional MVC](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/traditional_mvc.gif
)


https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/traditional_mvc.gif

사용자가 View를 동작해 event를 발생시킨다.
Controller는 event를 받아 처리한다.
이때, 이 처리한다는 것은 Model의 상태를 변경을 요청하는 것일 수도 있고, View의 외형이나 동작의 변경을 요청하는 것일 수도 있다. (Controller는 View - Model 둘다 영향 가능)
Model는 상태가 바뀌게 되면 Observer로 등록된 모든 객체에게 알리는데, observer에 view가 있다면, view의 외형을 바꾸는 구현일 수도 있다.

View: 유저의 입력과 이벤트가 생기는 곳
Controller: 이벤트와 액션에 대해서 전달 받아, 뷰 혹은 모델이 바뀌게 한다.
Model: 데이터에 대한 처리 -> View에 전달

가장 큰 차이 - View와 모델은 열결되어 있다.
뷰가 변할 때, 컨트롤러를 거치지 않아도 된다. (뷰와 모델이 서로 의존하는 관계이다.)


스위프트에서 사용한 CocoaMVC


view와 Model에 컨트롤러가 있다.

View : 유저의 이벤트를 받고, 데이터를 표시하고, 이벤트가 일어나면 Controller에 전달
Controller: 모델을 통해서 데이터 업데이트, 그 결과를 View에 전달
Model: 


![Cocoa MVC](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/cocoa_mvc.gif)
