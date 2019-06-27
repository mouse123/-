# 浏览器

### CORS

* 只有 Web 才有跨域 CORS，移动端 iOS 与 Android 就没有，谁让 Web 能看源代码呢，沙盒机制也不如移动端健全。HTML5 支持跨域以后，就变成了CORS技术。 这是内置于http协议本身的。所以自然用起来更流畅，更舒心。 同源策略的限制：XmlHttpRequest 只允许请求当前源（域名、协议、端口）的资源，所以AJAX是不允许跨域的。 相反就是跨域：如果想让XmlHttpRequest 按照自己意愿（域名、协议、端口）请求数据，那就需要跨域
* 那为什么有同源策略限制？
* 没有同源策略的话，资源（如HTTP头、Cookie、DOM、localStorage等）就能相互随意访问，那就没有安全了。同源策略就是把每个网站都关在一个笼子里，每个网站互相访问不到数据，只有用户和网站开发者可以访问数据，这样就安全了。

### 浏览器是怎么绘制一帧动画的

* 在默认状态下，我们点击左上角的圆记录事件，几秒后我们可以点击 Performance 中的 Stop 产生分析数据。在概览面板中我们看到在渡过最初的几百毫秒后，CPU 面积图中各种事件占比按固定周期变化，我们点取其中一小段观察，在主线程图中可看到一段一段类似事件组。观察几组事件后，我们发现，这些事件组的组成都是：10 个 Recalculate Style + Layout 的循环 -&gt; Update Layer Tree -&gt; Paint -&gt; Composite Layers。我们知道，Composite Layers 事件之后，意味着人眼可见新的页面图层，也就是说这样一组事件过后，一帧画面绘制在眼前。

### 浏览器渲染过程

![&#x6D4F;&#x89C8;&#x5668;&#x6E32;&#x67D3;](https://raw.githubusercontent.com/mouse123/my-tips/master/image/v2-a9b24264340f0402ece0ec6c9989d889_hd.jpg)

* 当渲染首屏时，浏览器分别解析 HTML 与 CSS 文件，生成文档对象模型（DOM）与 样式表对象模型（CSSOM）；合并 DOM 与 CSSOM 成为渲染树（Render Tree）；计算样式（ Style）；计算每个节点在屏幕中的精确位置与大小（Layout）；将渲染树按照上一步计算出的位置绘制到图层上（Paint）；渲染引擎合成所有图层最终使人眼可见（Composite Layers）。

  如果改变页面布局，则是先通过 JS 更新 DOM 再经历计算样式到合成图像这个过程。如果仅仅是非几何变化（颜色、visibility、transform），则可以跳过布局步骤。

### 其他

* [浏览器缓存](https://www.infoq.cn/article/8VU-VCrhoxducaFPrNOL)
* [前端监控](https://www.cnblogs.com/hustskyking/p/fe-monitor.html)
* [web优化](https://www.infoq.cn/article/Xxyy8WZrWLwUlIF0*IxR)
* [前端性能优化清单](https://juejin.im/post/5a966bd16fb9a0635172a50a)
* [网站性能优化实战](https://juejin.im/post/5b0b7d74518825158e173a0c)
* **浏览器资源监控**
  * window.performance.getEntriesByType\("resource"\)
  * window.performance.getEntriesByType\("navigation"\)

