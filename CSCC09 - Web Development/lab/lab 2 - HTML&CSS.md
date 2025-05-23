---
tags:
  - code
  - language
---
- https://github.com/UTSC-CSCC09-Programming-on-the-Web/lab2-jieyinggong.git
- [[Week 1]]
---

## 一、HTML 与 CSS 基础

### HTML 是什么？

- **HTML（超文本标记语言）** 是构建网页结构的基础语言。
    
- 类似网页的骨架，定义页面的元素和语义结构（如标题、段落、图像、表单等）。
    
- 每个元素由标签包裹，例如：
    
    ```html
    <p>Hello World</p>
    ```
    

### HTML 常用语义标签分类

|类别|标签|说明|
|---|---|---|
|文本结构|`<p>`, `<h1>`~`<h6>`, `<blockquote>`|段落、标题、引用|
|布局容器|`<div>`, `<section>`, `<article>`, `<main>`, `<header>`, `<footer>`|页面结构划分|
|行内内容|`<span>`, `<strong>`, `<em>`, `<a>`|强调、链接、局部格式|
|媒体展示|`<img>`, `<video>`, `<audio>`, `<figure>`, `<figcaption>`|图片、视频、配图说明|
|表单交互|`<input>`, `<textarea>`, `<button>`, `<label>`, `<select>`|表单输入控件|

#### 图片插入方式对比

| 用法         | 适用场景  | 特点                      |
| ---------- | ----- | ----------------------- |
| `<img>` 标签 | 内容图片  | 语义强，支持 `alt`，适合 logo/插图 |
| CSS 背景图    | 装饰性图像 | 灵活控制样式、位置、hover 效果      |

### HTML 属性基础

- HTML 标签通常配有属性，提供额外信息：
    
    ```html
    <img src="cat.jpg" alt="A cute cat" width="200" />
    ```
    
- **通用属性**：`id`, `class`, `title`, `style`, `hidden`, `tabindex`
    
- `id`：唯一标识某元素，通常配合 JS 或 CSS 使用
    
- `class`：可复用标记，可为多个元素指定样式
    

### HTML 的作用

- 构建网页“结构”和“语义”，如：
    
    - 哪一块是导航？哪一块是正文？
        
    - 哪些是段落？哪些是图像？
        
    - 帮助浏览器、开发者、搜索引擎、辅助设备理解网页内容
        

---

## 二、CSS 样式与定位

### CSS 是什么？

- **CSS（层叠样式表）** 是为网页“添加样式”的语言。
    
- 控制网页元素的外观：颜色、字体、布局、响应式行为等。
    
- 可以通过**选择器**选中 HTML 元素，并给它们加上样式。
    

### CSS 的作用

- 美化网页：字体、颜色、背景、边框、阴影等
    
- 设置布局：横向排版、居中对齐、响应式缩放等
    
- 提升用户体验：悬停变化、过渡动画、状态高亮
    

### class 和 id 的差异及使用场景

|属性|写法|可复用性|典型用途|
|---|---|---|---|
|`id`|`#header`|❌ 不可复用|页面中唯一的元素，如 header, footer|
|`class`|`.btn`|✅ 可多个元素共享|通用样式组，如按钮、表单组|

**HTML 示例：**

```html
<div id="main" class="content highlight">
  <p class="text">Hello!</p>
</div>
```

**CSS 示例：**

```css
#main { padding: 20px; }
.content { background-color: #f0f0f0; }
.text { color: #333; }
```

### 选择器类型详解

|类型|示例|描述|
|---|---|---|
|ID 选择器|`#nav`|精确选中某个唯一元素|
|Class 选择器|`.card`|选中所有有该类名的元素|
|标签选择器|`p`, `h1`|选中所有该类型的元素|
|组合选择器|`div > p`, `.menu a:hover`|结构和状态选择|
|属性选择器|`input[type="text"]`|精准选中具有特定属性的元素|
|通配选择器|`*`|选中所有元素（性能较低）|

### CSS 权重与优先级

- 权重从高到低：
    
    1. 行内样式：`style="..."`
        
    2. ID 选择器：`#box`
        
    3. 类、属性、伪类：`.btn`, `[type=text]`, `:hover`
        
    4. 标签选择器：`div`, `p`
        
    5. 通配符选择器：`*`
        
- 冲突时根据“最近定义”和“权重”共同决定
    

### 样式属性分类

- 文本样式：`font-size`, `color`, `line-height`, `font-family`, `font-weight`
    
- 间距布局：`margin`, `padding`
    
- 定位属性：`position: relative/absolute`, `z-index`
    
- 显示属性：`display: block/inline/inline-block`, `visibility`
    

### margin and padding（布局控制核心）

- **`margin`（外边距）**：用于控制元素与外部元素之间的距离。
    
    - 可设置：`margin-top`, `margin-right`, `margin-bottom`, `margin-left`
        
    - 简写方式：
        
        - `margin: 10px`（四边相同）
            
        - `margin: 10px 5px`（上下 10px，左右 5px）
            
        - `margin: 10px 5px 15px`（上 10，左右 5，下 15）
            
        - `margin: 10px 5px 15px 0`（上右下左）
            
- **`padding`（内边距）**：用于控制内容与元素边框之间的距离。
    
    - 与 margin 语法完全一致
        
    - 常用于增加内容区域的“呼吸感”，使内容不贴边显示
    

- **尺寸 size 属性**：决定元素的整体占位
    
    - `width`, `height`：指定元素的可视宽高
        
    - `min-width`, `max-width`, `min-height`, `max-height`：设置限制范围
        
    - 实践建议：尽量配合百分比、`auto`、`max-width` 控制响应式行为
        
- **box-sizing 属性**：定义尺寸计算方式
    
    - `content-box`（默认）：`width` 不包括 `padding` 和 `border`
        
    - `border-box`（推荐）：`width` 包含 `padding` 和 `border`，更直观易控


- **示例对比**：
    

```
.box {
  margin: 20px; /* 与外部距离 */
  padding: 10px; /* 内部文本留白 */
  border: 1px solid #ccc;
}
```

- **实践提示**：
    
    - 使用 `box-sizing: border-box` 能让 padding 不影响整体尺寸计算
        
    - margin 会叠加（尤其是块元素上下），而 padding 不会

---
## 三、布局系统与网格设计

### Flexbox 布局（弹性盒子）

- 用于一维布局（横向或纵向）
    
- 常用属性：`display: flex`, `justify-content`, `align-items`, `flex-direction`
    

### Grid 布局（网格）

- 用于二维布局（横+纵）
    
- 常用属性：`display: grid`, `grid-template-columns`, `gap`
    

### Bootstrap 栅格系统（基于 12-column 网格）

- 响应式类名：`.col-12`, `.col-sm-6`, `.col-md-4`, `.col-lg-3` 等
    
- 与 Grid/Flex 结合使用
    

```
<div class="row">
  <div class="col-12 col-md-4"></div>
</div>
```

- `row` 为 Flex 容器，`col-*` 自动适配宽度，支持响应式断点
    
- 行间内容分隔：`<hr>` 或自定义 `.divider`
    

### 栅格系统与布局关系说明

- Grid 是原生 CSS 的二维布局方案
    
- Bootstrap 的 12-column 栅格系统是对 Grid/Flex 的封装与抽象
    
- 在实际开发中，两者可以配合使用，或纯 CSS 也能实现等效布局
    

---

##  四、响应式设计（Responsive Design）

### 核心概念

- 页面样式根据不同屏幕尺寸动态变化
    
- 使用媒体查询（Media Query）实现
    

### Media Query 写法与断点

```
@media (max-width: 576px) {
  body {
    max-width: 100%;
    padding: 0 10px;
  }
}
```

- 常见断点：
    
    - `max-width: 576px` → 手机
        
    - `min-width: 768px` → 平板
        
    - `min-width: 992px` → 小型桌面
        
    - `min-width: 1200px` → 大型桌面
        

### 响应式策略对比

|   |   |   |   |
|---|---|---|---|
|策略|默认样式|媒体查询方向|推荐|
|Mobile First|小屏|`min-width` 向上覆盖|✅|
|Desktop First|大屏|`max-width` 向下覆盖|❌|

---

##  五、开发工具与规范

### CSS 写法推荐

- ✅ 推荐：使用 `<style>` 或外部 `.css` 文件
    
- ❌ 避免：内联 `style="..."` 中写 media query
    

### Prettier 自动格式化

- 格式化全部文件：`npx prettier --write .`
    
- 检查不合规范文件：`--check`
    
- 可通过 `.prettierrc` 自定义风格
    

### Utility-first CSS（如 Tailwind）

- 类名即样式单元：如 `bg-blue-500`, `text-white`, `px-4`
    
- 响应式语法：如 `md:text-lg`
    
- 优点：样式集中于 HTML，开发高效，响应式灵活