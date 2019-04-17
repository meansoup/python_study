
# chapter 4

# 예제

1. Screen과 ScreenManager의 사용
2. color가 하위에까지 영향을 미치는 것
3. color를 동적으로 setting

# 개념

## ScreenManager

ScreenManager는 여러 device에서 screen을 적절하게 조절할 수 있게 해준다.  
multiple screen을 갖도록 해주며 screen간 switch를 쉽게 해준다.
  * ScreenManager는 항상 `Screen` widget을 가져아하고, 다른 Widget을 가질 수 없음
    * ColorPicker를 `Screen` 하위에 놓음(ex/01 - comicscreenmanager.kv)
    * `Screen`으로 사용되는 곳에도 명시가 필요함
      * `ComicCreator`는 `ComicCreatorScreenManager`의 `Screen`으로 사용되고 있으며, 따라서 `ComicCreator@Screen`을 통해 Screen임을 명시함(ex/01 - comiccreator.kv)
    * `name` property를 `Screen`에 명시하여 screen을 변경할 수 있도록 함.
      * `root.current = 'comicscreen'`을 통해 comicscreen으로 switch 함. `root`는 여기서 ScreenManager 이고, `current`는 active screen 임
    * `Screen`은 `manager` attribute를 갖고, 이를 통해 접근할 수 있음
      * `current = 'colorscreen'`으로 colorscreen으로 switch 함.(ex/01 - generaloptions.py)  
      `comiccreator.kv`에서 각 항목들에 대해 id, root를 부여하는 이유
    * ComicScreenManager가 Screen들을 통제하게 되었기 때문에 최상위가 ComicScreenManager로 바뀌어야 하고, comiccreator.py에서 이렇게 변경된 것을 확인할 수 있음 (ex/01 - comiccreator.py)

## Color

  * 동적 coloring  
    `canvas.add`와 `with ---.canvas:`를 통해 color를 추가할 수 있음.(ex/03 - toolbox.py)  
      * ToolStickman의 경우 `canvas.before.add`를 사용하였는데, 이는 `Color` instruction이 `Stickman` Canvas에 추가한 다른 instructions보다 먼저 적용되게 하기 위함이다.  
      다른 ToolFigure에서 `before`를 사용하지 않는 것은 해당 canva의 order에 대한 권한을 가지고 있기 때문이다.
      * 소스상 color_picker.color를 가져다 사용하며, `*`를 통해 `colorpicker.color`의 list를 unpack 해줌.
        * 예를들면 (1, 0, 1) 을 unpack하여 1, 0, 1로 만듦
      * Color를 import해야 함
       
  * **ColorPicker**
    * 색상을 고르는 widget, 자리를 많이 차지하는 편. 예제상 보이는 colorpicker와는 상관 없는 API를 말하는 것으로 보임.
  * **[transision](https://kivy.org/doc/stable/api-kivy.uix.screenmanager.html#changing-transitions)**
    * screen을 switch 할 때 어떤 animation이 보이는가에 대한 것.

  * `load_file`은 .kv를 include하는 것이며, 이와 유사하게 `load_string`으로 .kv를 python file에서 사용할 수 있음(ex/02)

## stencilView
  특정 영역에만 이벤트를 처리하기 위해서 `collide_points`와 같은 방법을 사용했었는데, 이건 group mode나 resize 같은 상황에서 완벽하지 않다.  
  따라서 StencilView를 쓰는데, `StencilView`는 drawing area를 해당 view의 공간까지로 제한하며, 밖에 그려진 것들은 숨겨진다.
   * `drawingspace`를 제한하기 위해 `StencilView`를 상속하도록 함. `DrawingSpace(stencilView)` (ex/04 - drawingspace.py)  

  `StencilView`는 `RelativeLayout`이 아니므로, `StencilView` class는 relative coordinates를 사용할 수 없다.  
  즉, 여기서 사용한다면 상위의 RelativeLayout을 사용하게 되는 것이며, 일반적으로 drawing은 `relative coordinates`를 사용하는 것이 좋으므로 `RelativeLayout`안에 `DrawingSpace`을 사용하도록 한다.
   * 원래 `DrawingSpace(RelativeLayout)`으로 RelativeLayout을 상속하고 있었으므로, 위의 수정을 반영하면서 RelativeLayout으로 DrawingSpace를 감싸도록 함. (ex/04 - comiccreator.kv)
     * RelativeLayout에서 width, height의 설정과, DrawingSpace에서 default로 `size_hint: 1, 1`을 통해 동일한 area를 갖고 있음을 확인.

  원래 touch event에 대한 정의는, 어디서든 할 수 있는 것으로 보임(ch3에서 다루는)
   * `on_touch_down`을 보면, toolbox.py의 `ToolButton`에 정의되어 있지만, collide_point로 가리키고 있는 범위는 drawingspace이기 때문이다.  
   혼동되었던 개념인데, 관련한 touch event를 해당 클래스 함수에서 전 범위에 관해 정의하고 있다고 생각하면 될 것 같다.

   