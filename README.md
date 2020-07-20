## bg.html

实现效果：背景图片高度随内容高度自适应，并且适配所有屏幕。
1. 高度 < iphoneX，滚动显示。
2. 高度 = iphoneX不滚动。

背景图片设计：750 * 1624（按照iphoneX大小设计）

```html
<!-- 核心代码 -->
<style>
  html, body {
    margin: 0;
    padding: 0;
    font-family: "Heiti SC", DroidSansFallback, "Microsoft YaHei";
  }
  body {
    background-image: url('./images/bg.jpg');
    background-size: 100%;
    background-repeat: no-repeat;
  }
</style>
```