1. 广播类型：
    - 标准广播(Normal broadcasts)
    - 有序广播(Ordered broadcasts)

2. 注册广播的方式：
    - 动态注册（代码中注册）
    - 静态注册（AndroidManifest.xml中注册）

3. 本地广播
    - 不能通过静态注册的方式进行。
    - 只会在本程序内能发送和接收，安全性高。
    - 使用 `LocalBroadcastManager` 对广播进行管理。

    ```java
    public class MainActivity extends AppCompatActivity {

        IntentFilter intentFilter;
        LocalReceiver localReceiver;
        LocalBroadcastManager localBroadcastManager ;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            Button button =(Button) findViewById(R.id.button);

            localBroadcastManager = LocalBroadcastManager.getInstance(this);

            button.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    Intent intent = new Intent("com.example.mybroadcastreceiver.LOCAL_BROADCAST");
                    localBroadcastManager.sendBroadcast(intent);
                }
            });

            intentFilter = new IntentFilter();
            intentFilter.addAction("com.example.mybroadcastreceiver.LOCAL_BROADCAST");
            localReceiver = new LocalReceiver();
            localBroadcastManager.registerReceiver(localReceiver, intentFilter);
        }

        @Override
        protected void onDestroy() {
            super.onDestroy();
            localBroadcastManager.unregisterReceiver(localReceiver);
        }

        class LocalReceiver extends BroadcastReceiver{
            @Override
            public void onReceive(Context context, Intent intent) {
                Toast.makeText(context,"received local broadcast", Toast.LENGTH_SHORT).show();
            }
        }
    }
    ```
