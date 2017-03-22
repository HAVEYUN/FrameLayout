# FrameLayout
霓虹灯效果

布局文件

<?xml version="1.0" encoding="utf-8"?>
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="zzy.fragment.MainActivity">

    <TextView
        android:id="@+id/view1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="320dp"
        android:height="320dp"
        android:background="#f00"/>
    <TextView
        android:id="@+id/view2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="270dp"
        android:height="270dp"
        android:background="#0f0"/>
    <TextView
        android:id="@+id/view3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="220dp"
        android:height="220dp"
        android:background="#00f"/>
    <TextView
        android:id="@+id/view4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="170dp"
        android:height="170dp"
        android:background="#ff0"/>
    <TextView
        android:id="@+id/view5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="120dp"
        android:height="120dp"
        android:background="#f0f"/>
    <TextView
        android:id="@+id/view6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:width="70dp"
        android:height="70dp"
        android:background="#0ff"/>
</FrameLayout>

color文件


    <color name="color1">#ff4040</color>
    <color name="color2">#fff240</color>
    <color name="color3">#43ff40</color>
    <color name="color4">#4053ff</color>
    <color name="color5">#f540ff</color>
    <color name="color6">#40fff5</color>
	
	
	
ublic class MainActivity extends AppCompatActivity {

    private int currentColor = 0;
    final int[] colors = new int[]{
            R.color.color1,
            R.color.color2,
            R.color.color3,
            R.color.color4,
            R.color.color5,
            R.color.color6
    };
    final int[] names = new int[]{
            R.id.view1,
            R.id.view2,
            R.id.view3,
            R.id.view4,
            R.id.view5,
            R.id.view6
    };

    TextView[] mViews = new TextView[names.length];

    Handler mHandler = new Handler() {
        @Override
        public void handleMessage(Message msg) {

            if (msg.what == 0X123) {
                for (int i = 0; i < names.length; i++) {
                    mViews[i].setBackgroundResource(colors[(i + currentColor) % names.length]);
                }

                currentColor++;

            }
            super.handleMessage(msg);
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        for (int i = 0; i < names.length; i++) {
            mViews[i] = (TextView) findViewById(names[i]);
        }

        // 定义一个线程周期性地改变 currentColor 变量值
        new Timer().schedule(new TimerTask() {
            @Override
            public void run() {
                // 发送一条空消息通知系统改变 6 个TextView 组件的背景色
                mHandler.sendEmptyMessage(0x123);
            }
        }, 0, 200);

    }
}
	
		
