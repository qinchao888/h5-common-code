## bg.html

实现效果：背景图片高度随内容高度自适应，并且适配所有屏幕。
1. 内容高度 >  屏幕高度，滚动显示。
2. 内容高度 <= 屏幕高度，不滚动。
3. 一般来说，设计稿是按照 750 * 1334 设计，因此，在 iphone6、7、8 和 iphoneX 中内容不会滚动显示，而在 iphone4、5 等设备中内容则是滚动显示。

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

## page.html

分页加载

```js
// 核心代码（不使用jquery）
var lazyScroll = function (opts) {
  this.callback = opts.callback; //回调函数
  this.distance = opts.distance || 0; //距离
  this.elem = opts.elem; // 标记元素
  this.content = opts.content || window;
}
lazyScroll.prototype = {
  init: function () {
    var self = this;
    this.content.onscroll = function () {
      var elTop = self.elem.offsetTop // 标记元素距离顶部的高度
      if (this === window) {
        var height = this.innerHeight // 窗口的高度
        // 滚动条滚动的高度
        var scrollTop = document.documentElement.scrollTop || document.body.scrollTop
        if (elTop - scrollTop - height <= self.distance) {
          self.callback()
        }
      } else {
        var height = this.offsetHeight // 元素的高度
        var scrollTop = this.scrollTop
        if (elTop - scrollTop - height <= self.distance) {
          self.callback()
        }
      }
    }
  }
}

// 使用jquery
//滚动加载事件
var lazyScroll=function(opts){
  this.callback=opts.callback; //回调函数
  this.distance=opts.distance || 0; //距离
  this.elem=$(opts.elem);
  this.content=opts.content || window;
}
lazyScroll.prototype={
  init:function(){
    var self=this;
    $(self.content).on("scroll",function(){
      var _scrollTop=$(this).scrollTop();
      var _w_height=$(this).height();
      if(self.content!=window){
        var _ele_top=self.elem.position().top;
        // console.log(_ele_top-_w_height);
        if((_ele_top-_w_height)<=self.distance){
          self.callback();
        }
      }else{
        var _ele_top=self.elem.offset().top;
        var _distance=_ele_top-_scrollTop;
        if((_distance-_w_height)<=self.distance){
          self.callback();
        }
      }
    })
  }
}
```