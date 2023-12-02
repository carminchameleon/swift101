


### 사용자와의 인터렉션과정
1. 사용자로부터 입력/이벤트를 받는 과정
2. 내부적으로 이 이벤트에 대한 처리를 하는 과정
3. 처리된 정보를 사용자에게 보여주는 과정

디자인 패턴 -> 이 과정을 어떤 식으로 처리할 것인가에 대한 고민.

전통적인 MVC 패턴


![Traditional MVC](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/traditional_mvc.gif
)


https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/traditional_mvc.gif

사용자가 View를 동작해 event를 발생시킨다.<br>
Controller는 event를 받아 처리한다.<br>
이때, 이 처리한다는 것은 Model의 상태를 변경을 요청하는 것일 수도 있고, View의 외형이나 동작의 변경을 요청하는 것일 수도 있다. (Controller는 View - Model 둘다 영향 가능)<br>
Model는 상태가 바뀌게 되면 Observer로 등록된 모든 객체에게 알리는데, observer에 view가 있다면, view의 외형을 바꾸는 구현일 수도 있다.<br><br>

View: 유저의 입력과 이벤트가 생기는 곳<br>
Controller: 이벤트와 액션에 대해서 전달 받아, 뷰 혹은 모델이 바뀌게 한다.<br>
Model: 데이터에 대한 처리 -> View에 전달<br>

가장 큰 차이 - View와 모델은 열결되어 있다.
뷰가 변할 때, 컨트롤러를 거치지 않아도 된다. (뷰와 모델이 서로 의존하는 관계이다.)

<br>
스위프트에서 사용한 CocoaMVC

<br>
view와 Model에 컨트롤러가 있다.

View : 유저의 이벤트를 받고, 데이터를 표시하고, 이벤트가 일어나면 Controller에 전달 <br>
Controller: 모델을 통해서 데이터 업데이트, 그 결과를 View에 전달 <br>
Model: 데이터를 정의하고, 데이터에 대한 동작을 수행

컨트롤러가 중재자, View와 Model은 서로 모른다.

![Cocoa MVC](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Art/cocoa_mvc.gif)


왜 애플에서는 전통적인 MVC를 사용하지 않고, Cocoa MVC로 수정하였는가?

우선 두가지의 차이점은 CocoaMVC에서는 Controller가 View와 Model의 중재자가 되게 하여, View와 Model이 분리되었다는 것입니다.<br>
View의 재 사용성을 강화하기 위해선 Model과 View를 분리하는 것이 가장 좋기 때문입니다.

Model은 우리가 무엇을 만드는지에 따라서 달라질 수 있다. 하지만, Model에 따라서 View가 달라진다면, View를 재사용하는 것이 어려워진다.<br>
그래서 애플에서는 View는 오직, Look & Feel을 구현하는 것에만 초점을 두었다.


UIView는 오로지 어떻게 화면을 그릴지에만 관심을 가지게 한다.<br>
: 비즈니스 로직이 어떻든지, 니가 만드는 앱이 뭐든지 간에, 우리가 가지고 있는 뷰는 그대로야. 너는 갖다가 쓰기만 하면 되거든.<br>
Toggle Button -> 말 그대로 토글이야.<br>
너가 토글을 가지고 데이터를 받아오든, 다크모드를 만들든 그건 너네가 알아서 해. <br>
근데 나는 우선 false는 이렇게 보여지고, true면 이렇게 보여져. 그리고 너네가 바꾸면 알려줄게.<br>
(알려주고, 알아서 하는 대상은 컨트롤러)<br>
<br>
데이터 셀에서도, 셀이 눌리면 어떤 작업을 해야 하는지, 셀 안에 어떤 텍스트를 넣어야 하는지, textfield 입력은 어떻게 처리해야 하는지 이런 것들은<br>
Delegate 혹은 DataSource Protocol을 사용해서 ViewController에 위임한다.<br>
<br>
UIKit에서는 UIView와 UIController가 강하게 결합되어 있다. <br>


###  MVP 와의 비교
Cocoa MVC와 함께 언급되는 것 중 하나가 MVP <br>
Presenter는 Model과 View의 중재자이기 때문에. (이론적으로는 비슷함)<br>
그러나, 차이점은 MVP에서 View와 Presenter는 강하게 결합되어 있지 않는다.<br>
Presenter는 UI를 모르는 존재가 되어야 하는, 별도로 존재하는 것이어야 한다.<br>
<br>
그래서 iOS에서 MVP로 구현을 한 다는 것의 의미는 ViewController + View - View이고<br>
Presenter는 별도로 구현 하는 것이다.


### 추가 _ 개인적인 생각
프론트엔드 개발자로 일할 때, 디자인 시스템을 직접 구축하면서 버튼, 토글, Search Bar, Multi Select Search Bar, 등등의 컴포넌트를 만들었었다.<br>
그때 정말 많은 UI컴포넌트 라이브러리들 (antd, material design, chakra ... 등등)을 참고했고, 그것을 따라서 구현해보았다.<br>
우리는 별 생각 없이 사용해온 것들을 직접 구현하는 과정에서 그 컴포넌트를 만들기 위해서 얼마나 많은 노력과 디테일이 필요한지를 알게 되었다. <br>
컴포넌트와 디자인 시스템은 사용자에게 보여지는 것을 만드는 개발과정에서 너무나도 중요한 요소라는 것을 알게 되었다.<br>

애플의 입장에서 프레임워크를 만들 때, 특히 UIkit을 만들 때에도 비슷한 맥락의 고민들이 있었을 것 같다.<br>
애플에서는 HGI가 있을 정도로, 최적의 사용자 경험을 추구하기 위해 정말 많은 고민을 한다는 것을 기반으로 생각해보면<br>

- 기본적인 컴포넌트를 자체적으로 디자인해서 제공함으로써 (물론 개발자가 만들 수 있지만 기본적으로 configuration 을 통해 제어하는 방식)
    - 최악의 디자인과 사용성이 나오는 것을 방지 (기본 컴포넌트만 써도 Looks good.)
    - 개발자들이 컴포넌트를 직접 구축하는 것을 대신 함 - 이건 우리가 열심히 고민해서 만들어놓았으니까 넌 유저들의 benefit을 주기 위한 개발에만 힘써
    (잘 만들어 놓았으니까, 잘 갖다 쓰기만 해 - React native와 비교해보면 디자인 라이브러리 갖다가 쓰는 제품도 많음.)
    - 그 자체적으로 이미 reusable하고 configurable 하기 때문에 네이티브 앱으로서 성능도 좋음.
