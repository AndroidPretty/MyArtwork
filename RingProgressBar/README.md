#圆形、环形进度条使用说明

**1、在layout的xml中添加如下代码：**

```
<RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    <io.netopen.hotbitmapgg.library.view.RingProgressBar
        android:id="@+id/progress_bar_1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:layout_alignParentTop="true"
        app:max="100"
        android:layout_marginTop="100dp"
        app:ringColor="@color/colorPrimary"
        app:ringProgressColor="@color/colorPrimaryDark"
        app:ringWidth="3dp"
        app:style="FILL"
        app:textColor="@color/colorPrimary"
        app:textIsShow="true"
        app:textSize="16sp" />



    <io.netopen.hotbitmapgg.library.view.RingProgressBar
        android:id="@+id/progress_bar_2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:layout_alignParentBottom="true"
        android:layout_marginBottom="100dp"
        app:max="100"
        app:ringColor="@android:color/darker_gray"
        app:ringProgressColor="@color/colorPrimary"
        app:ringWidth="3dp"
        app:style="STROKE"
        app:textColor="@color/colorPrimary"
        app:textIsShow="true"
        app:textSize="16sp" />
</RelativeLayout>
```
**2、在相对应的java文件中添加如下代码：**

```
private RingProgressBar mRingProgressBar1;

private RingProgressBar mRingProgressBar2;

private int progress = 0;

private Handler mHandler = new Handler()
{

    @Override
    public void handleMessage(Message msg)
    {

        if (msg.what == 0)
        {
            if(progress < 100)
            {
                progress++;
                mRingProgressBar1.setProgress(progress);
                mRingProgressBar2.setProgress(progress);
                mRingProgressBar1.setOnProgressListener(new RingProgressBar.OnProgressListener()
                {

                    @Override
                    public void progressToComplete()
                    {
                        // Here after the completion of the processing
                    }
                });

                mRingProgressBar2.setOnProgressListener(new RingProgressBar.OnProgressListener()
                {

                    @Override
                    public void progressToComplete()
                    {
                        // Here after the completion of the processing
                    }
                });
            }

        }
    }
};

@Override
protected void onCreate(Bundle savedInstanceState)
{

    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    mRingProgressBar1 = (RingProgressBar) findViewById(R.id.progress_bar_1);
    mRingProgressBar2 = (RingProgressBar) findViewById(R.id.progress_bar_2);

    new Thread(new Runnable()
    {

        @Override
        public void run()
        {

            for (int i = 0; i < 100; i++)
            {
                try
                {
                    Thread.sleep(100);

                    mHandler.sendEmptyMessage(0);
                } catch (InterruptedException e)
                {
                    e.printStackTrace();
                }
            }
        }
    }).start();
}

@Override
protected void onDestroy()
{

    super.onDestroy();

    mHandler.removeCallbacksAndMessages(null);
}
```
**3、运行即可查看效果**