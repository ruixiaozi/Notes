## Echarts学习笔记 基本概念

---

### 1. echarts实例

准备一个 DOM 节点（作为 echarts 的渲染容器），就可以在上面创建一个 echarts 实例。每个 echarts 实例独占一个 DOM 节点。

### 2. 系列（series）

在 echarts 里，`系列`（series）是指：一组数值以及他们映射成的图。

系列是一个数组，每个元素包含的要素至少有：**一组数值、图表类型（`series.type`）、以及其他的关于这些数据如何映射成图的参数。**

也可以使用从 `dataset` 中取出。

### 3. 组件（component）

echarts 中各种内容，被抽象为“组件”（**echarts实例属性**）。例如，echarts 中至少有这些组件：[xAxis](https://echarts.apache.org/zh/option.html#xAxis)（直角坐标系 X 轴）、[yAxis](https://echarts.apache.org/zh/option.html#yAxis)（直角坐标系 Y 轴）、[grid](https://echarts.apache.org/zh/option.html#grid)（直角坐标系底板）、[angleAxis](https://echarts.apache.org/zh/option.html#angleAxis)（极坐标系角度轴）、[radiusAxis](https://echarts.apache.org/zh/option.html#radiusAxis)（极坐标系半径轴）、[polar](https://echarts.apache.org/zh/option.html#polar)（极坐标系底板）、[geo](https://echarts.apache.org/zh/option.html#geo)（地理坐标系）、[dataZoom](https://echarts.apache.org/zh/option.html#dataZoom)（数据区缩放组件）、[visualMap](https://echarts.apache.org/zh/option.html#visualMap)（视觉映射组件）、[tooltip](https://echarts.apache.org/zh/option.html#tooltip)（提示框组件）、[toolbox](https://echarts.apache.org/zh/option.html#toolbox)（工具栏组件）、[series](https://echarts.apache.org/zh/option.html#series)（系列）、...

**因为系列是一种特殊的组件，所以有时候也会出现 “组件和系列” 这样的描述，这种语境下的 “组件” 是指：除了 “系列” 以外的其他组件。**

### 4. 用 option 描述图表

echarts 的使用者，使用 `option` 来描述其对图表的各种需求，包括：有什么数据、要画什么图表、图表长什么样子、含有什么组件、组件能操作什么事情等等。简而言之，`option` 表述了：`数据`、`数据如何映射成图形`、`交互行为`。

### 5. 组件的定位

1. **[类 CSS 的绝对定位]**

多数组件和系列，都能够基于 `top` / `right` / `down` / `left` / `width` / `height` 绝对定位。 这种绝对定位的方式，类似于 `CSS` 的绝对定位（`position: absolute`）。绝对定位基于的是 echarts 容器 DOM 节点。

其中，他们每个值都可以是：

- 绝对数值（例如 `bottom: 54` 表示：距离 echarts 容器底边界 `54` 像素）。
- 或者基于 echarts 容器高宽的百分比（例如 `right: '20%'` 表示：距离 echarts 容器右边界的距离是 echarts 容器宽度的 `20%`）。

2. **[中心半径定位]**

少数圆形的组件或系列，可以使用“中心半径定位”，例如，[pie](https://echarts.apache.org/zh/option.html#series-pie)（饼图）、[sunburst](https://echarts.apache.org/zh/option.html#series-sunburst)（旭日图）、[polar](https://echarts.apache.org/zh/option.html#polar)（极坐标系）。

中心半径定位，往往依据 [center](https://echarts.apache.org/zh/option.html#series-pie.center)（中心）、[radius](https://echarts.apache.org/zh/option.html#series-pie.radius)（半径）来决定位置。

3. **[其他定位]**

少数组件和系列可能有自己的特殊的定位方式。在他们的文档中会有说明。



### 6. 坐标系

很多系列，例如 [line](https://echarts.apache.org/zh/option.html#series-line)（折线图）、[bar](https://echarts.apache.org/zh/option.html#series-bar)（柱状图）、[scatter](https://echarts.apache.org/zh/option.html#series-scatter)（散点图）、[heatmap](https://echarts.apache.org/zh/option.html#series-heatmap)（热力图）等等，需要运行在 “坐标系” 上。坐标系用于布局这些图，以及显示数据的刻度等等。例如 echarts 中至少支持这些坐标系：[直角坐标系](https://echarts.apache.org/zh/option.html#grid)、[极坐标系](https://echarts.apache.org/zh/option.html#polar)、[地理坐标系（GEO）](https://echarts.apache.org/zh/option.html#geo)、[单轴坐标系](https://echarts.apache.org/zh/option.html#singleAxis)、[日历坐标系](https://echarts.apache.org/zh/option.html#calendar) 等。其他一些系列，例如 [pie](https://echarts.apache.org/zh/option.html#series-pie)（饼图）、[tree](https://echarts.apache.org/zh/option.html#series-tree)（树图）等等，并不依赖坐标系，能独立存在。还有一些图，例如 [graph](https://echarts.apache.org/zh/option.html#series-graph)（关系图）等，既能独立存在，也能布局在坐标系中，依据用户的设定而来。

一个坐标系，可能由多个组件协作而成。我们以最常见的直角坐标系来举例。直角坐标系中，包括有 [xAxis](https://echarts.apache.org/zh/option.html#xAxis)（直角坐标系 X 轴）、[yAxis](https://echarts.apache.org/zh/option.html#yAxis)（直角坐标系 Y 轴）、[grid](https://echarts.apache.org/zh/option.html#grid)（直角坐标系底板）三种组件。`xAxis`、`yAxis` 被 `grid` 自动引用并组织起来，共同工作。





---

#### [返回目录](./)