# BFC布局的理解
### 一、触发条件  

- **float**属性不为none.
- **position**属性不为static和relative.
- **display**属性为下列之一:table-cell,table-caption,inline block,flex,or inline-flex.
- **overflow**属性不为visible。 

### 二、BFC布局规则： 

	a.内部的Box会在垂直方向，一个接一个地放置。
	b.Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
	c.每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
	d.BFC的区域不会与float box重叠。
	e.BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
	f.计算BFC的高度时，浮动元素也参与计算 
### 三、BFC布局作用
- 1.利用BFC可以消除外面距塌陷
- 2.用于清除浮动
- 3.利用BFC阻止文本换行
