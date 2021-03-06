**转载请注明本仓库地址**

最新版文档逐步完善中, 之前版本请参考 [**这里**](https://github.com/xswei/d3js_doc/tree/master/d3js_doc_old)

# D3: Data-Driven Documents

<a href="https://d3js.org"><img src="https://d3js.org/logo.svg" align="left" hspace="10" vspace="20"></a>

**D3** (或者叫 **D3.js** )是一个基于 web 标准的 JavaScript 可视化库. D3 可以借助 SVG, Canvas 以及 HTML 将你的数据生动的展现出来. D3 结合了强大的可视化交互技术以及数据驱动 DOM 的技术结合起来, 让你可以借助于现代浏览器的强大功能自由的对数据进行可视化. 

<br>

## 资源

* [API 参考](https://github.com/xswei/d3js_doc/tree/master/API_Reference/README.md)
* [API 参考 ( 原英文版 )](https://github.com/d3/d3/blob/master/API.md)
* [发布说明](https://github.com/d3/d3/releases)
* [官方画廊](https://github.com/d3/d3/wiki/Gallery)
* [Mike Bostock 的示例](https://bl.ocks.org/mbostock)
* [可视化编程](https://beta.observablehq.com/?utm_source=d3js-org)
* [教程](https://github.com/d3/d3/wiki/Tutorials)
* [插件](https://github.com/d3/d3/wiki/Plugins)
* [v3 与 v4](https://github.com/xswei/d3js_doc/tree/master/Release_Notes/CHANGES.md)
* [一些 Demo](https://github.com/xswei/d3js_doc/blob/master/API_Reference/EXAMPLES.md)

## 联系译者

微信：weichat_6955

QQ: 214175619

### 最新版本动态

#### 5.0.0

[Released March 22, 2018.](https://github.com/d3/d3/releases/tag/v5.0.0)

D3 5.0 引入了很少的非向后兼容的改变.

D3 现在采用的是 [Promises](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises) 来替代异步回调加载数据。 Promises 简化了异步代码结构，尤其是现代浏览器支持 [async and await](https://javascript.info/async-await) 操作。(在 [Observable](https://beta.observablehq.com) 中参考 [introduction to promises](https://beta.observablehq.com/@mbostock/introduction-to-promises) 的介绍)。例如在 V4 中使用如下方式加载 CSV 文件:

```js
d3.csv("file.csv", function(error, data) {
  if (error) throw error;
  console.log(data);
});
```

在 V5 中基于 Promises 实现:

```js
d3.csv("file.csv").then(function(data) {
  console.log(data);
});
```

要注意的是不需要重新抛出错误，因为 Promise 会自动 reject，并且需要的话可以使用 *promise*.catch。使用 await 的话代码会更简单：

```js
const data = await d3.csv("file.csv");
console.log(data);
```

由于采用了 promises，D3 现在使用 [Fetch API](https://fetch.spec.whatwg.org/) 来代替 [XMLHttpRequest](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest): [d3-request](https://github.com/d3/d3-request) 模块由 [d3-fetch](https://github.com/d3/d3-fetch) 替代。Fetch 支持许多强大的特性，比如 [streaming responses](https://beta.observablehq.com/@mbostock/streaming-shapefiles)。D3 5.0 也不再使用 [d3-queue](https://github.com/d3/d3-queue)，取而代之推荐 [Promise.all](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) 来处理批量异步任务，或者使用辅助库比如 [p-queue](https://github.com/sindresorhus/p-queue) 来 [control concurrency(控制并发)](https://beta.observablehq.com/@mbostock/hello-p-queue).

D3 不再提供 d3.schemeCategory20* 颜色方案。因为这些颜色有缺陷，可能会错误的暗示数据中的关系：色调相近的可能被认为是一个分组，而亮度可能被错认为是排序。作为替换，D3 5.0 使用 [d3-scale-chromatic](https://github.com/d3/d3-scale-chromatic)，它实现了 ColorBrewer 的方案设计，包括 [categorical](https://github.com/d3/d3-scale-chromatic/blob/master/README.md#categorical), [diverging](https://github.com/d3/d3-scale-chromatic/blob/master/README.md#diverging), [sequential single-hue](https://github.com/d3/d3-scale-chromatic/blob/master/README.md#sequential-single-hue) 和 [sequential multi-hue](https://github.com/d3/d3-scale-chromatic/blob/master/README.md#sequential-multi-hue) 方案。这些颜色方案在连续式和分散式都是可用的。

D3 提供了通过 [d3-contour](https://github.com/d3/d3-contour) 实现的 [marching squares(生成二维轮廓的算法)](https://beta.observablehq.com/@mbostock/d3-contour-plot) and [density estimation(密度估计)](https://beta.observablehq.com/@mbostock/d3-density-contours). 并且添加了两个新的 [d3-selection](https://github.com/d3/d3-selection)  方法：[*selection*.clone](https://github.com/d3/d3-selection/blob/master/README.md#selection_clone) 用来克隆已选择的节点，[d3.create](https://github.com/d3/d3-selection/blob/master/README.md#create) 用来创建分离的元素。 [Geographic projections](https://github.com/d3/d3-geo) 也支持  [*projection*.angle](https://github.com/d3/d3-geo/blob/master/README.md#projection_angle)，一种由 Philippe Rivière 提出的梦幻般的新的多面体投影。

最后，D3 的 [package.json](https://github.com/d3/d3/blob/master/package.json) 不再引用依赖的精确版本，解决了重复安装 D3 模块的问题。

## 安装

如果使用 `npm`, 则可以通过 `npm install d3` 来安装. 此外还可以下载 [最新版](https://unpkg.com/d3/build/), 最新版支持 AMD、CommonJS 以及基础标签引入形式. 你也可以直接从 [d3js.org](https://d3js.org), [CDNJS](https://cdnjs.com/libraries/d3), 或者 [unpkg](https://unpkg.com/d3/) 加载. 比如:

```js
<script src="https://d3js.org/d3.v4.js"></script>
```

压缩版:

```js
<script src="https://d3js.org/d3.v4.min.js"></script>
```

你也可以单独使用 `d3` 中的某个模块, 比如单独使用 [d3-selection](https://github.com/d3/d3-selection): 

```js
<script src="https://d3js.org/d3-selection.v1.min.js"></script>

```

如果要使用某个固定的版本, 则考虑 [CNDJS](https://cdnjs.com/libraries/d3) 或 [ unpkg](https://unpkg.com/d3/)

D3基于 [ES2015 modules](http://www.2ality.com/2014/09/es6-modules-final.html) 开发.  可以使用 Roolup, webpack 或者其他你偏爱的打包工具进行构建. 在一个符合 ES2015 的应用中导入 `d3` 或者 `d3` 的某些模块:

```js
import {scaleLinear} from "d3-scale";
```

或者导入 `d3` 的全部功能并且设置命名空间 (这里是 `d3`):

```js
import * as d3 from "d3";
```

在 Nodejs 环境中:

```js
var d3 = require("d3");
```

你也可以导入多个模块然后将这些模块集合到 `d3` 对象中, 此时使用 [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign):

```js
var d3 = Object.assign({}, require("d3-format"), require("d3-geo"), require("d3-geo-projection"));
```

