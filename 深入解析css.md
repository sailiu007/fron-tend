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
 
 使用 vw 定义字号 `:root { font-size: **calc**(0.5em + 1**vw**);}`

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

3.2 元素高度的问题

给容器设置 display: flex，它就变成了一个弹性容器(flex container)，子元素默认等高。 你可以给子元素设置宽度和外边距，尽管加起来可能超过 100%，Flexbox 也能妥善处理。

