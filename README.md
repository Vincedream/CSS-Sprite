### 什么是CSS Sprite雪碧图
CSS Sprites在国内很多人叫css精灵，是一种网页图片应用处理方式。它允许你将一个页面涉及到的所有零星图片都包含到一张大图中去，我们通过对这张大图用定位“裁剪”，剪出我们需要的部分装载到页面中，这样一来，当访问该页面时，载入的图片就不会像以前那样一幅一幅地慢慢显示出来了。
### 为什么需要使用CSS Sprite雪碧图
我们都知道在一个网页中，往往会包含许多小图标，而这些小图标大都是一个个image组成的，当我们进入一个网页的时候，如果这个页面有一百个小图标，那么浏览器需要向服务器发送一百次http请求，需要耗费过多的时间才能加载完全，这对用户访问网页是非常不友好的，这个时候就需要我们所说的CSS Sprite雪碧图啦～
### 原理
其实原理很简单，就是使用background-position在一张大图中定位裁剪出我们需要的一个部分，然后用这个部分当作单个的图片使用。
- background-position（x,y)

简单描述：以图片的左上角为原点坐标，两个参数分别为xy轴坐标起始点，比如background-position(148px,-180px)就是如图蓝色箭头坐标点为起始点，紫色的边框大小设置为background的背景大小。
![image](https://user-gold-cdn.xitu.io/2017/8/15/53d71308d3107037985d6e793c2c1132)
### Sprite图制作
作为一个程序员花很多时间去学习ps似乎显得不太合理，我们就使用一个现成的工具方便地制作出Sprite“大图”， [CSS Sprite雪碧图在线制作](http://spritegen.website-performance.org/)，制作下载到本地完成后，我们就开始实践吧～
### 实践
- html：

我们模仿一个菜单样式，在文字的左边有一个小图标，其实这个图标并不是一个image标签存在，而是利用一个<i></i>标签将图片设置为背景显示出来。

```
  <div class="cat">
    <ul>
      <li class="li-1">
        <i></i>
        <h3>咖啡冰淇淋 </h3>
      </li>
      <li class="li-2">
        <i></i>
        <h3>甜筒冰淇淋</h3>
      </li>
      <li class="li-3">
        <i></i>
        <h3>西瓜冰淇淋</h3>
      </li>
      <li class="li-4">
        <i></i>
        <h3>牛奶冰淇淋</h3>
      </li>
      <li class="li-5">
        <i></i>
        <h3>原谅冰淇淋</h3>
      </li>
      <li class="li-6">
        <i></i>
        <h3>小熊冰淇淋</h3>
      </li>
    </ul>
  </div>
```
- css样式：

我们重点看li i{}样式，这个样式是作为一个背景图片的统一样式，也就是说我们用url(spritesheet.png)作为“大图”。再分别用.li i{background-position: x y}裁剪出小图标作为背景。

```
h3,ul {margin: 0;padding: 0}
    ul{list-style: none;}
    li h3{font-size: 23px;font-weight: 300}
    li{display: block;height: 40px;line-height: 40px; border-bottom: 1px solid #dedede;}
    .cat{
      width: 170px;
      border: 1px solid #d2cece;
      padding-right: 10px;
    }
    li i{
      background:url(spritesheet.png);
      display: inline;
      width: 40px;
      height: 40px;
      float: left;

    }
    .li-1 i{background-position: -3px -4px;}
    .li-2 i{background-position: -45px -1px;}
    .li-3 i{background-position: -87px -1px;}
    .li-4 i{background-position: -3px -42px;}
    .li-5 i{background-position: -45px -42px;}
    .li-6 i{background-position: -87px -42px;}
```
- 效果图：

![image](https://user-gold-cdn.xitu.io/2017/8/15/f4cc6db9f77a828588247ce8ff1bc52f)

### Tips
1. 我们在制作雪碧图的时候，建议先想好每个小图标的大小再制作雪碧图，因为在css中调整一个图片的大小并不是很方便，倒不如开始的时候就把大小确定。
2. 在线制作雪碧图时，会有自动生成的代码，在我实际体验当中，这些代码最多只能参考，真正还需要我们自己去调整。
3. 我们在调整background-position的时候，可以利用chrome下的css调试工具，将background-position调到合适的位置后，修改样式的值，这样就比较方便我们定位。

### 总结

虽然CSS Sprites是一个非常老的技术，但是能够大大地减少http请求，还能减少图片的字节，解决图片命名上的困扰，简化开发的步骤，是一个非常方便的CSS技巧。
- [DEMO代码传送门](https://github.com/Vincedream/CSS-Sprite)
- [参考文献](https://baike.baidu.com/item/css%20sprite/1139316?fr=aladdin)
