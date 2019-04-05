
chapter 3
==========


예제
----------
```
01 - id와 attribute 사용과 차이 구분 (.kv)
02 - touch event 사용과 comicwidgets의(py/kv) StickMan/DraggableWidgets의 관계
```

개념
----------
```
id		.kv 내에서만 접근 가능함
		보통 맨 앞에 _를 붙이지만, 구분하기 위함이지 필수는 아님
attribute	어떤 widget에 attribute를 생성하고, id를 여기 넣어주면 그 attribute로 접근
		commiccreator.kv의 ToolBox에서 drawing_space attribute는 _drawing_space(id)를 가지고 있으며, python에서 drawing_space로 여기에 접근 가능(ex/01)
		root도 동일 방식 (ex/01)
root		base widget in the rule hierarchy
self		current widget
app		the instance of the application
```

touch event
----------
```
mouse, finger touch, magic pen touch로 나눔
아래 touch는 mouse, finger touch에서 가능
on_touch_down	new touch start
on_touch_move	the touch is moved
on_touch_up		the touch ends
	-> 각 touch event는 parameter(touch)로 여러 정보를 갖는 [MotionEvent](https://kivy.org/doc/stable/api-kivy.input.motionevent.html#kivy.input.motionevent.MotionEvent)를 받음
	-> return value가 hierarchy 구조상 parent에게 touch event를 신경 써야 하는가/아닌가를 알려주는 역할(ex/02 - comicwidgets.py)
	-> 유사하게 super.on_touch_~ 으로 chidren의 event를 신경쓸 수 있음

collide_point		모든 widget이 app(coordinate space)에서 발생하는 touch event(MotionEvent)를 받지만, 그 event가 특정 widget에서 발생하는지 확인하는 보편적인 방법(ex/02 - comicwidgets.py)
```

* (ex/02) self.selected에 Line instance를 넣어서 삭제할 수 있게 구현한 부분 확인
* ```self.canvas```를 통해 canvas에 instructions를 넣을 수 있음
* ```self.canvas.remove(self.selected)```를 통해 canvas에 self.selected를 지울 수 있음
* left corner를 벗어나지 않게, ```(touch.x - self.width/2, touch.y - self.height/2)```