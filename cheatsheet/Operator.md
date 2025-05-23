---
tags:
  - cheatsheet
---
## **三元运算符（Ternary Operator）**

```
condition ? exprIfTrue : exprIfFalse
```
- **condition**：布尔表达式（true 或 false）
- **exprIfTrue**：条件为 true 时执行的表达式
- **exprIfFalse**：条件为 false 时执行的表达式

---
## **逻辑运算符（Logical Operators）**

### **1.**  **`&&`** **（逻辑与）**
 - 如果左边为 false，**返回左边值**
- 否则返回右边值
 
```
console.log(true && "Hello");   // "Hello"
console.log(false && "World");  // false
```

### **2.** **  `||`** **（逻辑或)**
- 如果左边为 true，**返回左边值**
- 否则返回右边值

```
console.log("Hi" || "Bye");     // "Hi"
console.log(null || "Default"); // "Default"
```

