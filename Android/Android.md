Android 的图形用户界面是由多个View 和 ViewGroup 构建出来的。View是通用的UI窗体小组件，比如按钮(Button) 或文本框(text field)，而ViewGroup是不可见的，是用于定义子View布局方式的容器，比如网格部件(grid)和垂直列表部件(list)。    
# Activity
# Service
# Broadcast Receiver
# Content Provider

# 布局
## LinearLayout  
LinearLayout是***ViewGroup***的一个子类，用于放置水平或者垂直方向的子视图部件，放置方向由属性***android:orientation***设定。LinearLayout里的子布局按照XML里定义的顺序显示在屏幕上。     

- android:hint  
当文本框为空的时候,会默认显示这个字符串    
- android:layout_weight     
***权重***的值指的是每个部件所占剩余空间的大小，该值与同级部件所占空间大小有关。就类似于饮料的成分配方：“两份伏特加酒，一份咖啡利口酒”，即该酒中伏特加酒占三分之二。例如，我们设置一个View的权重是2，另一个View的权重是1，那么总数就是3，这时第一个View占据2/3的空间，第二个占据1/3的空间。如果你再加入第三个View，权重设为1，那么第一个View(权重为2的)会占据1/2的空间，剩余的另外两个View各占1/4。(请注意，使用权重的前提一般是给View的宽或者高的大小设置为0dp，然后系统根据上面的权重规则来计算View应该占据的空间。但是很多情况下，如果给View设置了match_parent的属性，那么上面计算权重时则不是通常的正比，而是反比，也就是权重值大的反而占据空间小)。      
对于所有的View默认的权重是0，如果只设置了一个View的权重大于0，则该View将占据除去别的View本身占据的空间的所有剩余空间。    
**为了提升布局的效率，在设置权重的时候，应该把EditText的宽度设为0dp。**     


# 使用***ProGuard***混淆代码。
# 

