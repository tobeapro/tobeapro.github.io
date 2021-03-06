## flex布局使用

##### 布局的传统解决方案，基于盒状模型，依赖 display属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。

##### 2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

#### 兼容：ie10+和其他浏览器

### 一、flex	简介
flex意为“弹性布局”，任何容器都可以设置成flex布局。

注意:设为flex布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。

使用方法：如下，这样盒子就设置撑了弹性布局
```javascript
.box{
	display: -webkit-flex; //webkit内核前缀,本文后面为了简写不添加
	display:flex;
}
```

### 二、设置flex属性容器的主要属性

> flex-direction

> flex-wrap

> flex-flow

> justify-content

> align-items

> align-content

#### 2.1 flex-direction
`flex-direction`属性决定主轴上的方向（即子元素在盒子中的排列方向）
```javascript
.box{
	flex-direction:row (默认)| row-reverse | column | column-reverse;
}
```
![flex-direction](https://tobeapro.github.io/img/flex-direction.png)

#### 2.2 flex-wrap
`flex-wrap`属性决定在轴线上的如果排列不下的换行规则(默认不换行)
```javascript
.box{
	flex-wrap: nowrap(默认) | wrap | wrap-reverse;
}
```
![flex-wrap](https://tobeapro.github.io/img/flex-wrap.png)
#### 2.3 flex-flow
`flex-flow`属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
```javascript
.box {
  	flex-flow: <flex-direction> || <flex-wrap>;
}
```

#### 2.4 justify-content
`justify-content`属性定义项目在主轴上的对齐方式
```javascript
.box{
	justify-content: flex-start(默认) | flex-end | center | space-between | space-around;
}
```
 注意：如果主轴上的方向为`column/column-reverse`(此时横方向变成了交叉轴了，因此该属性无效,在下面会提到),项目会始终在左侧

![justify-content](https://tobeapro.github.io/img/justify-content.png)

#### 2.5 align-items
`align-items`属性定义项目在`交叉轴`上如何对齐
```javascript
.box {
  	align-items: flex-start| flex-end | center | baseline | stretch(默认);
}
```
>* flex-start：交叉轴的起点对齐。
>* flex-end：交叉轴的终点对齐。
>* center：交叉轴的中点对齐。
>* baseline: 项目的第一行文字的基线对齐。
>* stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

 注意：如果主轴上的方向为`column/column-reverse`,横方向就是交叉轴方向,联系上一条,要是设置项目的在横方向对其方式应该使用`align-items`
![align-items](https://tobeapro.github.io/img/align-items.png)

#### 2.6 align-content
`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用
```javascript
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch(默认);
}
```
>* flex-start：与交叉轴的起点对齐。
>* flex-end：与交叉轴的终点对齐。
>* center：与交叉轴的中点对齐。
>* space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
>* space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
>* stretch（默认值）：轴线占满整个交叉轴。

![align-content](https://tobeapro.github.io/img/align-content.png)

### 三、设置项目主要属性
> order

> flex-grow

> flex-shrink

> flex-basis

> flex

> align-self

#### 3.1 order
`order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
```javascript
.item {
  order: 0(数字,默认为0)
}
```
#### 3.2 flex-grow
`flex-grow`属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
```javascript
.item {
  flex-grow: 0(数字,默认为0)
}
```
注意：如果所有项目的`flex-grow`属性都为`1`，则它们将`等分`剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为`2`，其他项目都为`1`，则前者占据的剩余空间将比其他项`多一倍`。
#### 3.3 flex-shrink
`flex-shrink`属性定义了项目的缩小比例(值越大缩的越小)，默认为1，即如果空间不足，该项目将缩小
```javascript
.item {
  flex-shrink: 1(数字,默认为1)
}
```
注意：如果所有项目的`flex-shrink`属性都为`1`，当空间不足时，都将等比例`缩小`。如果一个项目的`flex-shrink`属性为`0`，其他项目都为`1`，则空间不足时，前者`不缩小`。
负值对该属性无效。
#### 3.4 flex-basis
`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
```javascript
.item {
  flex-basis: <length> | auto(默认);
}
其实相当于设置width
```
#### 3.5 flex
`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选
```javascript
.item {
  flex: 0 1 auto(默认) | [ <'flex-grow'> <'flex-shrink'> <'flex-basis'> ]
}
```
该属性有两个快捷值：`auto (1 1 auto)` 和 `none (0 0 auto)`。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
#### 3.6 align-self
`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。
```javascript
.item {
  align-self: auto(默认) | flex-start | flex-end | center | baseline | stretch;
}
```