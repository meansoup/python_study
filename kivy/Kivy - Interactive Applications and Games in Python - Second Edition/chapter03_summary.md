
chapter 3
==========


����
----------
```
01 - id�� attribute ���� ���� ���� (.kv)
02 - touch event ���� comicwidgets��(py/kv) StickMan/DraggableWidgets�� ����
```

����
----------
```
id		.kv �������� ���� ������
		���� �� �տ� _�� ��������, �����ϱ� �������� �ʼ��� �ƴ�
attribute	� widget�� attribute�� �����ϰ�, id�� ���� �־��ָ� �� attribute�� ����
		commiccreator.kv�� ToolBox���� drawing_space attribute�� _drawing_space(id)�� ������ ������, python���� drawing_space�� ���⿡ ���� ����(ex/01)
		root�� ���� ��� (ex/01)
root		base widget in the rule hierarchy
self		current widget
app		the instance of the application
```

touch event
----------
```
mouse, finger touch, magic pen touch�� ����
�Ʒ� touch�� mouse, finger touch���� ����
on_touch_down	new touch start
on_touch_move	the touch is moved
on_touch_up		the touch ends
	-> �� touch event�� parameter(touch)�� ���� ������ ���� [MotionEvent](https://kivy.org/doc/stable/api-kivy.input.motionevent.html#kivy.input.motionevent.MotionEvent)�� ����
	-> return value�� hierarchy ������ parent���� touch event�� �Ű� ��� �ϴ°�/�ƴѰ��� �˷��ִ� ����(ex/02 - comicwidgets.py)
	-> �����ϰ� super.on_touch_~ ���� chidren�� event�� �Ű澵 �� ����

collide_point		��� widget�� app(coordinate space)���� �߻��ϴ� touch event(MotionEvent)�� ������, �� event�� Ư�� widget���� �߻��ϴ��� Ȯ���ϴ� �������� ���(ex/02 - comicwidgets.py)
```

* (ex/02) self.selected�� Line instance�� �־ ������ �� �ְ� ������ �κ� Ȯ��
* ```self.canvas```�� ���� canvas�� instructions�� ���� �� ����
* ```self.canvas.remove(self.selected)```�� ���� canvas�� self.selected�� ���� �� ����
* left corner�� ����� �ʰ�, ```(touch.x - self.width/2, touch.y - self.height/2)```