---
tags:
  - code
  - "#language"
---
- https://github.com/UTSC-CSCC09-Programming-on-the-Web/lab3-jieyinggong.git
- [[Week 2- Interactive frontends with JS]]

---

## Part 1: Good Practice of JS

### 1. Encapsulation and "use strict"

```js
(function () {
  "use strict";
  // your code goes here
})();
```

封装作用域，避免全局变量污染。

### 2. Encapsulation with `window.onload`

为了避免 DOM 还没加载完就操作元素，必须确保 DOM Ready：
防止race condition

```js
window.onload = function () {
  document.addEventListener("click", function () {});
  // other logic
};
```

---

## Part 2: DOM Elements
### DOM、Element、Object、Event 的关系说明：

- **DOM (Document Object Model)** 是浏览器中对网页内容的抽象表示，用一棵“节点树”来组织 HTML 元素。
    
- **Element** 是 DOM 树中的一个节点，通常对应页面上的一个 HTML 标签，如 `<div>`、`<button>`。这些元素通过 `id` 和 `class` 等属性进行标识。
    
- **Object** 是 JavaScript 中对这些 Element 节点的引用或封装，我们操作的 `document.getElementById("id")` 或 `document.querySelector(".class")` 返回的就是一个 JS 对象。
    
- **Event** 是指用户与页面的交互行为，比如点击、提交、键盘输入等。这些事件可以通过 `addEventListener`绑定到 DOM 对象上，从而触发交互逻辑。
    

👉 总结：HTML 中的 `id` 和 `class` 主要用来**标识 DOM 元素**，以便 CSS 进行样式设定，JavaScript 可以精确选中并操作这些元素，而事件（event）则赋予它们行为能力。

### 获取元素：

```js
document.getElementById("id")         // 通过 id 获取元素对象
document.querySelector(".class")       // 通过 class 获取元素对象
```

### 添加事件监听：

```js
element.addEventListener("click", function (e) {
  // 处理点击事件
});
```

### 创建并插入元素：

```js
const el = document.createElement("div"); // 创建元素
el.innerHTML = "Hello";                    // 设置内容
parent.appendChild(el);                   // 添加到父元素中
```


---

## Part 3: Web Storage API - localStorage

在 Web 应用中，localStorage 提供了一种简单方式让我们可以在浏览器中保存最多约 5–10MB 的数据。它以字符串形式存储键值对。对于复杂数据结构（如对象或数组），需要使用 JSON 进行序列化和反序列化。

### 存储数据的一般流程：

1. **定义对象的结构**：以 message 为例：

```js
const obj = {
  username: "Alice",
  content: "Hello"
};
```

2. **使用数据结构存储信息**：多个对象通常被放入一个数组中：

```js
const arr = [obj];
```

3. **将数组转换为字符串存入 localStorage**：

```js
localStorage.setItem("messages", JSON.stringify(arr));
```

### 获取数据的一般流程：

1. **从 localStorage 获取字符串并转为数组**：

```js
const saved = JSON.parse(localStorage.getItem("messages")) || [];
```

2. **对数组中的每个对象执行某种操作**：

```js
saved.forEach(msg => renderMessage(msg));
```

### 增删改时的流程：

- **添加新对象**：

```js
saved.push(newObj);
localStorage.setItem("messages", JSON.stringify(saved));
```

- **更新对象**（如 upvote +1）：

```js
const updated = saved.map(msg =>
  msg.id === targetId ? { ...msg, upvote: msg.upvote + 1 } : msg
);
localStorage.setItem("messages", JSON.stringify(updated));
```

- **删除对象**：

```js
const filtered = saved.filter(msg => msg.id !== targetId);
localStorage.setItem("messages", JSON.stringify(filtered));
```

---

**总结**：localStorage 本质是字符串存储，但我们可以通过：
- 将数组结构 stringify 存储；
- 每次读取都 parse 成对象数组；
- 对数组进行 `push`、`map`、`filter` 等操作；
- 再次 `setItem` 更新存储；

---

## Part 4: Refactor: 架构设计 - 分层职责
#design

- **Frontend Controller** (`index.js`) controls the UI
- **Frontend API Service** (`api-service.js`) provides an API to push/pull data (to localStorage for now)
### Controller（index.js）

- 负责 UI 控制（监听事件、触发更新）

### View State 管理（meact.js）

- 使用 `useState`, `useEffect` 驱动状态响应式更新

```js
const [messagesKey, getMessages, setMessages] = meact.useState([]);
meact.useEffect(() => {
  render();
}, [messagesKey]);
```

> 只能通过 `setMessages(newArray)` 才会触发 useEffect，直接 `msg.upvote += 1` 不会触发

### 数据层（api-service.js）

- 负责读写 localStorage 数据
    
- 函数接口有：`addMessage`, `deleteMessage`, `getMessages`, `updateMessage`
    

### 三者连接：

- `index.js` 监听 UI → 调用 `apiService` 改数据 → 用 `setMessages(...)` 触发 UI 重渲染（通过 meact）
    

---
## Part 5: `meact` 中的状态管理

Instead of directly manipulating the DOM based on user events, we can use a declarative approach to describe the UI and let the "framework" handle the DOM updates. You may practice writing better declarative code by using the `useState`and `useEffect` functions in `js/meact.js`. You may also create your own "framework" if you want to.

### 状态结构与绑定原理

```js
const [stateKey, getState, setState] = meact.useState(initialValue);
```

- `stateKey` 是唯一的 Symbol，用于追踪这个状态（meact 内部使用它判断依赖变化）
    
- `getState()` 返回当前状态值（不可直接修改）
    
- `setState(newValue)` 设置新的状态，会触发所有监听了该 key 的 `useEffect`
    

```js
meact.useEffect(() => {
  // 当 setState 被调用且对应 key 更新时，执行此函数
}, [stateKey]);
```

⚠️ 如果你直接修改对象内部属性，如：

```js
getMessages()[0].upvote += 1;
```

不会触发 `useEffect`，因为数组的引用值（即 getMessages() 返回的数组对象本身）没有改变。注意这里引用的是整个数组的内存地址，而不是 stateKey。只有通过 `setMessages(newArray)` 明确传入一个新的数组对象时，meact 才会检测到状态变化并触发对应的 `useEffect`。

必须使用不可变更新方式：

```js
const updated = getMessages().map(m =>
  m.messageId === msg.messageId ? { ...m, upvote: m.upvote + 1 } : m
);
setMessages(updated); // ✅ 正确做法，引用改变，触发 useEffect
```

### 推荐：函数式状态更新方式

为了避免状态不同步，可以直接在 `apiService` 中支持函数式更新：

```js
apiService.updateMessage(id, (prev) => ({ ...prev, upvote: prev.upvote + 1 }));
```

### 状态与 UI 的连接：

1. `index.js` 提交用户交互事件（如点击点赞）
2. 使用 `getMessages()` 获取当前状态，使用 `map()`/`filter()` 等方法构造新的状态数组
3. 调用 `setMessages(updatedArray)` 设置新的状态
4. `meact.useEffect(..., [messagesKey])` 触发，调用 `render()` 或其他 DOM 更新逻辑
这样就实现了“数据变化 → 状态变化 → 自动 UI 更新”的完整链条。

### OH:
![[IMG_2957.jpg]]

meact用于单独封装update DOM的行为，来和html一对一关联
useEffect 相当于一个listener，setter 相当于event trigger
`[msg, getter, setter] = useState`  
`state msg = [...]` 用来保存/追踪状态，也是`useEffect` 判断对应callback的dependence
`useEffect` 中的update DOM 是关于`state msg = [...]`这个依赖项的
只有dependence变化了，对应的useEffect才会触发

### Summary
1. **meact 用于单独封装 update DOM 的行为，并与 HTML 一对一关联**
    - 通过 `useEffect` 来管理 DOM 更新
    - 每个 `useEffec`t 可以对应某一个具体的 DOM 元素更新逻辑
    
2. **`useEffect` 相当于一个“状态监听器”（listener）**
    - 它注册一个副作用函数，当依赖项发生变化时就执行这个函数
    
3. **`setXXX（setter）`相当于“事件触发器”（event trigger）**
    - 每次调用 setter 修改状态时，会触发依赖这个状态的所有副作用（listener）
    
4. **`[msgKey, getMsg, setMsg] = useState(...)`**
    - msgKey 是这个状态的唯一标识符（用 Symbol 实现）
    - getMsg() 用于获取当前状态值
    - setMsg(newVal) 用于修改状态，并触发依赖这个 msgKey 的 useEffect
    
5. **`state[msgKey] = value`**
    - 是内部用于保存和追踪状态的容器（隐藏在框架内部）
    - useEffect 判断依赖项是否变化，就是通过检查这个状态值
    
6. **`useEffect` 中的 DOM 更新，依赖的是 `state[msgKey]` 的变化**
    - 只有当某个 msgKey 的状态值被 setter 改变时，相关的 useEffect 才会执行
    - 不变就不触发（模拟 React 的依赖追踪机制）
---

## JS 相关语法 & 方法汇总
#language #cheatsheet 
### array function in js

|方法名|功能类别|修改原数组|返回新数组|示例用法|
|---|---|---|---|---|
|`push()`|添加（尾部）|✅ 是|❌ 否|`arr.push(3)` → 在尾部加 3|
|`unshift()`|添加（头部）|✅ 是|❌ 否|`arr.unshift(0)` → 在头部加 0|
|`pop()`|删除（尾部）|✅ 是|❌ 否|`arr.pop()` → 移除最后一个元素|
|`shift()`|删除（头部）|✅ 是|❌ 否|`arr.shift()` → 移除第一个元素|
|`splice()`|插入/删除/替换|✅ 是|❌ 否|`arr.splice(1, 2)` → 从索引 1 删除两个|
|`slice()`|截取子数组|❌ 否|✅ 是|`arr.slice(0, 3)` → 提取前 3 个|
|`filter()`|条件筛选|❌ 否|✅ 是|`arr.filter(x => x > 0)` → 保留大于 0 的|
|`map()`|映射变形|❌ 否|✅ 是|`arr.map(x => x * 2)` → 每个乘 2|
|`find()`|查找第一个匹配|❌ 否|❌ 否|`arr.find(x => x.id === 1)` → 找到对应对象|
|`findIndex()`|查找索引|❌ 否|❌ 否|`arr.findIndex(x => x.id === 1)`|
|`includes()`|是否包含某值|❌ 否|❌ 否|`arr.includes(3)` → true / false|
|`forEach()`|遍历（不返回）|❌ 否|❌ 否|`arr.forEach(x => console.log(x))`|

### 语法技巧：

#### 展开运算符

```js
[...array] // 克隆数组
```

展开原数组元素，返回一个新数组，避免原数组被直接修改。

#### 条件函数结构（箭头函数）：

```js
(msg) => msg.id === targetId
```

这是一个简写的匿名函数（箭头函数），其结构为：

```js
(parameter) => expression
```

等价于：

```js
function(msg) {
  return msg.id === targetId;
}
```

在数组方法中非常常见，尤其在：

- `filter(fn)` 中作为保留条件
    
- `find(fn)` 中作为查找条件
    
- `map(fn)` 中作为映射规则
    

在 `map()` 示例中：

```js
const updated = messages.map(m =>
  m.id === targetId ? { ...m, upvote: m.upvote + 1 } : m
);
```

这个条件函数 `m => ...` 是将 `m.id` 等于目标 id 的那一项进行更新，其它项保持不变。  

---

## JS / HTML / CSS 三者关系

- **HTML**：页面结构，提供容器（如 `<div id="messages">`）
- **CSS**：外观样式，控制布局和视觉层次
- **JavaScript**：逻辑行为，响应事件、操作 DOM、控制状态

三者通过 `id` / `class` / `event` 进行连接（其中 `id` 和 `class` 是 HTML 元素的属性，同时可被 HTML、CSS 和 JavaScript 使用；而 `event` 是行为的一部分，仅被 JavaScript 使用）：

- **id**：唯一标识一个 HTML 元素，用于 JavaScript 精确定位元素。常用于逻辑操作，例如 `document.getElementById("messages")` 获取留言容器。CSS 中也可以通过 `#messages` 进行样式设定。
- **class**：用于标识一组具有相同样式或行为的元素。CSS 可通过 `.className` 统一应用样式，JavaScript 通过 `document.querySelectorAll(".className")` 选中元素集合。
- **event**：是用户与页面互动时触发的行为，如点击、输入、提交等，JavaScript 使用 `addEventListener("click", handler)` 将处理函数绑定到某个 DOM 元素上。

### HTML/CSS/JS 协作的简单流程图：

```

[HTML: 元素结构]  
↓ 提供 id/class 属性  
[CSS: 样式文件]  
→ 使用 id/class 进行样式绑定  
[JavaScript: 行为逻辑]  
→ 使用 id/class 选中元素  
→ 用 event 为元素绑定交互逻辑

````

例如：通过 `<div id="messages" class="message-list">` 和 `addEventListener("click")`，我们能定位该元素、设定样式并赋予行为，使结构、样式与交互自然融合。

### 示例：
```html
<div id="messages"></div>
<script src="meact.js"></script>
<script src="index.js"></script>
````

---

###  结论与推荐实践

- 使用 `useState` 管理状态，避免引用内部直接改动
- 所有状态更新都应 `setMessages(newArray)`
- 结构清晰：controller / state / service 解耦
- 推荐 `updateMessage` 支持函数式更新，更安全
- 正确加载顺序避免 `meact is not defined` 错误

---

