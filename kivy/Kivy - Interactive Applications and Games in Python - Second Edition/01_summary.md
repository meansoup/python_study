kivy - interactive applications and games in python second edition
==========
[parctice code](https://www.packtpub.com/support)

* kivy
Android, iOS, Linux, windows, Mac OS ���� ����
�ٽ� �κ��� Cython���� �����ϰ� ��κ��� �׷��� ������ directly GPU�� �����Ͽ� �ӵ��� ����

Chapter 1
----------

## ����
01_03 - �̷��� widget�� personalize �� �� ����. py�� �ش� ���� Ŭ���� ����
01_04 - �̷��� widget�� ����Ͽ� ����� �� ����. MyButton@Button
01_05 - layout �� Ư�� Ȯ�� ����
01_06 - <Layout>���� base class�� ��������� ��ü ���밡��
01_07 - pagelayout
01_08 - kv ���ϵ��� Builder.load_file �� ����ϴ� �� kv Ȱ��
----------


* FooApp class �� �ڵ����� foo.kv�� ����� (FooApp class�� ���� ���� ���� ��� ����)

* ����
```
widget		kivy GUI component. the minimal graphical units.
property	widget�� �Ӽ� �� �ϳ� (ex/ text)
self		�ڱ� �ڽ�
root		���� �ֻ���
id		.kv���� �ٸ� �������� ������ �� �ֵ��� �ϴ� ��

property
		x, right, center_x
		y, top, center_y
		width, height�� �� self, root�� ���� �� �� ����
	
		size_hint - 0~1 �� ���� ũ��
			size_hint_x, size_hint_y
		pos_hint - 0~1 �� ���� ��ġ	
```

*layout
1. FloatLayout
	size_hint, pos_hint�� â�� ���� �����α���
2. RelativeLayout
	FloatLayout�� �����ѵ�, layout�� ���� ������ ����
3. GridLayout
	��� ���� layout ����
4. BoxLayout
	���γ� ���η� �״� ����
5. StackLayout
	BoxLayout�� �����ѵ�, ��� �������� �״� ����
6. ScatterLayout
	RelativeLayout�� �����ѵ�, rotating, scaling, translating�� ���� ��Ƽ��ġ ���
7. PageLayout
	��Ƽ������ ����Ʈ�� �ְ�, ���� �ٸ� layout���� ���ο� widget���� ���
	swipe_threshold - ��� ������ŭ ��ܾ� �������� �Ѿ����