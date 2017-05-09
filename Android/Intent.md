1. 显式 Intent

    例如：
    ```java
    Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
    startActivity(intent);
    ```

2. 隐式 Intent

    指定一系列的action 和 category 等信息，然后交由系统去分析这个Intent， 并找出合适的活动去启动。

    例如：  只有当Intent中的设置与`intent-filter`标签中的设置一致时，`ThirdActivity`才能够响应Intent。
    ```xml
    <activity android:name=".ThirdActivity" android:label="Third Activity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:scheme="http"/>
            </intent-filter>
        </activity>
    ```

3. <div id="startActivityForResult">返回数据给上一个Activity</div>  

```java
//第一个Activity
public class MainActivity extends AppCompatActivity {

    private Button button1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button1 = (Button) findViewById(R.id.button1);
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, SecondActivity.class);
                startActivityForResult(intent, 1); //startActivityForResult
            }
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        switch (requestCode){
            case 1:
                if (resultCode == RESULT_OK){
                    String returnData = data.getStringExtra("data_return");
                }
                break;
            default:
                break;
        }
    }
}

//第二个Activity
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);


        Button button2 = (Button) findViewById(R.id.button2);
        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                returnFirstActivity();
            }
        });
    }

    //当按下Back键时，会执行onBackPressed()方法
    @Override
    public void onBackPressed() {
        returnFirstActivity();
    }

    private void returnFirstActivity(){
        Intent intent = new Intent();
        intent.putExtra("data_return", "Hello");
        setResult(RESULT_OK, intent);
        finish();
    }
}
```