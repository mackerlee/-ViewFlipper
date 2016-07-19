# -ViewFlipper

Lesson 93 ViewFlipper
1.ViewFlipper:屏幕切换是指在同一个Activity内屏幕间的切换,最常见的情况就是在一个FrameLayout内有多个页面，比如一个系统设置页面，一               个个性化设置页面;
  --简单的ViewAnimator之间，两个或两个以上的View加上动画效果;
  --只有一个子组件会显示在一个时间，即当前时间只能有一个View出现;
  --如果需要每个子组件能自动翻转之间在固定的时间间隔;
  --该类继承类FrameLayout类，ViewAnimator类的作用是FrameLayout里面的View切换提供动画效果;

2.ViewFlipper方法：
  --setInAnimation:设置View进入屏幕时使用的动画，该函数有两个版本，一个接收单个参数，类型为android.view.animation.Animation;一个                   接收两个参数，类型为Context和int,分别为Context对象和定义Animation的resourceID;
  --setOutAnimation:设置View退出屏幕时候使用的动画，参数setInAnimation函数一样；
  --showNext:调用该函数来显示FrameLayout里面的下一个View;
  --showPrevious:调用该函数来显示FrameLayout里面的上一个View;
