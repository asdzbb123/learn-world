## 微信小程序主要目录和文件的作用
- **project.config.json：**项目配置的文件
- **App.js：**设置一些全局的基础数据等
- **App.json：**底部tab丶标题栏和路由等设置
- **App.wxss：**公共样式丶引入iconfront等
- **pages：**里面包含一个个具体的页面
- **index.wxml：**(WeiXin Markup Language)是框架设计的一套标签语言，结合基础组件丶事件系统，可以构建出页面的结构。内部主要是微信自己定义的一套组件
- **index.wxss：**(WeiXin Style Sheets)是一套样式语言，用于描述WXML的组件样式
- **index.js：**页面的逻辑处理，网络请求等
- **index.json：**小程序设置，如页面注册，页面标题及tabar

## WXML和标准的HTML的异同?
**相同:**
- 用来描述页面结构
- 由标签 属性 等构成
**不相同:**
- 标签名字不一样，且小程序标签更少丶单一标签更多
- 多些 `wx:if` 这样的属性以及 `{{}}` 这样的表达式
- WXML 仅能在微信小程序开发者工具中预览，而 HTML 可以在浏览器内预览
- 组件封装不同，WXML 对组件进行了重新封装
- 小程序运行在 JsCore，没有 DOM 树和 window 对象，小程序中无法使用 window 对象和 document 对象

## WXSS和CSS的异同?
- 都是用来描述页面的样子
- WXSS 具有 CSS 大部分的特性，也做了一些扩充和修改
- WXSS 新增了尺寸单位，WXSS 在底层支持新的尺寸单位`rpx`
- WXSS 仅支持部分 CSS 选择器
- WXSS 支持全局样式与局部样式
- WXSS 没有 `body`, 样式可直接使用 `@import` 导入

## 小程序页面有哪些传递数据的方法
- URL参数传递: 通过跳转页面在URL携带参数,使用`wx.navigateTo`或`wx.redirectTo`方法跳转时,可以在URL中添加`?key=value`的形式来传递参数,在目标页面中通过`options.query`来获取参数值
- 页面之间共享数据: 通过全局变量 或 全局方法来实现页面间的数据共享. 在app.js中定义全局变量或方法,在任意页面可以通过`globalData`来访问和修改全局变量的值.
- Storage本地存储：可以使用`wx.setStorageSync`或`wx.setStorage`将数据存储到本地缓存中，然后在其他页面通过`wx.getStorageSync`或`wx.getStorage`来获取存储的数据
- 全局事件总线: 在appjs中创建一个eventEmitter实例,在任意页面通过`eventEmitter.emit`来触发事件,并传递数据,其他页面可以通过.on来监听该事件并获取数据
  
## 微信小程序怎样跟事件传值？
- 给HTML元素添加`data-`属性来传递需要的值,然后通过`e.currentTarget.dataset`或`onload`的`param`参数获取
- `data-`名称不能有大写字母 并且不可以存放对象

## 如何封装微信小程序的数据请求
- 在项目中创建`utils`目录及api.js文件及`apiConfig.js`文件
- 在`apiConfig.js`中封装基础的`get post put delete`等请求方式,设置请求体,带上token和处理异常
- 在api中引入`apiConfig.js`封装好的请求方法,页面数据请求的url设置对应的方法并导出
- 并且在具体的页面中导入