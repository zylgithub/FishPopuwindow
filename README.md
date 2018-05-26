### Android自定义View之实现流行的新浪微博底部菜单：高仿“咸鱼APP”的底部菜单动画效果。
   - 对应的详细解答博客地址：https://blog.csdn.net/xh870189248/article/details/75949283
#### 1、前几天在手机看到了很好看的动画效果，于是，扬起袖子就是干：
  - 上图的是咸鱼App效果，下图是俺高仿的，大神莫喷~

 - 以下是鄙人的~

----------


![这里写图片描述](http://img.blog.csdn.net/20170723215428867?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGg4NzAxODkyNDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

----------

### 2、代码讲解：

 - 代码讲解前，先上图，我手画的原理图，有点草，大家听我娓娓道来。

   - 1、看到咸鱼app的效果，大家都是第一反应想到是 安卓动画，没错！就是安卓动画，但是本人是刚刚入门动画，并没有使用高级的动画—— 属性动画，因此图片移动到了新的位置，那么新的位置就**不具备点击事件效果**，这也是帧动画的局限。所以，有大神还可以使用属性动画的，可以自己造一个啦！
 
   -  2、整个布局只是一个PopupWindow，但是毕竟是点击事件有限，因此我考虑了用了以下的方法：

    - 3、整个过程我简单的说一下：先画好一个布局，下面是3个图片，只有那个加号图片是显示的，而其他的二张是隐藏的，而我用的是RelativeLayout布局，就很好地解决了重叠图片问题。那么上面的2张图片也是隐藏的，为何要这样？因为我要的是这两张图片位置点击事件效果，如果你是按照下面2张图片到上面的话，点击事件还是在下面的，对吧？那么我想到是这样：先隐藏上面的图片。监听 下面图片的动画事件，当动画停止时候，就显示出来，所以，也要把对应的图片隐藏。退出界面，就直接使用动画，就好啦！没那么麻烦了~
    
----------
![这里写图片描述](http://img.blog.csdn.net/20170723223330764?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGg4NzAxODkyNDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

----------

#### 3、开发遇到的问题与细节的实现。

----------

-  1、既然讲到动画，坐标是肯定离不开的，每次的移动、旋转都是需要动画，那么在之前 先声明下，要想获取到自控件的坐标，必须要等其类**初始化完毕**才可以获取，要么会获取为0 。这是我反复遇到的问题，所以，一定要监听动画事件的停止，才可以做获取坐标的事情，这样就可以轻松获取到坐标了。

- 2、文件布局问题：要知道，如果想把某个控件平移到不是非父布局里面，就会在边界消失掉，不知道大家遇到这样的问题不？所以，我必须把整个布局放在只有仅仅一个父控件里，才可以轻松“漂移”控件。

- 3、动画插值器问题，想必仔细看到咸鱼APP的童鞋都知道，它是有回弹效果的。所以我这里用的是BounceInterpolator插值器，类似小球回弹效果。更细心的老司机会发现，其先是第一个按钮先上来，然后才是第二个按钮就上来，那么我们就可以这样做，把其对应的动画时间不一致，就会可以看到一长一短的效果了。


----------


![这里写图片描述](http://img.blog.csdn.net/20170723225708607?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGg4NzAxODkyNDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

