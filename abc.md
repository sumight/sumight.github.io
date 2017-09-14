# css 组件化

## 首先需要考虑的一些问题

- 组件在使用的过程中需要设置不同的尺寸，以及间距
- 组件可能会有不同的表现形式，比如反色，情景等
- 一些全局的样式可能会影响到组件
- 组件的可能是作为一个容器，在内部会插入其他内容
- 组件需要被用户直接使用
- 组件需要在一些功能组件（比如vue组件）中被复用

## 组件 API

- 组件的名字: 标识一个独立的组件
- 组件的属性: 决定组件的的不同表现形式
- 组件的组成元素: BEM 中的 element

### 几种 API 风格


- class

```html
<div class="is-button"><div>
<div class="is-button color-danger size-big"><div>
```

- 自定义标签 *

```html
<ui-button>按钮</ui-button>
<ui-button color="danger" size="big">按钮</ui-button>
```

- 自定义属性

```html
<div data-is="button"><div>
<div data-is="button" data-prop-color="danger" data-prop-size="big"><div>
```

为什么选择自定义标签的API风格 ？

下面的例子中采用 API 风格

### 多元素组件

```html
<ui-detail-list>
  <ul>
    <li>...</li>
    <li>...</li>
    <li>...</li>
  </ul>
<ui-detail-list>
```

```html
<ui-select-list>
  <div>...</div>
  <a>...</a>
<ul-select-list>
```

### 将状态定义到根节点上

## 原生html元素的位置

自定义的组件不应该和原生的元素混淆，原生元素保留原有的语义，和自定义组件平别，或者作为组件的组成部分

### 作为组件的组成部分的时候应该任然保留原有的语义

- div 组件中的块状区域
- span 组件中的文本部分
- i 组件中的图标
- ul li 组件中的列表
- table 组件中的阵列
- a 组件中的链接
...

```html
<ui-menu>
<ul>
  <li><a> <i></i> <span></span> </a></li>
  <li><a> <i></i> <span></span> </a></li>
</ul>
</ui-menu>
```

## 屏蔽全局样式

组件是独立的，有可能会被放置到任何页面中，所以我们需要考虑组件不应该被全局的css所影响

可能出现的全局css
- font
- box-sizing

在组件中 我们应该覆盖这些可能的全局 css 属性

## 组件之间的嵌套

组件可能作为一个元素，也可能作为一个容器，当组件作为容器的时候，我们就应该考虑到，组件的选择器不应该影响到被嵌套的内容

比如下面的组件

```html
<ui-detail-list>
  <ul>
    <li>...</li>
    <li>...</li>
    <li>...</li>
  </ul>
<ui-detail-list>
```

选择器应该这样设计

```css
ui-detail-list > ul > li {
  ...
}
```

而不是

```css
ui-detail-list ul li {
  ...
}
```

## 尺寸

设计一个组件的时候，我们不应该假定一个最佳尺寸，组件的尺寸应该由使用者来决定。所以当我们编写组件样式的时候应该让组件的内容无论在何种尺寸下都能良好的呈现。

这里我们考虑两种情况

1. 当组件比较宽，出现空间闲置的时候，应该考虑组件的对齐方式，左对齐，右对齐，或者居中。
2. 当组件比较窄的时候，出现空间不足的时候，我们应该更加，情况进行内容的压缩，或者进行换行。

组件的样式应该能再上述情况发生的时候都能良好的表现。我推荐使用 flex 布局，因为它能很好的处理横向的布局情况。


