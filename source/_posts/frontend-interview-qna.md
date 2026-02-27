---
title: 前端面试八股整理（2026 版）
date: 2026-02-27 10:00:00
categories: 面试
tags:
  - HTML
  - CSS
  - JavaScript
  - TypeScript
  - Vue
  - 网络
  - 性能
  - 工程化
cover: /images/covers/cover-01.jpg
comments: false
---

> 面向快速复盘的问答清单。每个问题给出要点与可追问方向，面试前 30 分钟浏览即可。

## HTML / CSS

### Q1: 语义化 HTML 的价值是什么？

**答：**

- 结构清晰：利于团队协作与后期维护。
- 可访问性：屏幕阅读器能正确理解页面结构。
- SEO 友好：搜索引擎更容易理解内容层级。

**可追问：**

- `header` / `nav` / `main` / `article` / `section` 的使用边界？
- `figure` 和 `img` 的组合场景？

### Q2: BFC 是什么？常见触发条件？

**答：**

- BFC（块级格式化上下文）是一个独立的布局环境。
- 解决问题：清除浮动、阻止外边距折叠、避免元素重叠。

**常见触发条件：**

- `overflow: hidden/auto/scroll`
- `display: inline-block` / `flow-root`
- `position: absolute/fixed`
- `float` 非 `none`

**可追问：**

- 为什么 `overflow: hidden` 能清除浮动？
- `flow-root` 与传统方式的差异？

### Q3: 盒模型有哪些？如何切换？

**答：**

- 标准盒模型：`width/height` 只包含内容。
- IE 盒模型：`width/height` 包含 `padding` 和 `border`。
- 切换方式：`box-sizing: border-box`。

**可追问：**

- `border-box` 在组件库中为何更常用？

### Q4: Flex 与 Grid 的适用场景区别？

**答：**

- Flex：一维布局（行或列），适合组件级布局。
- Grid：二维布局，适合页面级布局与网格系统。

**可追问：**

- Flex 的 `flex-basis` 与 `width` 优先级？
- Grid 的 `minmax` 与自适应布局？

### Q5: 如何实现 1px 细线与移动端适配？

**答：**

- 方案：使用 `transform: scale(0.5)` + `devicePixelRatio` 或使用 `border-image`。
- 适配：`rem + viewport` 或 `vw`。

**可追问：**

- `viewport` 缩放导致的字体渲染问题？

## JavaScript

### Q6: 原型链与继承的核心概念？

**答：**

- 每个对象都有 `__proto__` 指向其原型。
- 函数有 `prototype` 作为实例共享属性。
- 继承的本质是原型链查找。

**可追问：**

- `new` 的执行过程？
- `Object.create` 的用途？

### Q7: 事件循环（Event Loop）如何运行？

**答：**

- 同步代码先执行。
- 微任务队列（Promise）优先于宏任务队列（setTimeout）。
- 每轮循环：执行宏任务 -> 清空微任务。

**可追问：**

- `requestAnimationFrame` 属于哪一类？
- Node.js 中的事件循环差异？

### Q8: 闭包的作用与风险？

**答：**

- 作用：封装私有变量、延长变量生命周期。
- 风险：持有引用导致内存无法释放。

**可追问：**

- 在 React/Vue 中闭包常见坑？

### Q9: `this` 指向规则？

**答：**

- 默认绑定：全局对象或 `undefined`（严格模式）。
- 隐式绑定：由调用者决定。
- 显式绑定：`call/apply/bind`。
- `new` 绑定优先级最高。

**可追问：**

- 箭头函数为何没有自己的 `this`？

### Q10: 防抖与节流的区别？

**答：**

- 防抖：停止触发一段时间后执行。
- 节流：固定时间间隔内只执行一次。

**可追问：**

- 输入搜索用哪种？滚动监听用哪种？

## TypeScript

### Q11: `any`、`unknown`、`never` 的区别？

**答：**

- `any`：放弃类型检查。
- `unknown`：需要类型收窄后才能使用。
- `never`：永不出现的类型（异常或死循环）。

**可追问：**

- `unknown` 与 `any` 的安全性差别？

### Q12: 泛型的典型使用场景？

**答：**

- 让函数/类支持多类型复用。
- 常见于工具函数、接口封装、组件 Props。

**可追问：**

- 何时用泛型约束？如何写 `extends`？

### Q13: 类型体操常用工具类型？

**答：**

- `Partial`、`Required`、`Pick`、`Omit`、`Record`。

**可追问：**

- 自己实现 `Pick`/`Omit` 的思路？

## Vue

### Q14: Vue2 与 Vue3 响应式原理差异？

**答：**

- Vue2：`Object.defineProperty`，无法监听新增/删除属性。
- Vue3：`Proxy`，支持更全面的拦截。

**可追问：**

- 为什么 Vue3 性能更好？

### Q15: 组件通信方式有哪些？

**答：**

- 父子：`props` / `emit`。
- 跨层：`provide/inject`。
- 全局状态：`pinia` / `vuex`。
- 事件总线（不推荐）。

**可追问：**

- 什么时候用 `provide/inject`？

### Q16: Vue 的 diff 算法优化点？

**答：**

- 同层比较、key 复用、最长递增子序列优化。

**可追问：**

- `key` 的最佳实践？

### Q17: 生命周期在实际项目如何用？

**答：**

- `onMounted` 拉取数据。
- `onUnmounted` 清理副作用。

**可追问：**

- SSR 场景生命周期差异？

## 浏览器 / 网络

### Q18: HTTP 与 HTTPS 区别？

**答：**

- HTTPS 在 HTTP 上增加 TLS，确保加密与身份验证。
- 提升安全性与完整性。

**可追问：**

- TLS 握手流程？

### Q19: 缓存策略有哪些？

**答：**

- 强缓存：`Cache-Control` / `Expires`。
- 协商缓存：`ETag` / `Last-Modified`。

**可追问：**

- 强缓存与协商缓存的优先级？

### Q20: 跨域的常见解决方案？

**答：**

- CORS、JSONP、代理转发、postMessage。

**可追问：**

- 预检请求触发条件？

## 性能

### Q21: 常见前端性能指标？

**答：**

- FCP、LCP、TTI、CLS。

**可追问：**

- CLS 主要由什么引起？如何优化？

### Q22: 资源优化方法？

**答：**

- 图片压缩与懒加载。
- Tree-shaking、代码分割。
- 预加载/预连接。

**可追问：**

- 预加载与预取的差异？

## 工程化

### Q23: 为什么需要模块化？

**答：**

- 提升可维护性与可复用性。
- 避免命名污染。

**可追问：**

- CommonJS 与 ESModule 的差异？

### Q24: CI/CD 的核心价值？

**答：**

- 自动化测试与部署，减少人为错误。

**可追问：**

- 前端常见 CI 流程？

---
