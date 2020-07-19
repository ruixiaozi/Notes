## Vue全家桶学习笔记 概念与安装
---
### 1. Vue是什么

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

---
### 2. 安装

1. js引用：
    ```
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    ```
    或
    ```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
    ```
    或
    ```
    <script type="module">
      import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.esm.browser.js'
    </script>
    ```

2. NPM：
    ```
    $ npm install vue
    ```

3. 命令行工具 (CLI)：  
    Vue 提供了一个官方的 CLI，为单页面应用 (SPA) 快速搭建繁杂的脚手架。