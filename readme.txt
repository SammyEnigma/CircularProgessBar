CircularProgessBar是一个基于Qt widget开发的圆形进度条组件。

该组件目前仅提供一个环形风格的进度条，通过2D绘图(QPainter)的方式绘制。其绘制原理就是先通过外圆和内圆分割出一个环形进度条，然后使用drawArc()在环形内绘制弧度展示当前进度，并在内圆中心绘制显示的文本。该组件由单独一个类(CircularProgessBar)实现，项目下的widget用于测试接口功能，提供了一组不同样式的环形进度条示例。

CircularProgessBar类提供了一些常用功能的对外接口，可通过这些接口设计不同样式风格的进度条，有关接口的具体功能详见代码注释，这里仅阐述使用该组件的大体流程：
//设置圆形(弧形/外圆/内圆/)占比，可以在需要调整圆环进度条各部分大小比例时调用
void setCircleRatio();
//设置圆形(外圆/内圆)画笔，因为外圆与内圆的颜色是通过画刷填充的，默认不设置画笔，可以在需要为其绘制边缘线时调用
void setCirclePen();
//设置圆形(外圆/内圆)画刷，设置外圆与内圆的颜色，因为内圆颜色覆盖了外圆的中间部分，所以这里外圆的颜色实际就是环形的颜色
void setCircleBrush();
//设置弧形画笔，进度条长什么样就是通过这里设置的
void setArcPenBrush();//画刷 进度条的颜色
void setArcPenDashPattern();//虚线模式 
void setArcPenGradient();//渐变色
//设置文本属性，可以设置中间显示文本的颜色、字体
void setTextProperty();

//下面两个方法内部会调用update()刷新显示，用来显示文本与进度
void setText(const QString &text);//设置显示的文本
void setProgressValue(const qreal &progressValue);//设置进度值


该组件核心绘图代码在drawCircleProgressBar()方法内，仅仅使用了QPainter的几个函数，功能相对简单，能绘制的样式风格也比较单一，但基本上能实现一些常见的环形进度条的样式。其实也考虑过在该组件中提供更多风格样式进度条的接口，但这就需要添加更多的标志变量，降低了代码的可读性和执行效率，增加了程序复杂度和空间占用。所以最终决定不再添加新的风格，真正需要时可以参考这里的绘图代码重新设计。另外该组件没有提供绘制图片（drawPixmap）的功能，当需要使用一些难以手绘的图片做背景时，可以将外圆和内圆的画刷颜色设置一定程度的透明度，然后将该组件布局到背景图片部件之上，调整圆形占比等细节应该也可以实现，实现不了的话那就重新设计吧。


作者联系方式：@为-何-而来(新浪微博)
