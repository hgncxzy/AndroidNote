## 内容

1. [启动模式](#启动模式)
2. [设置横竖屏](#设置横竖屏)
3. [跳转动画](#https://www.cnblogs.com/zhujiabin/p/5404248.html)

## <a id = "启动模式">启动模式</a>

Standard 模式:

不管有没有已存在的实例，都生成新的实例

SingleTop 模式:

系统发现存在有 FirstActivity 实例,但不是位于栈顶，于是重新生成一个实例。

这就是 singleTop 启动模式，如果发现有对应的 Activity 实例正位于栈顶，则重复利用，不再生成新的实例

SingleTask 模式:

 如果发现有对应的 Activity 实例，则使此 Activity 实例之上的其他 Activity 实例统统出栈，使此 Activity 实例成为栈顶对象，显示到幕前。

SingleInstance 模式:

以上内容参考: http://blog.csdn.net/liuhe688/article/details/6754323/

## <a id = "设置横竖屏">设置横竖屏</a>

```xml-dtd
代码设置
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);//设置成全屏模式  
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);//强制为横屏  
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);//竖屏  

xml 控制
android:screenOrientation属性
landscape,横屏
portrait,竖屏


```

