1. 给主活动指定的label不仅会成为标题栏中的内容，还会成为启动器(Launcher)中应用程序显示的名称。
2. Activity 状态： 运行状态，暂停状态，停止状态，销毁状态.
3. **`Activity 生命周期`**：   

    - `onCreate()` 在第一次创建的时候被调用。 在此方法中应完成Activity的初始化操作，比如加载布局、绑定事件等等。
    - `onStart()` 在Activity 由不可见变为可见的时候调用。
    - `onResume()` 在Activity 准备好和用户进行交互的时候调用。此时Activity一定位于返回栈的栈顶，处于运行状态。
    - `onPause()` 在系统准备去启动或者恢复另一个Activity时调用。 `通常在这个方法中将一些消耗CPU的资源释放，以及保存一些关键数据`，但这个方法中的执行速度一定要快，不然会影响到新的栈顶Activity的使用。
    - `onStop()` 在Activity完全不可见的时候调用。它与`onPause()`的主要区别在于，如果新的Activity是一个对话框时，`onPause()`方法会得到执行，而`onStop()`并不会执行。
    - `onDestroy()` 在Activity被销毁之前调用，之后Activity的状态将变为销毁状态。
    - `onRestart()` 在Activity由停止状态变为运行状态之前调用，即Activity被重新启动。

    > 完整生存期：`onCreate()` ---> `onDestroy()` 之间所经历的，就是完整生存期。     
    > 可见生存期：`onStart()` ---> `onStop()` 之间所经历的，就是可见生存期。     
    > 前台生存期：`onResume()` ---> `onPause()` 之间所经历的，就是前台生存期。   

4. Activity 启动模式
    - `standard`
    - `singleTop` -- 当启动Activity时，如果发现返回栈的栈顶已经是该Activity，则会直接使用它，而不会再创建新的Activity实例。
    - `singleTask` -- 每次启动该活动时系统首先会在返回栈中检查是否存在该Activity的实例，如果发现已经存在则直接使用该实例，并把在这个活动之上的所有活动统统出栈，如果没有发现就会创建一个新的Activity实例。
    - `singleInstance` -- 会启动一个新的返回栈来管理这个Activity。
    
 
*Methods*

- `public boolean onCreateOptionsMenu(Menu menu)`   用于生成 menu

- `public boolean onOptionsItemSelected(MenuItem item)` 用于处理menu中的点击事件

- `protected void onActivityResult(int requestCode, int resultCode, Intent data)` 用于处理接受从其他Activity返回时带的数据

- `startActivityForResult` 用加载新的Activity，并能接受返回的数据

- `startActivity` 加载新的Activity

- `public void onBackPressed()` -- 当按手机的“返回”键时执行

- `finish()` -- 用于“杀”死当前Activity

- `protected void onSaveInstanceState(Bundle outState)` 在Activity被回收之前一定会被调用。

- `android.os.Process.killProcess(android.os.Process.myPid())` -- 用于杀掉当前进程，以保证程序完全退出， 此方法只能用于杀掉当前程序的进程，而`不能使用这个方法去杀掉其他程序`。