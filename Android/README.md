Android 的图形用户界面是由多个View 和 ViewGroup 构建出来的。View是通用的UI窗体小组件，比如按钮(Button) 或文本框(text field)，而ViewGroup是不可见的，是用于定义子View布局方式的容器，比如网格部件(grid)和垂直列表部件(list)。 

# 四大组件：

1. [Activity >>](./Activity.md)

    [Fragment(碎片) >>](./Fragment.md)   

    [Intent >>](./Intent.md) 
2. Service
3. [Broadcast Receiver >>](./Broadcast_Receiver.md)
4. [Content Provider >>](./Content_Provider.md)

# 代码实例：

1. [调用摄像头和相册 代码详例>>](./调用摄像头和相册.md)

2. [播放多媒体文件 代码详例>>](./播放多媒体文件.md) 

3. [用于进行调试用的日志工具类 LogUtil 代码>>](./tools_codes/LogUtil.md)

4. 打电话功能：   
    ```java
    button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Intent.ACTION_DIAL);
                intent.setData(Uri.parse("tel:10086"));
                startActivity(intent);
            }
        });
    ```

5. [返回数据给上一个Activity](./Intent.md#startActivityForResult)

危险权限列表:
![生命周期](./images/危险权限列表.png) 

## [文件存储 详情>>](./持久化.md)


## build.gradle文件说明：    

+ `apply plugin: 'com.android.application'` -- 表示这是一个应用程序模块。
+ `apply plugin: 'com.android.library` -- 表示这是一个库模块。

```gradle
android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "android.coolweather_test.com.coolweatherdemo"  # 用于指定项目的包名
        minSdkVersion 15 #用于指定项目最低兼容的android系统版本,“15”表示最低兼容到android4.0系统。
        targetSdkVersion 25  
        versionCode 1  # 用于指定项目的版本号
        versionName "1.0" # 用于指定项目的版本名
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false # 表示是否要进行代码混淆
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
} 
```
+ Android Studio 项目一共有3种依赖方式：本地依赖、库依赖和远程依赖。
 
# [布局 >>](.\布局.md)

# 使用***ProGuard***混淆代码。


#

1. 隐藏系统自带的标题栏   
```java
import android.support.v7.app.ActionBar;

ActionBar actionBar = getSupportActionBar();//获取系统的标题栏对象
if (actionBar != null){
    actionBar.hide();
}
```

2. *ArrayAdapter< T >* 用法实例
```java
FruitAdapter adapter = new FruitAdapter(MainActivity.this, R.layout.fruit_item, fruitList);


public class FruitAdapter extends ArrayAdapter<Fruit> {

    //item 的 layout ID
    private int resourceId;

    public FruitAdapter(@NonNull Context context, @LayoutRes int resource, @NonNull List<Fruit> objects) {
        super(context, resource, objects);
        resourceId = resource;
    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = getItem(position);
        View view;
        ViewHolder viewHolder;
        if (convertView == null) {//当系统中没有缓存View时
            view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);//标准写法
            viewHolder = new ViewHolder();
            viewHolder.fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
            viewHolder.fruitName = (TextView) view.findViewById(R.id.fruit_name);

            view.setTag(viewHolder);
        }else{
            view = convertView;
            viewHolder = (ViewHolder) view.getTag();
        }

        viewHolder.fruitImage.setImageResource(fruit.getImageId());
        viewHolder.fruitName.setText(fruit.getName());

        return view;
    }

    class ViewHolder{
        ImageView fruitImage;
        TextView fruitName;
    }
}
```

3. *RecyclerView* [用法>>](./recyclerview.md)    
RecyclerView 属于新增的控件。需要手动添加设置:  
在app/build.gradle文件中，进行如下设置：    
    ```gradle
    dependencies{
        compile 'com.android.support:recyclerview-v7:25.2.0' #数字可能会有所不同。
    }
    ``` 


4. draw9patch  9-patch  点9图片文件  

    在图片的四个边框绘制一个个的小黑点， 在上边框 和左边框 绘制的部分表示当图片需要拉伸时就拉伸黑点标记的区域， 在下边框 和 右边框 绘制的部分表示内容会被放置的区域。
