
chapter 2
==========


����
----------
```
01 - canvas �׸��� ����� ���� ����(Triangle ~ Mesh)
02 - line�� ��, �ﰢ��, �簢�� ������ �׸��� ����
03 - �̹����� ����
04 - canvas.after
05 - �̵�, ȸ��
```

����
----------
```
coordinate space �� ���ѵ��� ������, bottom-left corner of the screeon�� origin���� ��

canvas	widget�� vector shape�� �׸� �� ����
		canvas�� �׸��°� �ƴ϶�, canvas�� coordinate space�� �׸��� ��ɵ��� ����
		��� widget�� ���� Canvas�� ����.
		��� widget�� ������ coordiante space�� ����
		coordiante space�� windows�� screen size�� ���ѵ��� ����

canvas�� canvas.before, canvas, canvas.after�� �� ��ü�� ����. canvas.after�� ���� �������� ȣ��Ǿ� �ٸ� widget�� ���� ������.(ex/04)

vertax instruction
	inherit from the VertexInstruction. ��� �׸� ������ ���� ��.
	VertexInstruction�� ����ϱ� ������ pos, size�� Widget�Ŷ� �ٸ�. fixed value�� �����
context instruction
	inhefit from the CntextInstruction. ���, ��� �׸����� ���� ��. (Color, Rotate, Translate, Scale)
```

vertax instruction
----------
```
Rectangle
Ellipse		��ä�� ���� ��. 0���� 12��
		angle_start, angle_end �� ��ä���� �׸� �� ����
		segments �� �� ���� ������ ���� �׸������� ���� ��. �������� ������ ���� �׷��� ��Ȯ�� ���̰�����, default=180, segments : 3���� �ϸ� �ﰢ��(ex/01)
Triangle	x,y points 3�� -> �ﰢ��
Quad		points 4�� -> �簢��
Line		points 2�� -> �� (2���� ���� ���� ���� �� �׸� �� ����)
Point		points 1�� -> �� (���� ���� ���� �� ���� �� ���� ex/01)
Bezier		�. points�� attractors�� ���. (math formalism.. ������)
		dash_length �� ������ ����, dash_offset �� ���� ������ �Ÿ�
Mesh		�ﰢ���� �������� �̷������, ������ ������
```

context instruction
----------
```
source: 'kivy.png'	�̹����� ���� �� ����
Color: rgba:		color ���� ����
			�̹����� �ִٰ� �ص�, �̹����� �ش� �÷��� ���� ��(ex/03)
Rotate: angle:	ȸ��
           axis:		� ������ ���� ���� ����(ex/05)
Translate: x: or y:	�̵�. ȸ�� ���¶��, x, y�� ������ �ݴ밡 ��
Scale: xyz:		�� �࿡ ���� size�� ������ ����
			0.5�踦 �ߴٸ�, ���󺹱��� ���ؼ� 2�踦 ����� ��

* Color, Rotate, Translate, Scale�� ��� �����ϸ� �� �������� coordinate space�� ������ ��� ��ħ.
* ��� ������ ȸ���ϱ� ���ؼ� RelativeLayout �������� �����ϸ� ��. RelativeLayout�� ���������� widget�� position ���� �����ϱ� ����

```