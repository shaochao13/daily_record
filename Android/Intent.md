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