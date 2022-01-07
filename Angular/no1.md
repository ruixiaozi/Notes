## Angular学习笔记 搭建环境

---

### 1. 安装 Angular CLI

```
npm install -g @angular/cli
```

### 2. 创建工作区和初始应用

1. 运行 CLI 命令 `ng new` 并提供 `my-app` 名称作为参数，如下所示：

   ```sh
   ng new my-app
   ```

2. `ng new` 命令会提示你提供要把哪些特性包含在初始应用中。按 Enter 或 Return 键可以接受默认值。

### 3. 运行应用

Angular CLI 中包含一个服务器，方便你在本地构建和提供应用。

1. 导航到 workspace 文件夹，比如 `my-app`。
2. 运行下列命令：

```sh
cd my-app
ng serve --open
```

`ng serve` 命令会启动开发服务器、监视文件，并在这些文件发生更改时重建应用。

`--open`（或者只用 `-o` 缩写）选项会自动打开你的浏览器，并访问 `http://localhost:4200/`。





---

#### [返回目录](./)