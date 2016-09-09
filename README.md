# XiaoBingSplashMoreMethod
 【Android】android开发之splash闪屏页的四种实现方式，启动页的实现教程。
作者：程序员小冰，CSDN博客：http://blog.csdn.net/qq_21376985
QQ986945193 微博：http://weibo.com/mcxiaobing
首先给大家看一下今天实现的效果图（其他三种都差不太多底下详细介绍）：
![效果图请看：](http://img.blog.csdn.net/20160909104841533?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

这个启动页实现的方法是四种，两种是利用handler，其它两种是利用了动画的方式。
具体给大家贴一下源代码吧，很简单。
布局文件就一个图片，mainfest添加上我们的类就行了。
java实现代码如下：
package xiaobingsplashmoremethod.qq986945193.xiaobingsplashmoremethod.xiaobingsplashmoremethod;

import android.annotation.SuppressLint;
import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.view.animation.AlphaAnimation;
import android.view.animation.Animation;
import android.view.animation.AnimationSet;
import android.view.animation.RotateAnimation;
import android.view.animation.ScaleAnimation;
import android.widget.LinearLayout;


/**
 * @author ：程序员小冰
 * @新浪微博 ：http://weibo.com/mcxiaobing
 * @GitHub:https://github.com/QQ986945193
 * @CSDN博客: http://blog.csdn.net/qq_21376985
 * @交流Qq ：986945193
 * 类名：splash闪屏页的四种实现方式
 */
public class SplashActivity extends Activity {
    private LinearLayout ll_splash;
    private Handler mHandler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            super.handleMessage(msg);
            switch (msg.what) {
                case 1:
                    startMainActivity();
                    break;
                case 2:
                    startMainActivity();
                    break;
            }
        }
    };

    @SuppressLint("WrongViewCast")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);

        ll_splash = (LinearLayout) findViewById(R.id.ll_splash);
        /**
         * 第一种方法，利用handler自带的sendEmptyMessageDelayed()方法。
         */
        mHandler.sendEmptyMessageDelayed(1, 2000);

        /**
         * 第二种方法，其实实现原理和第一种是一样的，
         */
//
//        Message message = new Message();
//        message.what = 2;
//        mHandler.sendMessageDelayed(message, 2000);

        /**
         * 第三种方法，利用动画实现
         */
//        startAdimThree();
        /**
         * 第四种方法，利用动画实现
         */
//        StartAniFour();

    }

    private void StartAniFour() {
        AlphaAnimation start = new AlphaAnimation(0.0f, 1.0f);
        start.setDuration(1000);
        // findViewById(R.id.splash).startAnimation(start);
        start.setAnimationListener(new Animation.AnimationListener() {
            @Override
            public void onAnimationStart(Animation animation) {

            }

            @Override
            public void onAnimationEnd(Animation animation) {
                startMainActivity();
            }

            @Override
            public void onAnimationRepeat(Animation animation) {

            }
        });
        ll_splash.startAnimation(start);
    }


    /**
     * 开启动画
     */
    private void startAdimThree() {
        // 动画集合
        AnimationSet set = new AnimationSet(false);
        // 旋转动画
        RotateAnimation rotateAnimation = new RotateAnimation(180, 180,
                Animation.RELATIVE_TO_SELF, 0.5f, Animation.RELATIVE_TO_SELF,
                0.5f);
        rotateAnimation.setDuration(2000);// 设置动画时间
        rotateAnimation.setFillAfter(true);// 保持动画状态

        // 缩放动画
        ScaleAnimation scaleAnimation = new ScaleAnimation(0, 1, 0, 1,
                Animation.RELATIVE_TO_SELF, 0.5f, Animation.RELATIVE_TO_SELF,
                0.5f);
        scaleAnimation.setDuration(2000);// 设置动画时间
        scaleAnimation.setFillAfter(true);// 保持动画状态

        // 渐变动画

        AlphaAnimation alphaAnimation = new AlphaAnimation(0, 1);
        alphaAnimation.setDuration(2000);
        alphaAnimation.setFillAfter(true);// 保持动画状态

        // 添加动画
        set.addAnimation(rotateAnimation);
        set.addAnimation(scaleAnimation);
        set.addAnimation(alphaAnimation);
        /*
         * 设置动画的监听事件，当动画运行完成后，启动新的activity
		 */
        set.setAnimationListener(new Animation.AnimationListener() {

            @Override
            public void onAnimationStart(Animation animation) {
                // TODO Auto-generated method stub

            }

            @Override
            public void onAnimationRepeat(Animation animation) {
                // TODO Auto-generated method stub

            }

            @Override
            public void onAnimationEnd(Animation animation) {
                // TODO Auto-generated method stub
                startMainActivity();
            }
        });

        ll_splash.startAnimation(set);

    }


    /**
     * 跳转到主界面
     */
    private void startMainActivity() {
        startActivity(new Intent(SplashActivity.this, MainActivity.class));
        finish();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
//        mHandler.removeMessages(1);
//        mHandler.removeMessages(2);
    }
}

如果对您有帮助，欢迎star，fork。。。
