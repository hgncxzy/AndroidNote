

[TOC]



##  重要概念

### px、pt、ppi、dpi、dp、sp 之间的关系

#### 各自的定义

- pt：point，点，印刷行业常用单位。
  $$
  1英寸 = 2.54厘米（约）； 1pt = 1/72 英寸= 0.035 厘米；
  $$

- px：pixel，像素，电子屏幕上组成一幅图画或照片的最基本单元。

  - [x] 平常所说的 1920×1080 只是像素数量，也就是 1920px × 1080px，代表手机高度上有 1920 个像素点，宽度上有 1080 个像素点；1px 代表屏幕上一个物理的像素点。

  - [x] px 单位不被建议使用，因为同样 100px 的图片，在不同手机上显示的实际大小可能不同，如下图所示（图片来自[android developer guide](http://developer.android.com/guide/practices/screens_support.html)，下同）。

  ![img](https://images0.cnblogs.com/i/1804/201407/012203494805825.png)

  - [x] 偶尔用到 px 的情况，是需要画 1 像素表格线或阴影线的时候，用其他单位如 dp 会显得模糊。

- ppi：pixel per inch，每英寸像素数，该值越高，则屏幕越细腻。

- dpi： dots  per inch，每英寸多少点，该值越高，则图片越细腻。

  - [x] 一般用 dpi 即每英寸多少像素来评价屏幕的显示效果，dpi 等同 ppi 。

- dp：Density-independent pixel, 是安卓开发用的长度单位。

  - [x] 1dp 表示在屏幕像素点密度为 160ppi 时1px 长度。

  - [x] 其实 dp 就是为了使得开发者设置的长度能够根据不同屏幕(分辨率 / 尺寸也就是 dpi )获得不同的像素 (px) 数量。比如：我将一个控件设置长度为 1dp，那么在 160dpi 上该控件长度为 1px，在 240dpi 的屏幕上该控件的长度为 240/160 = 1.5 px。也就是 dp 会随着不同屏幕而改变控件长度的像素数量。

  - [x] dp 为安卓开发时的长度单位，根据不同的屏幕分辨率，与 px 有不同的对应关系。安卓端屏幕大小各不相同，根据其像素密度，分为以下几种规格(图片来自网络)：

  ![QQ20150717160404](http://image.woshipm.com/wp-files/2015/07/QQ20150717160404.png)



  - [x] 1dp 定义为屏幕密度值为 160ppi 时所对应的像素为 1px，即，在 mdpi 时，1dp = 1px。 

  ​       以 mdpi 为标准，这些屏幕的密度值比为：
$$
  ldpi : mdpi : hdpi : xhdpi : xxhdpi = 0.75 : 1 : 1.5 : 2 : 3；
$$
  ​       即，在 xhdpi 的密度下，1dp = 2px；在hdpi情况下，1dp = 1.5px；其他类推。

    - [x] 其实记住一点，dp 最终都要化为像素数量来衡量大小的，因为只有像素数量最直观。使用 dp 作为单位在不同手机上的效果，见下图。（图片来自[android developer guide](http://developer.android.com/guide/practices/screens_support.html)，下同）。
    

![img](https://images0.cnblogs.com/i/1804/201407/012206531991719.png)

- dip：与 dp 完全相同，只是名字不同而已。在早期的 Android 版本里多使用 dip，后来为了与  sp  统一就建议使用 dp 这个名字了。
- sp: scale-independent pixel，安卓开发用的字体大小单位。

  - [x] 与缩放无关的抽象像素（Scale-independent Pixel）。sp 和 dp 很类似但唯一的区别是，Android 系统允许用户自定义文字尺寸大小（小、正常、大、超大等等），当文字尺寸是“正常”时，1sp = 1dp = 0.00625 英寸，而当文字尺寸是“大”或“超大”时，1sp > 1dp = 0.00625英寸。类似我们在 windows 里调整字体尺寸以后的效果——窗口大小不变，只有文字大小改变。

#### 换算公式

```reStructuredText
- 1pt = (dpi / 72) px
- dpi = ppi (实际上是约等于)
- ppi = 屏幕对角线上的像素点数/对角线长度 = √ （屏幕横向像素点^2 + 屏幕纵向像素点^2）/ 对角线长度
- 1dp =（dpi / 160）px
- 当文字尺寸是“正常”时 1sp = 1dp，而当文字尺寸是“大”或“超大”时，1sp > 1dp。一般情况下可认为sp = dp。
```

![img](https://mmbiz.qpic.cn/mmbiz_png/5EcwYhllQOgM19n6iawpWQRCfcibxicoBYG51prmqwNCLAVALyK5Rhv4uSbrU5FQKQL6bZI3iaibTJaz3NMpEQ8zWAA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 现象剖析

在标识尺寸的时候，Android 并不推荐我们使用 px 这个真实像素单位，因为不同的手机之间，分辨率是不同的，比如一个 96*96 像素的控件在分辨率越来越高的手机上会在整体 UI 中看起来越来越小。（图片来自[android developer guide](http://developer.android.com/guide/practices/screens_support.html)，下同）。

![img](https://images0.cnblogs.com/i/1804/201407/012203494805825.png)

## 核心问题

Android适配最核心的问题有两个：

1. 适配的效率，即把设计图转化为 App 界面的过程是否高效；
2. 高度的兼容性，如何保证实现 UI 界面在不同尺寸和分辨率的手机中 UI 的一致性。

这两个问题都很重要，一个是保证我们开发的高效，一个是保证我们适配的成效；今天我们就这两个核心的问题来聊一聊Android的适配方案。

## 适配方案

### 直接适配

#### 原理

dpi 是像素密度，指的是在**系统软件上指定**的单位尺寸的像素数量，它往往是写在系统出厂配置文件的一个固定值。

大家买手机的时候，往往会听到另一个叫 ppi 的参数，这个在手机屏幕中指的也是像素密度，但是这个是物理上的概念，它是客观存在的不会改变。dpi 是软件参考了物理像素密度后，人为指定的一个值，这样保证了某一个区间内的物理像素密度在软件上都使用同一个值。这样会有利于我们的 UI 适配。

![1559098483059](C:\Users\002034\AppData\Roaming\Typora\typora-user-images\1559098483059.png)

Android 推荐使用 dp 作为尺寸单位来适配 UI。理由是 ，dp 指的是设备独立像素密度，以 dp 为尺寸单位的控件，在不同分辨率和尺寸的手机上代表了不同的真实像素。根据上面的概念，我们都知道一个公式：
$$
1dp =  ( dpi / 160) px
$$
系统都是通过这个来判断 px 和 dp 的数学关系。 这里的 dpi 也就是 ppi（ppi 它是一个物理概念，表示的是每英寸的像素点）。

而在不同分辨率下，dpi 将会不同，比如：

| ...     | 1080*720 | 1920*1080 |
| ------- | -------- | --------- |
| dpi     | 320      | 480       |
| dpi/160 | 2        | 3         |

根据上面的表格，我们可以发现，720P 和 1080P 的手机，dpi 是不同的，这也就意味着，不同的分辨率中，1dp 对应不同数量的 px ( 720P 中，1dp = 2px，1080P 中 1dp = 3px )，**这就实现了，当我们使用 dp 来定义一个控件大小的时候，他在不同的手机里表现出相应大小的像素值**。也就在不同的手机里面表现一致（图片来自[android developer guide](http://developer.android.com/guide/practices/screens_support.html)，下同）。

![img](https://images0.cnblogs.com/i/1804/201407/012206531991719.png)

#### 优点

1. 最原始的适配方案
   - 我们可以说，通过 dp 加上自适应布局和 weight 比例布局可以基本解决不同手机上适配的问题，这基本是最原始的 Android 适配方案。

#### 缺点

1. 只能适配 90% 的手机
   - 这只能保证我们写出来的界面适配绝大部分手机，部分手机仍然需要单独适配，为什么 dp 只解决了 90% 的适配问题，因为并不是所有的 1080P 的手机 dpi 都是 480，比如 Google 的 Pixel2（1920 x 1080）的 dpi 是 441，也就是说，在 Pixel2 中，1dp = 2.756px, 这样会导致相同分辨率的手机中，这样，一个 100dp x 100dp 的控件，在一般的 1080P手机上，可能都是 300px, 而 Pixel 2 中 ，就只有 275.6px ,这样控件的实际大小会有所不同。
2. 效率低
   - 这种方式无法快速高效的把设计师的设计稿实现到布局代码中。设计稿的 ImageView 是 128px * 128px，当我们在编写 layout 文件的时候，却不能直接写成 128dp * 128dp。在把设计稿向UI代码转换的过程中，我们需要耗费相当的精力去转换尺寸，这会极大的降低我们的生产力，拉低开发效率(虽然通常来说，我们写程序时几乎不用计算 dp，而是直接凭着自己的感觉写的)。

### 宽高限定符适配（分辨率限定符适配）

#### 原理

也可以看这里的[讲解](https://www.jianshu.com/p/1302ad5a4b04)

简单说，就是穷举市面上所有的Android手机的宽高像素值：

![img](https://upload-images.jianshu.io/upload_images/689802-7ade63d364870c5c?imageMogr2/auto-orient/)

设定一个基准的分辨率，其他分辨率都根据这个基准分辨率来计算，在不同的尺寸文件夹内部，根据该尺寸编写对应的dimens 文件。

比如以 480x320 为基准分辨率

- 宽度为320，将任何分辨率的宽度整分为320份，取值为 x1-x320
- 高度为480，将任何分辨率的高度整分为480份，取值为 y1-y480

那么对于 800*480 的分辨率的 dimens 文件来说，

x1 = ( 480 / 320 ) * 1 = 1.5px

x2 = ( 480 / 320 ) * 2 = 3px

...

![img](https:////upload-images.jianshu.io/upload_images/689802-4f88182107be5a90?imageMogr2/auto-orient/strip%7CimageView2/2/w/964/format/webp)

#### 优点

1. 提升了开发效率
   - 这个时候，如果我们的 UI 设计界面使用的就是基准分辨率，那么我们就可以按照设计稿上的尺寸填写相对应的 dimens 引用了,而当 APP 运行在不同分辨率的手机中时，这些系统会根据这些 dimens 引用会去该分辨率的文件夹下面寻找对应的值。这样基本解决了我们的适配问题，而且极大的提升了我们UI开发的效率。

2. 有团队使用过，是一个成熟的适配方案。

#### 缺点

1. 容错机制很差
   - 但是这个方案有一个致命的缺陷，那就是需要精准命中才能适配，比如 1920x1080 的手机就一定要找到1920x1080 的限定符，否则就只能用统一的默认的 dimens 文件了。而使用默认的尺寸的话，UI就很可能变形，简单说，就是容错机制很差。

#### 备注

[鸿洋大佬的适配方案](https://github.com/hongyangAndroid/AndroidAutoLayout)的项目也来自于宽高限定符方案的启发。

##### 优点

这可以说是一个极好的方案，因为它在宽高限定符适配的基础上更进一步，并且解决了容错机制的问题，可以说完美的达成了开发高效和适配精准的两个要求。

##### 缺点

1. 但是我们能够想到，因为框架要在运行时会在 onMeasure 里面做变换

```java
  @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec)
    {
        if (!isInEditMode())
        {
            mHelper.adjustChildren();
        }
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
    }
```

2. 我们自定义的控件可能会被影响或限制，可能有些特定的控件，需要单独适配，这里面可能存在的暗坑是不可预见的，还有一个比较重要的问题，那就是整个适配工作是有框架完成的，而不是系统完成的，一旦使用这个框架，未来一旦遇到很难解决的问题，替换起来是非常麻烦的，而且项目一旦停止维护，后续的升级就只能靠你自己了，这种代价团队能否承受？当然，它已经停止维护了。

3. 另外，这个方案是根据宽高比例进行适配的，在当前 Android 碎片化严重的情况下，各家厂商屏幕宽高比有很大的不同，这样会造成严重的变形。

### SmallestWidth 适配

#### 原理

也可以看这里的一篇[讲解](https://www.jianshu.com/p/1302ad5a4b04)

或者叫 sw 限定符适配。指的是 Android 会识别**屏幕可用高度和宽度的最小尺寸**的 dp 值（其实就是手机的宽度值），然后根据识别到的结果去资源文件中寻找对应限定符的文件夹下的资源文件。

这种机制和上文提到的宽高限定符适配原理上是一样的，都是系统通过特定的规则来选择对应的文件。

举个例子，小米 5 的 dpi 是 480,横向像素是 1080px，根据 
$$
px = dp ( dpi / 160 )
$$
横向的 dp 值是 1080 / ( 480 / 160 ),也就是 360dp,系统就会去寻找是否存在 value-sw360dp 的文件夹以及对应的资源文件。



![img](https:////upload-images.jianshu.io/upload_images/689802-6db507f8665651a7?imageMogr2/auto-orient/strip%7CimageView2/2/w/494/format/webp)

#### 优点

1. 解决了上文提到的宽高限定符的容错问题
   - smallestWidth 限定符适配和宽高限定符适配最大的区别在于，前者有很好的容错机制，如果没有 value-sw360dp文件夹，系统会向下寻找，比如离 360dp 最近的只有 value-sw350dp，那么Android就会选择 value-sw350dp 文件夹下面的资源文件。这个特性就完美的解决了上文提到的宽高限定符的容错问题。

2. 开发效率高
   - 这套方案是上述几种方案中最接近完美的方案。首先，**从开发效率上，它不逊色于上述任意一种方案**。根据固定的放缩比例，我们基本可以按照 UI 设计的尺寸不假思索的填写对应的 dimens 引用。 我们还有以 375 个像素宽度的设计稿为例，在 values-sw360dp 文件夹下的 diemns 文件应该怎么编写呢？这个文件夹下，意味着手机的最小宽度的dp值是 360，我们把 360dp 等分成 375 等份，每一个设计稿中的像素，大概代表 smallestWidth 值为360dp 的手机中的 0.96dp，那么接下来的事情就很简单了，假如设计稿上出现了一个10px*10px 的 ImageView,那么，我们就可以不假思索的在layout文件中写下对应的尺寸。



![img](https:////upload-images.jianshu.io/upload_images/689802-786f6abb77edd4d4?imageMogr2/auto-orient/strip%7CimageView2/2/w/666/format/webp)

而这种 diemns 引用，在不同的 values-sw<N>dp 文件夹下的数值是不同的，比如 values-sw360dp 和 values-sw400dp,



![img](https:////upload-images.jianshu.io/upload_images/689802-9fffc4b8d779edf5?imageMogr2/auto-orient/strip%7CimageView2/2/w/535/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/689802-5bbab1e5442e4966?imageMogr2/auto-orient/strip%7CimageView2/2/w/530/format/webp)

当系统识别到手机的 smallestWidth 值时，就会自动去寻找和目标数据最近的资源文件的尺寸。

3. 稳定性更好

   - 其次，从稳定性上，它也优于上述方案。原生的 dp 适配可能会碰到 Pixel 2 这种有些特别的手机需要单独适配，但是在 smallestWidth 适配中，通过计算 Pixel 2 手机的的 smallestWidth 的值是 411，我们只需要生成一个values-sw411dp(或者取整生成 values-sw410dp 也没问题)就能解决问题。

   - smallestWidth 的适配机制由系统保证，我们只需要针对这套规则生成对应的资源文件即可，不会出现什么难以解决的问题，也根本不会影响我们的业务逻辑代码，而且只要我们生成的资源文件分布合理，即使对应的smallestWidth 值没有找到完全对应的资源文件，它也能向下兼容，寻找最接近的资源文件。

#### 缺点

1. 增加 apk 的体积
   - 多个 dimens 文件可能导致 apk 变大，这是事实，根据生成的 dimens 文件的覆盖范围和尺寸范围，apk 可能会增大 300kb-800kb 左右，我认为这是可以接受的。

#### 小工具

生成 values-sw<N> 的项目代码，[点击这里获取项目地址](https://github.com/ladingwu/dimens_sw)

### 今日头条适配方案

#### 原理

也可以看这里的[讲解](https://juejin.im/post/5b7a29736fb9a019d53e7ee2)

今日头条屏幕适配方案的核心原理在于，根据以下公式算出 density:
$$
当前设备屏幕总宽度（单位为像素）/ 设计图总宽度（单位为 dp) = density
$$
设计图总宽度计算公式：
$$
设计图总宽度（单位为 dp） =  设计图总宽度（单位为 px）/ (dpi / 160)
$$
dpi 的获取方式，系统已经提供了

```java
  DisplayMetrics dm = new DisplayMetrics();
  int dpi = dm.densityDpi
```

**density 的意思就是 1 dp 占当前设备多少像素**

**只要 density 根据不同的设备进行实时计算并作出改变，就能保证 设计图总宽度 不变，也就完成了适配**

*举例说明*

比如，设计稿宽度是 360px，那么开发这边就会把目标 dp 值设为 360dp，在不同的设备中，动态修改 density 值，从而保证(手机像素宽度) px / density 这个值始终是 360dp,这样的话，就能保证 UI 在不同的设备上表现一致了。

#### 升级版 （[AndroidAutoSize](https://juejin.im/post/5bce688e6fb9a05cf715d1c2)）

在今日头条技术团队提出 30 多行核心适配代码的基础上，扩展到了十几个类，使得适配效率和兼容性大大提高了，推荐使用这个升级版。

#### 优点

1. 稳定性好，侵入性低
   - 这个方案侵入性很低，而且也没有涉及私有 API，是极不错的方案，有今日头条的大厂在用，稳定性应当是有保证的。

2. 可以快速接入，替换方案时成本很低

## 参考资料

1. [px、pt、ppi、dpi、dp、sp之间的关系](https://www.cnblogs.com/bluestorm/p/8951761.html)
2. [基本概念](https://www.cnblogs.com/JLZT1223/p/6784449.html)
3. [今日头条屏幕适配方案终极版正式发布](https://juejin.im/post/5bce688e6fb9a05cf715d1c2)
4. [AndroidAutoSize 源码](https://github.com/JessYanCoding/AndroidAutoSize)