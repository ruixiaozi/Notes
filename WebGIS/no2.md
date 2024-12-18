## WebGIS学习笔记 GIS地图学基础

---

### 1. 坐标系

坐标系是用于定义要素实际位置的坐标框架，包括坐标原点（0），长半轴（a），短半轴（b），扁率（f）。

坐标系可分为地理坐标系和投影坐标系：地理坐标系是之间建立在椭球体上的，用经度和纬度表达地理对象位置；投影坐标系是建立在平面上的。

### 2. 投影转换

球面是一个不可展曲面，需要使用投影理论：

因为球面上的一点是由经度和纬度决定的，所有在平面上，构建纬度为横向，经度为纵向的经纬网络，然后将球面上的点展开到经纬网里面。但是由于经度纬度转换成平面直角坐标系或者极坐标时总会出现扭曲变形，投影方法就是用来解决这种问题。

#### 2.1 地图投影方法：

##### 2.1.1 按变形性质分类：

1. 等角投影：没有角度变化，便于测量方向和角度，但是不能测量面积
2. 等积投影：没有面积变化，便于面积计算和测量
3. 任意投影：既不等角也不等积，变形适中，其中有一类为等距投影

##### 2.1.2 按投影的构成方式分类：

1. 几何投影
2. 解析投影

### 3. 比例尺

比例尺等于图上距离除以实际距离。



---

#### [返回目录](./)

