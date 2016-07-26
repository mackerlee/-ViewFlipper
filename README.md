# ViewFlipper

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
  
3.ViewFlipper实例：
  在res->layout->activity_main.xml:
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
      //--定义ViewFlipper
      <ViewFlipper
          android:id="@+id/viewFlipper94"
          android:layout_width="match_parent"
          android:layout_height="match_parent">
          
          //--在ViewFlipper定义三个LinerLayout，用于在三个页面内切换
          <LinearLayout
              android:id="@+id/layout94_1"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
              <ImageView
                  android:id="@+id/image94_1"
                  android:src="@drawable/p1"
                  android:layout_width="wrap_content"
                  android:layout_height="wrap_content" />
          </LinearLayout>
  
          <LinearLayout
              android:id="@+id/layout94_2"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
              <ImageView
                  android:id="@+id/image94_2"
                  android:src="@drawable/p3"
                  android:layout_width="wrap_content"
                  android:layout_height="wrap_content" />
          </LinearLayout>
  
          <LinearLayout
              android:id="@+id/layout94_3"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
              <ImageView
                  android:id="@+id/image94_3"
                  android:src="@drawable/p4"
                  android:layout_width="wrap_content"
                  android:layout_height="wrap_content" />
          </LinearLayout>
      </ViewFlipper>
  </LinearLayout>
  
  在res->新建anim文件夹，然后再该文件夹下新建4个.xml文件用于屏幕切换动画效果：
  in_leftright.xml:
  <?xml version="1.0" encoding="utf-8"?> <!-- 在res目录下 新建resource directory 命名为anim -->
  <translate xmlns:android="http://schemas.android.com/apk/res/android"
      android:duration="3000"
      android:fromXDelta="-100%p"
      android:toXDelta="0">
  
  </translate>
  
  out_leftright.xml:
  <?xml version="1.0" encoding="utf-8"?> <!-- 在res目录下 新建resource directory 命名为anim -->
  <translate xmlns:android="http://schemas.android.com/apk/res/android"
      android:duration="3000"
      android:fromXDelta="0"
      android:toXDelta="100%p">
  
  </translate>
  
  in_rightleft.xml:
  <?xml version="1.0" encoding="utf-8"?> <!-- 在res目录下 新建resource directory 命名为anim -->
  <translate xmlns:android="http://schemas.android.com/apk/res/android"
      android:duration="3000"
      android:fromXDelta="100%p"
      android:toXDelta="0">
  
  </translate>
  
  out_rightleft.xml:
  <?xml version="1.0" encoding="utf-8"?> <!-- 在res目录下 新建resource directory 命名为anim -->
  <translate xmlns:android="http://schemas.android.com/apk/res/android"
      android:duration="3000"
      android:fromXDelta="0"
      android:toXDelta="-100%p">
  
  </translate>
  
  在java->包名->MainActivity.java:
  package com.example.mackerlee.android_93;

  import android.support.v7.app.AppCompatActivity;
  import android.os.Bundle;
  import android.view.MotionEvent;
  import android.widget.ViewFlipper;
  import android.widget.ViewSwitcher;
  
  public class MainActivity extends AppCompatActivity {
  
      private ViewFlipper viewFlipper;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          viewFlipper = (ViewFlipper)findViewById(R.id.viewFlipper94);
      }
  
      float startX = 0; //获取触屏按下的初始坐标
      float endX = 0;
      //--重写触屏事件方法
      @Override
      public boolean onTouchEvent(MotionEvent event) {
          int action = event.getAction();
          switch (action){
              case MotionEvent.ACTION_DOWN:
                  startX = event.getX();
                  break;
              case MotionEvent.ACTION_UP:
                  //--从左向右滑动
                  if(event.getX()>startX){
                      viewFlipper.setInAnimation(this,R.anim.in_leftright);
                      viewFlipper.setOutAnimation(this,R.anim.out_leftright);
                      viewFlipper.showNext(); //显示下一个视图
                  }else if(event.getX()<startX){ //向左滑动:从右到左滑动
                      viewFlipper.setInAnimation(this,R.anim.in_rightleft);
                      viewFlipper.setOutAnimation(this,R.anim.out_rightleft);
                      viewFlipper.showPrevious();//显示上一个视图
                  }
                  break;
              default:
                  break;
          }
          return super.onTouchEvent(event);
      }
  }


