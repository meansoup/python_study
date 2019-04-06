
# chapter 3

# 예제

1. id와 attribute 사용과 차이 구분 (.kv)
2. touch event 사용과 comicwidgets의(py/kv) StickMan/DraggableWidgets의 관계
3. localizing coordinates
4. drawing_space로의 접근과 python을 import하는 상황

# 개념

* **id**
  * .kv 내에서만 접근 가능함
  * 보통 맨 앞에 _를 붙이지만, 구분하기 위함이지 필수는 아님
* **attribute**
  * 어떤 widget에 attribute를 생성하고, id를 여기 넣어주면 그 attribute로 접근
  * commiccreator.kv의 ToolBox에서 drawing_space attribute는 _drawing_space(id)를 가지고 있으며, python에서 drawing_space로 여기에 접근 가능(ex/01)
  * root도 동일 방식 (ex/01)
* **root**: base widget in the rule hierarchy
* **self**: current widget
* **app**: the instance of the application

## Touch event

touch event는 mouse, finger touch, magic pen touch으로 나뉘며, 아래 event는 mouse, finger touch에서 사용 가능하다.
  
* **on_touch_down**: new touch start
* **on_touch_move**: the touch is moved
* **on_touch_up**: the touch ends
  * 각 touch event는 parameter(touch)로 여러 정보를 갖는 [MotionEvent](https://kivy.org/doc/stable/api-kivy.input.motionevent.html#kivy.input.motionevent.MotionEvent)를 받음
  * return value가 hierarchy 구조상 parent에게 touch event를 신경 써야 하는가/아닌가를 알려주는 역할(ex/02 - comicwidgets.py)
  * 유사하게 super.on_touch_~ 으로 chidren의 event를 신경쓸 수 있음

* **collide_point**는 모든 widget이 app(coordinate space)에서 발생하는 touch event(MotionEvent)를 받지만, 그 event가 특정 widget에서 발생하는지 확인하는 보편적인 방법(ex/02 - comicwidgets.py)

## dynamic create/deleate canvas

* ```self.selected```에 Line instance를 넣어서 삭제할 수 있게 구현한 부분 확인 (ex/02)
* ```with self.canvas```를 통해 canvas에 instructions를 넣을 수 있음
* ```self.canvas.remove(self.selected)```를 통해 canvas에 self.selected를 지울 수 있음
* to_parent로 부모의 coordinate에 접근
  * DraggableWidget의 parent(drawing space)의 범위 조건 체크를 위해 사용(ex/02 - comicwidgets.py)
* left corner를 벗어나지 않게, ```(touch.x - self.width/2, touch.y - self.height/2)```

## localizing coordinates

to_parent 같이, 현재 widget에서 구현하지만, 움직일 공간이 parent, 혹은 parent's parent와 같은 경우 coordinates의 범위를 지정해주는 것.  
RelativeLayout은 coordinate의 위치 값들이 다 다르니까.  
RelativeLayout이 아닌 layout들은 그 상위에 대해 절대적인 coordinate 값을 가지고 있음.

* **to_parent()**: transform relative coordinates inside RelativeLayout to the parent of RelativeLayout
* **to_local()**: transform the coordinates of parent of RelativeLayout to RelativeLayout
* **to_window()**: transform the coordinates of the current widget to absolute coordinate with respect to the window
* **to_widget()**: transform the absolute coordinates to coordinates within the parent of the current widget

* ```self.parent.drawing_space```를 통해 ToolButton에서 parent(ToolBox)의 drawing_space attribute에 접근 (ex/04)
* ```add_widget()```으로 layout에 widget을 더해줌 (ex/04 - toolbox.py)
* [```#:import toolbox toolbox```](https://kivy.org/doc/stable/guide/lang.html#special-syntaxes)으로 toolbox를 .kv에 import 함. (ex/04)
  * comiccreator.py에서 comiccreator.kv를 사용하고(kv에서 자동으로), commiccreator는 toolbox.kv를 사용하므로(내부적으로 사용하며, .py에서 Builder.load_file로 load), toolbox.py는 자동으로 호출되지 않아, import 필요.  
  즉, toolbox.py가 main이었다면 import를 안해도 .kv를 가져갔겠지만, toolbox가 main이 아니라 사용되는 상황에서, .py를 import 해줘야 했음.
