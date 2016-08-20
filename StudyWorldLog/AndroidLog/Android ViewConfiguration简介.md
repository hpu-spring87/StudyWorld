# .ViewConfiguration

### 简介

ViewConfiguration 这个类主要定义了UI中所使用到的标准常量，包含各种基础数据：超时，大小和距离.

ViewConfiguration中的值一般是在编写高级控件是才会用到。比如各种滑动控件里面.

### 使用

1. 获取ViewConfiguration对象，由于ViewConfiguration的构造方法为私有的，只能通过这个静态方法来获取到该对象。

```
ViewConfiguration configure = ViewConfiguration.get(context);

```

2. 通过该对象调用相关的函数，将返回相关的常量数据。

附上源码：

```
/**
 * 包含了方法和标准的常量用来设置UI的超时、大小和距离
 */  
public class ViewConfiguration {  
    // 设定水平滚动条的宽度和垂直滚动条的高度，单位是像素px  
    private static final int SCROLL_BAR_SIZE = 10;  

    //定义滚动条逐渐消失的时间，单位是毫秒  
    private static final int SCROLL_BAR_FADE_DURATION = 250;  

    // 默认的滚动条多少秒之后消失，单位是毫秒  
    private static final int SCROLL_BAR_DEFAULT_DELAY = 300;  

    // 定义边缘地方褪色的长度  
    private static final int FADING_EDGE_LENGTH = 12;  

    //定义子控件按下状态的持续事件  
    private static final int PRESSED_STATE_DURATION = 125;  

    //定义一个按下状态转变成长按状态的转变时间  
    private static final int LONG_PRESS_TIMEOUT = 500;  

    //定义用户在按住适当按钮，弹出全局的对话框的持续时间  
    private static final int GLOBAL_ACTIONS_KEY_TIMEOUT = 500;  

    //定义一个touch事件中是点击事件还是一个滑动事件所需的时间，如果用户在这个时间之内滑动，那么就认为是一个点击事件  
    private static final int TAP_TIMEOUT = 115;  

    /**
     * Defines the duration in milliseconds we will wait to see if a touch event  
     * is a jump tap. If the user does not complete the jump tap within this interval, it is
     * considered to be a tap.  
     */  
    //定义一个touch事件时候是一个点击事件。如果用户在这个时间内没有完成这个点击，那么就认为是一个点击事件  
    private static final int JUMP_TAP_TIMEOUT = 500;  

    //定义双击事件的间隔时间  
    private static final int DOUBLE_TAP_TIMEOUT = 300;  

    //定义一个缩放控制反馈到用户界面的时间  
    private static final int ZOOM_CONTROLS_TIMEOUT = 3000;  

    /**
     * Inset in pixels to look for touchable content when the user touches the edge of the screen
     */  
    private static final int EDGE_SLOP = 12;  

    /**
     * Distance a touch can wander before we think the user is scrolling in pixels
     */  
    private static final int TOUCH_SLOP = 16;  

    /**
     * Distance a touch can wander before we think the user is attempting a paged scroll
     * (in dips)
     */  
    private static final int PAGING_TOUCH_SLOP = TOUCH_SLOP * 2;  

    /**
     * Distance between the first touch and second touch to still be considered a double tap
     */  
    private static final int DOUBLE_TAP_SLOP = 100;  

    /**
     * Distance a touch needs to be outside of a window's bounds for it to
     * count as outside for purposes of dismissing the window.
     */  
    private static final int WINDOW_TOUCH_SLOP = 16;  

   //用来初始化fling的最小速度，单位是每秒多少像素  
    private static final int MINIMUM_FLING_VELOCITY = 50;  

    //用来初始化fling的最大速度，单位是每秒多少像素  
    private static final int MAXIMUM_FLING_VELOCITY = 4000;  

    //视图绘图缓存的最大尺寸，以字节表示。在ARGB888格式下，这个尺寸应至少等于屏幕的大小  
    @Deprecated  
    private static final int MAXIMUM_DRAWING_CACHE_SIZE = 320 * 480 * 4; // HVGA screen, ARGB8888  

    //flings和scrolls摩擦力度大小的系数  
    private static float SCROLL_FRICTION = 0.015f;  

    /**
     * Max distance to over scroll for edge effects
     */  
    private static final int OVERSCROLL_DISTANCE = 0;  

    /**
     * Max distance to over fling for edge effects
     */  
    private static final int OVERFLING_DISTANCE = 4;  

}  

```


项目中用到的就是屏蔽scrollview的滑动，这时候会用到判断用户是否为滑动操作的一个滑动常量值，根据这个值判断是否为滑动行为。如下：

```

package com.edaixi.uikit.view;

import android.content.Context;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.view.ViewConfiguration;
import android.widget.ScrollView;

/**
 * Copyright © 2016 edaixi. All Rights Reserved.
 * Author: wei_spring
 * Date: 16/8/19
 * Email:weichsh@edaixi.com
 * Function: 自定义Scrollview,拦截滑动事件,解决与Recycler的滑动冲突
 */
public class RecyclerScrollview extends ScrollView {
    private int downY;
    private int mTouchSlop;

    public RecyclerScrollview(Context context) {
        super(context);
        mTouchSlop = ViewConfiguration.get(context).getScaledTouchSlop();
    }

    public RecyclerScrollview(Context context, AttributeSet attrs) {
        super(context, attrs);
        mTouchSlop = ViewConfiguration.get(context).getScaledTouchSlop();
    }

    public RecyclerScrollview(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        mTouchSlop = ViewConfiguration.get(context).getScaledTouchSlop();
    }

    @Override
    public boolean onInterceptTouchEvent(MotionEvent e) {
        int action = e.getAction();
        switch (action) {
            case MotionEvent.ACTION_DOWN:
                downY = (int) e.getRawY();
                break;
            case MotionEvent.ACTION_MOVE:
                int moveY = (int) e.getRawY();
                if (Math.abs(moveY - downY) > mTouchSlop) {
                    return true;
                }
        }
        return super.onInterceptTouchEvent(e);
    }
}


```
