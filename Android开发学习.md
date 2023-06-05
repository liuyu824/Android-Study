

#### 



#### 3.1.2 EditView 编辑文本框

```xml
<EditView
	//属性列表/>
```



#### 3.1.4 RadioButton 单选按钮

在radioGroup中包含的radioButton只能选择一个选项。

```xml
<RadioGroup
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:orientation="vertical">

	<RadioButton
		android:id="@+id/radio0"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/Male"
    android:checked="true"/>

  <RadioButton
		android:id="@+id/radio1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/Female"/>

</RadioGroup>
```

在获取单选框的值时，有2种情况：

- 改变单选按钮组的值时获取

```java
RadioGroup rg = findViewById(R.id.radioGroup1);
rg.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
	@Override
	public void onCheckedChanged(RadioGroup group, int checkedId) {
		RadioButton radioButton = findViewById(checkedId);
		Log.d((String) radioButton.getText(), "onCheckedChanged: ");
	}
});
```

- 单击其他按钮时获取

```java
Button btn_sure = findViewById(R.id.sureButton);
        RadioGroup rg = findViewById(R.id.radioGroup1);
        btn_sure.setOnClickListener(v -> {
            Log.d("TAG", "onCreate: 1");
            for (int i = 0; i <= rg.getChildCount()-1; i++) {
                Log.d("TAG", "onCreate: 2");
                RadioButton r = (RadioButton) rg.getChildAt(i);
                if (r.isChecked()){
                    Log.d((String) r.getText(), "onClick: ");
                }
            }
        });
```



####  3.1.5 CheckBox复选框

CheckBox 和 radioButton类似

```xml
<CheckBox
	android:id="@+id/basketball"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:text="@string/basketball"/>
```

```java
CheckBox cb_basketball = findViewById(R.id.basketball);
//设定点击事件
cb_basketball.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
	@Override
	public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
		Log.d("TAG", "onCheckedChanged: 篮球爱好复选框被点击了");
	}
});
```



#### 3.1.6 ImageView 图像视图

```xml
<ImageView
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
  android:maxWidth="50dp"
  android:maxHeight="50dp"
  android:adjustViewBounds="true"
  android:src="@drawable/ASUS"
  android:contentDescription="@string/ig_desc"/>
```

android:maxWidth和android:maxHeight设置最大值后，

需要将android:adjustViewBounds设置为true，才能起作用。

imageView的属性可以在xml文件中设置，也可以在java文件中设置，

可以通过设置ImageView的scaleType属性，

对图形进行上下左右的定义。



#### 3.1.7 Spinner 列表选择框

在values文件夹下新建arrays.xml文件，

在arrays.xml文件中，新添加string-array元素，例如：

```xml
<string-array name="ctype">
	<item>身份证</item>
	<item>学生证</item>
	<item>军人证</item>
	<item>工作证</item>
	<item>其他</item>
</string-array>
```

在页面文件（xml文件）中，使用Spinner元素，例如：

```xml
<Spinner
	android:layout_height="wrap_content"
	android:layout_width="wrap_content"
	android:entries="@array/ctype"/>
```



#### 3.1.8 ListView 列表视图

使用方法和Spinner类似，

元素属性还包括了：

- android: divider
- android: dividerHeight
- android: headerDividersEnabled
- android: footerDividersEnabled

```xml
<ListView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:entries="@array/ctype"/>
```



#### 3.1.9 DatePicker 日期、TimePicker 时间拾取器

为了能选择日期和时间，Android提供了 **DatePicker** 和 **TimePicker** 组件。



#### 3.1.10 计时器





# Context

理解Context

- 可以理解为“上下文”：贯穿整个应用；
- 也可以理解为“运行环境”：它提供了一个应用运行所需要的信息，资源，系统服务等；
- 同样可以理解为“场景”：用户操作 和 系统交互，这一过程就是一个场景，比如Activity之前的切换，服务的启动等都少不了Context。

<img src="/Users/liuyu/Desktop/Android-Study/Screenshots/context体系结构.png" alt="context体系结构" style="zoom: 67%;" align="left"/>





#### TableLayout 表格布局

与GridLayout相似

可以实现单行比例，使用GridLayout时无法实现。

![tableLayout](/Users/liuyu/Desktop/Android-Study/Screenshots/tableLayout.png)



#### FrameLayout 帧布局

| XML属性                   | 描述                                                  |
| ------------------------- | ----------------------------------------------------- |
| android:foreground        | 设置该帧布局容器的前景图像                            |
| android:foregroundGravity | 定义绘制前景图像的gravity属性，即前景图像显示的位置。 |

```xml
<FrameLayout     	 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".FrameLayoutActivity"
    android:foreground="@drawable/ic_launcher_background"
    android:foregroundGravity="bottom|right">
  
		//最底层
    <TextView
        android:layout_width="400px"
        android:layout_height="400px"
        android:layout_gravity="center"
        android:background="#FFFF0000"/>
  
		//中层
    <TextView
        android:layout_width="300px"
        android:layout_height="300px"
        android:layout_gravity="center"
        android:background="#FFFF6600"/>
  
		//最上层
    <TextView
        android:layout_width="200px"
        android:layout_height="200px"
        android:layout_gravity="center"
        android:background="#FFFFEE00"/>
  
</FrameLayout>
```

结果：

![frameLayout](/Users/liuyu/Desktop/Android-Study/Screenshots/frameLayout.png)











## 3.4 按钮触控

Button由TextView派生而来，之间的区别：

- Button拥有默认的按钮背景，TextView默认无背景；
- Button内部文本默认居中对齐，TextView默认靠左对齐；
- Button默认英文字母转为大写，TextView维持原始小写。



#### 点击事件和长按事件

- 监听器，专门监听控件的动作行为。

​	   控件发生了指定动作，监听触发开关执行对应代码逻辑。

- 常用的两种按钮控件的监听器
  - setOnClickListener         —— 点击监听器
  - setLongOnClickListener —— 长按监听器



## 3.5 图像显示





# 23.5.16 学习总结

做出来的东西：

- 计算器的xml界面

- 点击事件，因为页面一共20个button，每一个弄一个onClick事件有点儿不太现实

  - 对每一个button都使用了

    ```xml
    findViewById("btn_id").setOnClickListener(this)
    ```

- 点击事件，点击数字显示数字；点击其他符号，没有反应



遇到的问题：

![截屏2023-05-16 13.29.04](/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-05-16 13.29.04.png)



- xml界面，因为全是<button/>，每一个button代码有很多相似的，想弄成像css文件那种，统一管理button。

  - 解决了，values文件夹新建style.xml

    ```xml
    <style name="calculatorButton">
    	<item name="android:layout_width">0dp</item>
      <item name="android:layout_height">0dp</item>
      <item name="android:layout_columnWeight">1</item>
      <item name="android:layout_rowWeight">1</item>
      <item name="android:textSize">28sp</item>
    </style>
    ```

    

- 太丑，想做圆形按钮，可以让 **android:layout_height 和 android:layout_width**的值相等。可是界面用了 layout_weight 平分，在想如何能获取到平分后的宽度，然后赋值 给layout_height。

  - 解决了，在java文件里设置

    ```xml
    //获取GridLayout
    GridLayout gridLayout = findViewById(R.id.gridLayout);
    Integer columnCount = gridLayout.getColumnCount();
    
    WindowManager wm = (WindowManager)this.getSystemService(Context.WINDOW_SERVICE);
    int width = (wm.getDefaultDisplay().getWidth())/columnCount;
    ```

  - 圆形，在drawable里面新建xml文件，设置solid值，背景颜色，radius值，圆弧度。

    

- 上午主要写了xml，和一些简单的逻辑。目前在想主要的计算逻辑，想法是：
  - 因为 乘除 有优先权， A + B × C
  - 想创建三个数字类型 值，num1 num2 num3
  - 两个string类型 运算符，operator1 operator2
  - 攒够3个才计算一次，把值赋给num1



- 命名问题，
  - 上午在命名按钮的时候，用的：oneButton, addButton, equalButton, 感觉不太行
  - 下午改成了btn_one, btn_add, btn_equal



印象深的：

Activity实现页面跳转。

```xml
Intent intent = new Intent();
Intent.setClass(MainActivity.this,MainActivity2.class);
startActivity(intent);
```

想往button里填充一个图片，填充不了，在网上搜了搜，

然后用了一下<ImageButton>







# 第四章 常用组件

类似于 iOS 中的 viewController

界面跳转：一个activity跳转为另一个activity

### 4.1  Activity起停活动页面

#### 4.1.1  activity 启动&停止

从当前页面跳转到新页面，跳转代码：

```xml
Intent intent = new Intent(源页面.this，目标页面.class)
startActivity(new Intent)
```

从当前页面回到上一个页面，相当于关闭当前页面，返回代码：

```xml
finish(); //结束当前的活动页面
```



#### 4.1.2  activity的生命周期

![Android生命周期](/Users/liuyu/Desktop/Android-Study/Screenshots/Android生命周期.png)

OnCreate()：创建活动。页面布局加载进内存，初始状态。

OnStart()：开始活动。页面显示在屏幕上，就绪状态。

OnResume()：恢复活动。页面进入活跃状态，能够正常交互。

OnPause()：暂停活动。页面暂停，无法与用户正常交互。

OnStop()：停止活动。页面不在屏幕上显示。

OnDestroy()：销毁活动。回收活动占用的系统资源，把页面从内存中清楚。

OnRestart()：重启活动。重新加载内存中的页面数据。

【不要求掌握】OnNewIntent()：重用已有的活动实例。



【初学者只要求掌握】

打开新页面的方法调用顺序为：

- onCreate —> onStart —> onResume

关闭旧页面的方法调用顺序为：

- onPause —> onStop —> onDestroy

  

#### 4.1.3  activity的启动模式

![Android_Activity启动模式](/Users/liuyu/Desktop/Android-Study/Screenshots/Android_Activity启动模式.png)

可以在清单文件AndroidManifest.xml配置启动模式。

属性值填入standard表示采取标准模式。

```xml
<activity android:name=".JumpFirstActivity" android:launchMode="standard"/>
```

##### 栈顶复用模式 singleTop

##### 栈内复用模式 singleTask

##### 全局唯一模式 singleInstance

##### 动态设置启动模式

###### FLAG_ACTIVITY_NEW_TASK

###### FLAG_ACTIVITY_SINGLE_TOP

###### FLAG_ACTIVITY_CLEAR_TOP



### 4.2  在Activity之间传递消息

#### 4.2.1  显式intent和隐式intent

- 显式 Intent，即在Intent构造函数中指定

```java
Intent intent = new Intent();
intent.setClass(this.MainActivity, ActNextActivity.class);
startActivity(intent);
```

- 隐式 Intent，没有明确指定要跳转的目标活动，值给出一个动作字符串让系统自动匹配，属于模糊匹配

通常App不希望向外部暴露活动名称，只给出一个事先定义好的标记串；隐式Intent起到了标记过滤作用。



<a align=center>常见系统动作的取值说明</a>

| Intent类的系统动作常命名 | 系统动作的常量值             | 说明            |
| ------------------------ | ---------------------------- | --------------- |
| ACTION_MAIN              | android.intent.action.MAIN   | App启动时的入口 |
| ACTION_VIEW              | android.intent.action.VIEW   | 向用户显示数据  |
| ACTION_SEND              | android.intent.action.SEND   | 分享内容        |
| ACTION_CALL              | android.intent.action.CALL   | 直接拨号        |
| ACTION_DIAL              | android.intent.action.DIAL   | 准备拨号        |
| ACTION_SENDTO            | android.intent.action.SENDTO | 发送短信        |
| ACTION_ANSWER            | android.intent.action.ANSWER | 接听电话        |

```java
// 此为隐式Intent，设置的动作为ACTION_DIAL，即拨打电话
intent.setAction(Intent.ACTION_DIAL);
// 需要提前设置好电话号码
// 并使用定义好的方式，例如“tel:”
Uri uri = Uri.parse("tel:"+ phoneNum);
startActivity(intent);
```



#### 4.2.2  向下一个Activity发送数据

使用Bundle在Activity之间交换数据

（intent使用Bundle对象存放带传递的数据信息）

```java
Bundle bundle = new Bundle();
bundle.putString("name",变量值)
intent.putExtras(bundle);
startActivity(intent);
```

在新页面接收数据

```java
Bundle bundle = getIntent().getExtras();
// 通过 name 获取 bundle 传递的值
String A = bundle.getString("name");
```



#### 4.2.3  向上一个Activity返回数据

处理下一个页面的应答数据，详细步骤：

- 上一个页面打包好请求数据，调用startActivityForResult方法执行跳转动作
- 下一个页面接收并解析请求数据，进行相应处理
- 下一个页面在返回上一个页面时，打包应答数据并调用setResult方法返回数据包裹
- 上一个页面重写方法onActivityResult，解析获得下一个页面的返回数据。



### 4.3  为Activity补充附加信息

#### 4.3.1  利用资源文件配置字符串

```xml
<String name="string_name">value</String>
```

在java文件中，通过name获取value的值

```java
String name = getString(R.string.name)
// 以便直接在java代码中对TextView等元素进行直接赋值
TextView tv_resource = findViewById(R.id.name_id)
tv_resource.setText(name);
```



#### 4.3.2  利用元数据传递配置信息

在使用第三方的SDK时，此种情况比较常见，例如：

- 高德地图：需要在官网下载一个token
- 微信登录

在整合这些的时候，需要用他们提供好的工具包。

一般android:value的值就是官方提供的token值。

```xml
<meta-data android:name="weather" android:value="晴天">
```

##### 在代码中获取元数据

在java代码中，获取元数据信息的步骤分为下列三步：

- 调用getPackageManager方法获得当前应用的包管理器
- 调用包管理器的getActivityInfo方法获得当前活动的信息对象
- 活动信息对象的metaData是Bundle包裹类型，调用包裹对象的getString即可获得指定名称的参数值。

```java
TextView tv_metaData = findViewById(R.id.tv_metaData);
PackageManager pm = getPackageManager();
ActivityInfo activityInfo = pm.getActivityInfo(getComponentName(),PackageManager.GET_META_DATA);
Bundle bundle_metaData = activityInfo.metaData;
String value = bundle_metaData.getString("weather");
tv_metaData.setText(value);
```



#### 4.3.3  给应用页面注册快捷方式





### 4.4 使用 Fragment

**fragment** 与 **activity** 非常相似，

多个 **fragment** 可以在一个单独的 **activity** 中建立多个UI面板，

也可以在多个 **activity** 中重用 **fragment**。

#### 4.4.1 创建 Fragment

必须创建一个 Fragment 的子类

```java
public class NewsFragment extends Fragment{
  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState){
    //从布局文件news.xml加载一个布局文件
    View v = inflater.inflate(R.layout.news,container, true);
    return v;
  }
}
```



#### 4.4.2 在 Activity 中添加 Fragment

##### 4.4.2.1 直接在布局文件中添加 **Fragment**





##### 4.4.2.2 当 **Activity** 运行时添加 **Fragment**







第五章 中级控件

第六章 数据存储

第七章 高级控件

第八章 自定义控件

第九章 组合控件

第十章 打造安装包



# 第五章 高级用户界面设计

### 5.1 高级组件

#### 5.1.1 AutoCompleteTextView 自动完成文本框

AutoCompleteTextView，用于实现用户输入一定字符后，显示一个下拉菜单，

供用户从中选择，当用户选择某个选项后，按用户选择自动填写该文本。

```java
// 第三步：初始化数据源 --- 这数据源去匹配文本框输入的内容
private static final String[] COUNTRIES = new String[]{
	"北汽研究总院","北汽新能源","北汽集团","北汽越野车"
};

@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_auto_complete_text_view);

  // 第一步：初始化控件
  AutoCompleteTextView tv_autoComplete = findViewById(R.id.tv_autoComplete);

  // 第二步：创建一个适配器
  ArrayAdapter<String> adapter = new ArrayAdapter<>
    (this, android.R.layout.simple_dropdown_item_1line, COUNTRIES);
  
  // 第四部：将adapter与当前AutoCOmpleteTextView绑定
  tv_autoComplete.setAdapter(adapter);
 }
```

如何设置在输入第几个字符时进行匹配

```xml
<AutoCompleteTextView
   android:completionThreshold = "1"/>
```



#### 5.1.2 ProgressBar 进度条

ProgressBar

```xml
<!--  水平进度条  -->
<ProgressBar
	android:id="@+id/pb_horizontal"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:max="100"
	style="@android:style/Widget.ProgressBar.Horizontal"/>

<!--  圆形进度条  -->
<ProgressBar
	android:id="@+id/pb_circle"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	style="?android:attr/progressBarStyleLarge"/>
```

.java文件中

```java
public class ProgressBarActivity extends AppCompatActivity {

    private int mProgressStatus;    // 完成进度
    private Handler mHandler;       // 声明一个用于处理消息的handler对象
    private ProgressBar horizonP;   // 水平进度条
    private ProgressBar circleP;    // 圆形进度条

    @SuppressLint("HandlerLeak")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_progress_bar);
        horizonP = findViewById(R.id.pb_horizontal);
        circleP = findViewById(R.id.pb_circle);

        // 声明一个用于处理消息的handler对象
        mHandler = new Handler(){
            @SuppressLint("HandlerLeak")
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == 0x111){
                    horizonP.setProgress(mProgressStatus);
                } else {
                    Toast.makeText(ProgressBarActivity.this, "耗时操作已经完成", Toast.LENGTH_SHORT).show();
                    horizonP.setVisibility(View.GONE);
                    circleP.setVisibility(View.GONE);
                }
            }
        };

        new Thread(new Runnable() {
            public void run(){
                while (true){
                    mProgressStatus = doWork();
                    Message m = new Message();
                    if (mProgressStatus<100){
                        m.what=0x111;
                        mHandler.sendMessage(m);
                    } else {
                        m.what=0x110;
                        mHandler.sendMessage(m);
                        break;
                    }
                }
            }

            //模拟一个耗时操作
            private int doWork(){
                mProgressStatus += Math.random()*10;
                try {
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                return mProgressStatus;
            }
        }).start();
    }
}
```



#### 5.1.3 拖动条和星级评分条

P126页



#### 5.1.4 TabHost 选项卡

选项卡只要由TabHost、TabWidget 和 FrameLayout 3个组件组成，

用于实现一个多标签页的用户界面，通过它可以将一个复杂的对话框分割成若干个标签页。

**现在已经被 TabLayout 以及 ViewPager 替代了。**



#### 5.1.5 图像切换器





#### 5.1.6 网格视图





#### 5.1.7 画廊视图





# 第六章 Android应用核心 Intent

### 6.1 Intent 对象

#### 6.1.1 组件名称（Component Name）



#### 6.1.2 动作（Action）



#### 6.1.3 数据（Data）



#### 6.1.4 种类（Category）



#### 6.1.5 额外（Extra）



#### 6.1.6 标记（Flags）



# 23.5.30 Java中【/】和【%】的区别

【/】除，整数结果相除，结果还是整数（向下取整）

【%】取余，结果为相除之后的余数。



# 23.5.30 新任务 RecyclerView

**希望达到的预期是：**

一个大界面，其中包含了一个六个模块的界面，点开之后，页面展开，里面包含了更多的模块，下方有两个按钮，左边加，右边减。

- RecyclerView.Adapter的写法
- 线性列表 LinearLayoutManager
- 网格列表 GridLayoutManager
- 瀑布流列表 StaggeredGridLayoutManager



RecyclerView如何进行创建：

在activity_main.xml文件里，添加一个recyclerView，作为整体的布局；

新建一个item.xml文件，是recyclerView中的单一item布局。

除此之外，还需要适配器，对recyclerView元素定义，以及对如何循环进行定义。



#### RelativeLayout 与 LinearLayout

- 在LinearLayout中，只能做到一个个按顺序排列；
- 在RelativeLayout中，可以按照自己设置的align或者padding进行随意的排版。



#### ItemDecoration

使用 **ItemDecoration** 可以实现对recyclerView中的元素进行padding设置

```java
outRect.left = divider;
outRect.right = divider;
outRect.top = divider;
outRect.down = divider;
```



- 设置的宽高dp，与windowsManager中.getWidth()方法，获取的值，单位不一样；
  - .getWidth()方法获取出来的值单位是 pixel, 不能放在一起运算。

- 在使用GridLayoutManager时，spanCount是列数，每一列都是使用相同权重进行分布的，

  如果想要实现循环中每一个单一的item元素有特定的排列方式，需要仔细考虑宽度，如下图：

![recyclerView实现上下左右宽度相同](/Users/liuyu/Desktop/Android-Study/Screenshots/recyclerView实现上下左右宽度相同.jpg)

- 在这个item里，不需要定义imageView以及TextView；
  - 可以只创建一个TextView，然后定义他的drawableTop元素



# 在Adapter里获取屏幕的宽度 & 单一item的宽度

```JAVA
WindowManager wm = (WindowManager) parent.getContext().getSystemService(Context.WINDOW_SERVICE);
Display display = wm.getDefaultDisplay();
int width = display.getWidth();              // 获取 整个屏幕的宽度
int vWidth = view.getLayoutParams().width; 
```



