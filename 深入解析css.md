# 第一部分 基础回顾

#### 1.1.4 两条经验法则
- 在选择器中不要使用 ID
- 不要使用`!important`

### 2.2 em 和 rem

一般会用 rem 设置字号，用 px 设置边框，用 em 设置 其他大部分属性，尤其是内边距、外边距和圆角。
- 1in（英尺） = 96px（像素）
- 1em 等于当前元素的字号
- rem 是相对于根元素的单位 `:root { font-size: 1em;}`

### 2.4 视口的相对单位

 vh、vw、vmin、vmax
 
 使用 vw 定义字号 `:root { font-size: calc(0.5em + 1vw);}`

### 2.6 CSS 变量
```css
  :root {
    --main-font: Helvetica, Arial, sans-serif;
    --brand-color: #369;
  }

  p {
    font-family: var(--main-font);
    color: var(--brand-color, blue);
  }
```

### 3.1 元素宽度的问题

box-sizing 的默认值为 content-box，这意味任何指定的宽或高都只会设置内容盒子的大小。将 box-sizing 设置为 border-box 后，height 和 width 属性会设置内容、内边距以 及边框的大小总和。
 ```css
    :root {
      box-sizing: border-box;
    }

    *,
    ::before,
    ::after {
      box-sizing: inherit;
    }
```

### 3.2 元素高度的问题

给容器设置 display: flex，它就变成了一个弹性容器(flex container)，子元素默认等高。 你可以给子元素设置宽度和外边距，尽管加起来可能超过 100%，Flexbox 也能妥善处理。

#### 3.2.3 使用min-height和max-height

#### 3.2.4 垂直居中内容

[howtocenterincss](http://howtocenterincss.com/)

### 3.5 容器内的元素间距

#### 3.5.2 更通用的解决方案:猫头鹰选择器

```css
    body * + * {
      margin-top: 1.5em;
    }
```
---

# 第二部分 精通布局

### 4.1 浮动的设计初衷

浮动能将一个元素(通常是一张图片)拉到其容器的一侧，这样文档流就能够包围它。这种布局在报纸和杂志中很常见，因此 CSS 增加了浮动来实现这种效果。

**双容器模式**: 通过将内容放置到两个嵌套的容器中，然后给内层的容器设置外边距，让它在外层容器中居中。
```css
    .container {
      max-width: 1080px;
      margin: 0 auto;
    }
```

### ~~4.2 容器折叠和清除浮动~~

浮动元素不同于普通文档流的元素，它们的高度不会加到父元素上。

清除浮动：
```css
    .clearfix::before,
    .clearfix::after {
      display: table;
      content: " ";
    }
    .clearfix::after {
      clear: both;
    }
```

### 5.1 Flexbox 的原则

给元素添加 display: flex，该元素变成了一个弹性容器(flex container)，它的直接子元素变成了弹性子元素(flex item)。**弹性子元素默认是在同一行按照从左到右的顺序并排排列**。弹性容器像块元素一样填满可用宽度，但是弹性子元素不一定填满其弹性容器的宽度。**弹性子元素高度相等，该高度由它们的内容决定**。

### 5.2 弹性子元素的大小

flex 属性是三个不同大小属性的简写:flex-grow、flex-shrink 和 flex-basis。只提供了 flex-grow 的值，剩下的两个属性是默认值(分别是 1 和 0%)，因此 flex: 2 等价于 flex: 2 1 0%。

### 5.5.2 整页布局

当浏览器加载内容时，它渐进渲染到了屏幕，即使此时网页的剩余内容还在加载。然后等到剩余内容加载完，浏览器会重新计算每个弹性子元素的大小，重新渲染网页。

对整页布局的时候使用网格布局。

## 6 网格容器

`display: grid`全是特性，不赘述，用时google。

### 7.1 固定定位

给一个元素设置 position: fixed 就能将元素放在**视口**的任意位置。

### 7.2 绝对定位

position: absolute 绝对定位是**相对于最近的非 static 定位的祖先元素**进行定位。如果找不到这样的祖先元素，那么会以 **文档的根元素**（<html> 或 body） 为参考点。（来自chatgpt，书上没有定语应该是错误的）

### 7.3 相对定位

当第一次给元素加上 position: relative 的时候，你通常看不到页面上有任何视觉改变。相对定位的元素以及它周围的所有元素，都还保持着原来的位置。如果加上 top、right、bottom 和 left 属性，**元素就会从原来的位置移走**，但是**不会改变它周围任何元素的位置**。

[The Shapes of CSS](https://css-tricks.cn/the-shapes-of-css/)

#### 7.4.1 理解渲染过程和层叠顺序

通常情况下(使用定位之前)，元素在 HTML 里出现的顺序决定了绘制的顺序。浏览器会先绘制所有非定位的元素，然后绘制定位元素。

#### 7.4.2 用z-index控制层叠顺序

### 7.5 粘性定位

没有搞懂用处，滑动时候怎么保证整个元素都能看到？

## 8 响应式设计

### 8.1 移动优先

#### 8.1.2 给视口添加meta标签

```html
 <meta name="viewport" content="width=device-width, initial-scale=1">
```
原来这一句的作用在这里，竟然是为了响应式设计...

### 8.2 媒体查询

```css
    @media (min-width: 35em) {
      .title > h1 {
        font-size: 2.25rem;
      }
    }
```

### 8.3 流式布局

---

# 第三部分 大型应用程序中的CSS

## 9 模块化 CSS

作者设计思路是BEM (Block, Element, Modifier)

目前更流行的CSS Modules、CSS-In—Js、Atomic CSS

[反对CSS-In—Js的声音](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b)

[StyleX](https://www.stylexjs.cn/)
