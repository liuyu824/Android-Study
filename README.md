# Android-Study

## 第1章  Android开发环境搭建

## 第2章  Android App开发基础

## 第3章  简单控件

### 3.1 文本显示

#### 3.1.1 设置文本的内容

设置文本的两种方式：

1. xml文件 ***Android:text*** 设置
2. Java代码中调用文本视图对象的setText方法设置

```xml
<TextView
	//属性列表/>
```

androidStudio中不推荐直接对text进行定义

```xml
//建议在 [strings.xml] 文件中
//通过 name 与 string 进行键值对赋值
//通过 @string/name 进行调用
<resources>
  <string name=""></string>
</resources>
```



#### 3.1.2 设置文本的大小

在xml文件中：

```xml
<TextView
	android:textSize = "__dp"/>
```

xml文件要求在字号数字后面写明单位类型，

常见的字号单位主要有px、dp、sp 3种。

1. **px: ** pixel像素，px是手机屏幕的最小显示单位

2. **dp: ** (device independent pixels)

3. **sp: **   (Scale-independent pixel)

| 名称                   | 解释                                                         |
| :--------------------- | ------------------------------------------------------------ |
| px（Pixel像素）        | 图像元素， 图像的基本构成单元，单个像素的大小并不固定，跟随屏幕大小和像素数量变化，一个像素点为1px。 |
| Resolution（分辨率）   | 屏幕垂直和水平方向的像素数量，if（1920*1080），即垂直1920个像素，水平1080个像素。 |
| Dpi（像素密度）        | 是指屏幕上每英寸距离中有多少个像素点。                       |
| Density（密度）        | 是指屏幕上每平方英寸中含有的像素点数量。                     |
| Dip/dp（设备独立像素） | 长度单位。                                                   |



#### 3.1.3 设置文本的颜色

在Android默认中，Color里定义了12种颜色。

| Color类种的颜色类型 | 说明 | Color类种的颜色类型 | 说明 |
| ------------------- | ---- | ------------------- | ---- |
| BLACK               | 黑色 | GREEN               | 绿色 |
| DKGRAY              | 深灰 | BLUE                | 蓝色 |
| GRAY                | 灰色 | YELLOW              | 黄色 |
| LTGRAY              | 浅灰 | CYAN                | 青色 |
| WHITE               | 白色 | MAGENTA             | 玫红 |
| RED                 | 红色 | TRANSPARENT         | 透明 |

在xml文件中：

```xml
<TextView
  // 使用 自定颜色
  android:textColor="#000000"/>
```

在java代码中：

```java
TextView tv_margin = findViewById(R.id.tv_margin);
// 使用自带color类中颜色
tv_margin.setTextColor(Color.GREEN);
```



### 3.2 视图基础

#### 3.2.1 设置视图的宽高

在xml代码中：

- match_parent：与上级视图保持一致
- wrap_content：与内容自适应
- 以dp为单位的具体尺寸

在java代码中使用ViewGroup.LayoutParams参数类型：

- getLayoutParams()
- setLayoutParams()



#### 公共方法dip2px

定义公共方法 dip2px， 将单位从dp转为pixel，代码实现：

```java
// dpValue 变量输入希望的dp值，例如
public static int dip2px(Context context, float dpValue){
  // 获取当前手机的像素密度
  float scale = context.getResources().getDisplayMetrics().density;
  return (int)(dpValue * scale + 0.5f); // 四舍五入取整
}
```



#### 3.2.2 设置视图的间距

- layout_margin 全部的四周间距

![layoutMargin](/Users/liuyu/Desktop/Android-Study/screenshots/layoutMargin.png)

- layout_marginStart (left)     左间距
- layout_marginEnd (right)    右间距
- layout_marginTop                上间距
- layout_marginBottom         下间距



#### 3.2.3 设置视图的对齐方式

设置视图的对齐方式有2种途径：

- 采用了layout_gravity属性，它指定了当前视图相对于上级视图的对齐方式。
- 采用了gravity属性，它制定了下级视图相对于当前视图的对齐方式。

layout_gravity与gravity的取值包括：left、top、right、bottom，还可以用竖线连接各取值，

例如 “left｜top” 表示即靠左又靠上，也就是朝左上角对齐。

![layout_gravity](/Users/liuyu/Desktop/Android-Study/screenshots/layout_gravity.png)



### 3.3 常用布局

#### 3.3.1 LinearLayout 线性布局

orientation属性值为horizontal：内部视图在水平方向从左往右排列；

orientation属性值为vertical：内部试图在垂直方向从上往下排列；

不指定orientation属性，则LinearLayout默认水平方向排列



LinearLayout可以层层嵌套，每一层再对vertical/horizontal单独定义

**单行等比分块**

```xml
<TextView
	android:layout_width="0dp"
	android:layout_height="wrap_content"
	android:layout_weight="1"
	android:gravity="center"
	android:text="@string/HorizonOne" />
<TextView
	android:layout_width="0dp"
	android:layout_height="wrap_content"
	android:layout_weight="1"
	android:gravity="center"
	android:text="@string/HorizonTwo" />
```

代码块中的android:layout_weight，就是行中每一块的比例，1:1即相同。



#### 3.3.2 RelativeLayout 相对布局

相对布局的下级视图位置由其他视图决定。

用于确定下级视图位置的参照物分两种：

1. 与该视图自身平级的视图
2. 该视图的上级视图（即归属的RelativeLayout）

![截屏2023-05-15 12.58.33](/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-05-15 12.58.33.png)

代码：

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    tools:context=".RelativeLayoutActivity">

    <TextView
        android:id="@+id/tv_message"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tv_relativeAsk"
        android:textSize="30sp"/>

    <Button
        android:id="@+id/btn_true"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/yes"
        android:textSize="20sp"
        android:layout_below="@id/tv_message"
        android:layout_alignEnd="@id/tv_message"/>

    <Button
        android:id="@+id/btn_no"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/no"
        android:textSize="20sp"
        android:layout_below="@id/tv_message"
        android:layout_toStartOf="@id/btn_true"/>

</RelativeLayout>
```



#### 3.3.3 GridLayout 网格布局

网格布局支持多行多列的表格排列

网格布局默认从左往右、从上往下排列，

新增了两个属性：

- ###### columnCount：指定网格列数

- ###### rowCount：指定网格行数



如何实现Grid等比平分屏幕

设置android:layout_width为0

设置android:layout_columnWeight为1

```xml
<TextView
        android:gravity="center"
        android:layout_height="60dp"
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:textColor="#000000"
        android:background="#ffcccc"
        android:text="@string/firstGrid"
        android:textSize="20sp"/>

    <TextView
        android:gravity="center"
        android:layout_height="60dp"
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:text="@string/secondGrid"
        android:background="#ffaa00"
        android:textSize="20sp"/>

    <TextView
        android:gravity="center"
        android:layout_height="60dp"
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:text="@string/thirdGrid"
        android:background="#00ff00"
        android:textSize="20sp"/>

    <TextView
        android:gravity="center"
        android:layout_height="60dp"
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:text="@string/forthGrid"
        android:background="#660066"
        android:textSize="20sp"
        android:textColor="#ffffff"/>
```



#### 3.3.4 ScrollView 滚动视图

滚动视图有两种：

**ScrollView，垂直方向**的滚动视图：

- layout_width属性设置为 match_parent
- layout_height属性设置为 wrap_content

**HorizontalScrollView，水平方向**的滚动视图：

- layout_width属性设置为 wrap_content
- layout_height属性设置为 match_parent 



#### 3.3.5 TableLayout 表格布局

与GridLayout相似, 可以实现单行比例，使用GridLayout时无法实现。

<img src="/Users/liuyu/Desktop/Android-Study/Screenshots/tableLayout.png" alt="tableLayout" align="left"/>



#### 3.3.6 FrameLayout 帧布局

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



### 3.4 按钮触控

#### 3.4.1 按钮控件Button

```xml
<Button
	//属性列表/>
```

Button由TextView派生而来，之间的区别：

- Button拥有默认的按钮背景，TextView默认无背景；
- Button内部文本默认居中对齐，TextView默认靠左对齐；
- Button默认英文字母转为大写，TextView维持原始小写。



#### 3.4.2 点击事件和长按事件

- 监听器，专门监听控件的动作行为。

​	   控件发生了指定动作，监听触发开关执行对应代码逻辑。

- 常用的两种按钮控件的监听器
  - setOnClickListener         —— 点击监听器
  - setOnLongClickListener —— 长按监听器

```java
Button btn_longClk = findViewById(R.id.btn_longClk);
	btn_longClk.setOnLongClickListener(new View.OnLongClickListener() {
		@Override
    public boolean onLongClick(View v) {
			btn_longClk.setText("按钮被长按了");
			return false;
		}
});
```



#### 3.4.3 禁用与恢复按钮

- setEnable
  - true：可以点
  - false：不能点

```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_button_enabled);

        // 获取三个按钮的实体对象
//        Button btn_enable = findViewById(R.id.btn_enable);
//        Button btn_disable = findViewById(R.id.btn_disable);
        btn_test = findViewById(R.id.btn_test);

        // 设置监听器
        findViewById(R.id.btn_enable).setOnClickListener(this);
        findViewById(R.id.btn_disable).setOnClickListener(this);

    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_enable){
            // 设置 btn_enable 点击启用测试按钮事件
            btn_test.setEnabled(true);
            btn_test.setTextColor(Color.WHITE);
        } else {
            // 设置 btn_disable 点击关闭测试按钮事件
            btn_test.setEnabled(false);
            btn_test.setTextColor(Color.GRAY);
        }
    }
```



### 3.5 图像显示

#### 3.5.1 图像视图 ImageView

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



#### 3.5.2 图像按钮 ImageButton

ImageButton主要用于将Button背景设置为自定义的图片。

- layout_width:   Button的宽度
- layout_height:  Button的高度
- scaleType: 
  - 如果图片的宽度高度比Button的宽高要大，默认无法正常显示；
  - 使用【fitCenter】值，可以使图片的尺寸自适应，以完整在Button中显示。

- src:

```xml
// 包含了以下内置属性
<ImageButton
	android:layout_width="wrap_content"
	android:layout_height="60dp"
	android:scaleType="fitCenter"
	android:src="@drawable/ic_launcher_background"/>
```

![imageButton](/Users/liuyu/Desktop/Android-Study/screenshots/imageButton.png)



#### 3.5.3 同时展示文本与图像

```xml
<Button
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:drawableLeft="@drawable/ic_launcher_foreground"
	android:drawablePadding="40dp"
	android:text="同时显示图像与文字"/>
```



#### ScaleType缩放类型取值说明

| XML中的缩放类型 | ScaleType类中的缩放类型 | 说明                                                     |
| --------------- | ----------------------- | -------------------------------------------------------- |
| fitCenter       | FIT_CENTER              | 保持宽高比例，缩放图片使其位于视图中间                   |
| centerCrop      | CENTER_CROP             | 缩放图片使其充满视图（超出部分会被裁减），并位于视图中间 |
| centerInside    | CENTER_INSIDE           | 保持宽高比例，缩小图片使之位于视图中间（只缩小不放大）   |
| center          | CENTER                  | 保持图片原始尺寸，并使其位于视图中间                     |
| fitXY           | FIT_XY                  | 缩放图片使其正好填满视图（图片可能被拉伸变形）           |
| fitStart        | FIT_START               | 保持宽高比例，缩放图片使其位于视图上方或左侧             |
| fitEnd          | FIT_END                 | 保持宽高比例，缩放图片使其位于视图下方或右侧             |



## 第四章 常用组件

类似于 iOS 中的 viewController

界面跳转：一个activity跳转为另一个activity

### 4.1  Activity起停活动页面

#### 4.1.1  Activity 启动和停止

从当前页面跳转到新页面，跳转代码：

```xml
Intent intent = new Intent(源页面.this，目标页面.class)
startActivity(new Intent)
```

从当前页面回到上一个页面，相当于关闭当前页面，返回代码：

```xml
finish(); //结束当前的活动页面
```



二次理解：

点击按钮后跳转到了新的页面，

在新的页面中，浏览完毕想要返回上一页面，点击按钮后，触发finish();



#### 4.1.2  Activity的生命周期

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

  

#### 4.1.3  Activity的启动模式

![Android_Activity启动模式](/Users/liuyu/Desktop/Android-Study/Screenshots/Android_Activity启动模式.png)

可以在清单文件AndroidManifest.xml配置启动模式。

属性值填入standard表示采取标准模式。

```xml
<activity android:name=".JumpFirstActivity" android:launchMode="standard"/>
```

栈顶复用模式 singleTop

栈内复用模式 singleTask

全局唯一模式 singleInstance

动态设置启动模式

FLAG_ACTIVITY_NEW_TASK

FLAG_ACTIVITY_SINGLE_TOP

FLAG_ACTIVITY_CLEAR_TOP



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



#### 4.2.2  普通的活动数据交互

使用Bundle在Activity之间交换数据

（intent使用Bundle对象存放带传递的数据信息）

<a style="font-weight:bold;color:red">调用意图对象的putExtras()方法，取出调用getExtras()方法</a>

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

| 数据类型     | 读方法             | 写方法             |
| :----------- | :----------------- | :----------------- |
| 整型数       | getInt             | putInt             |
| 浮点数       | getFloat           | putFloat           |
| 双精度数     | getDouble          | putDouble          |
| 布尔值       | getBoolean         | putBoolean         |
| 字符串       | getString          | putString          |
| 字符串数组   | getStringArray     | putStringArray     |
| 字符串列表   | getStringArrayList | putStringArrayList |
| 可序列化结构 | getSerializable    | putSerializable    |

- 如果将bundle传递到下一个页面后还需要返回数据
  - 调用startActivityForResult()方法

```java
@Override
public void onClick(View v) {
  // 新建 bundle
  Bundle bundle = new Bundle();
  
  // 设置bundle 携带信息
  bundle.putString("msg","带着bundle跳转");
  
  // 新建意图
  Intent intent = new Intent(StartActForResultActivity.this,StartActSendResultActivity.class);
  intent.putExtras(bundle);
  startActivityForResult(intent,0);
 }
```

新页面的java文件接收，在finish()跳回之前：

```java
// 配置Acitivity的resultCode，携带intent返回
setResult(Activity.RESULT_OK,intent);
```

原页面的java文件中，重写onActivityResult方法：

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent intent) {
  super.onActivityResult(requestCode, resultCode, intent);
  if (requestCode == 0 && resultCode == RESULT_OK && intent != null){
    Bundle backMsg = intent.getExtras();
    String msg = backMsg.getString("msg");

    tv_desc.setText("bundle返回的值为：");
    tv_bundleMsg.setText(msg);
  }
}
```



#### 4.2.3  改进后的活动数据交互

startActivityForResult方法现在已经被标记为废弃了。

官网建议使用 registerForActivityResult() 方法。

- 先声明一个活动结果启动器对象 ActivityResultLauncher

```java
private ActivityResultLauncher mLauncher;
```

- 调用registerForActivityResult方法注册一个善后工作的活动结果启动器

```java
mLauncher = registerForActivityResult(
  // 第一个参数
  new ActivityResultContracts.StartActivityForResult(),
  // 第二个参数填入 onActivityResult 要做的事情
  result -> {
    if (result.getResultCode() == RESULT_OK && result.getData() != null){
      Bundle backMsg = result.getData().getExtras();
      String backKeyValue = backMsg.getString("msg");

      // 然后就可以根据findViewById的结果
      // 使用setText等方法进行赋值
    }
  }
);
```



### 4.3 收发应用广播

#### 4.3.1 收发标准广播

#### 4.3.2 收发有序广播

#### 4.3.3 收发静态广播

#### 4.3.4 定时管理器 AlarmManager



### 4.4 操作后台服务

#### 4.4.1 服务的启动和停止

Service是android四大组件之一。







#### 4.4.2 服务的绑定与解绑



#### 4.4.3 活动与服务之间的交互



## 第五章 中级控件

### 5.1 图形定制

#### 5.1.1 图形Drawable

Android把所有能显示的图形都抽象为Drawable类（可绘制的）。

| 属性值        | 说明     | 属性值           | 说明         |
| ------------- | -------- | ---------------- | ------------ |
| drawable-ldpi | 低分辨率 | drawable-xhdpi   | 加高分辨率   |
| drawable-mdpi | 中分辨率 | drawable-xxhdpi  | 超高分辨率   |
| drawable-hdpi | 高分辨率 | drawable-xxxhdpi | 超超高分辨率 |



#### 5.1.2 形状图形

#### 5.1.3 九宫格图片

#### 5.1.4 状态列表图形



### 5.2 选择按钮

#### 5.2.1 复选框CheckBox

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



#### 5.2.2 开关按钮 Switch

switch是开关按钮，新添加的xml属性包含了：

- textOn 设置右侧开启时的文本
- textOff 设置左侧开启时的文本
- track     设置开关轨道的背景
- thumb  设置开关标识的图标

```xml
<LinearLayout
	android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:orientation="horizontal">

  <TextView
		android:layout_width="0dp"
		android:layout_weight="1"
		android:layout_height="wrap_content"
		android:padding="5dp"
		android:layout_gravity="start"
		android:text="Switch开关"/>

	<Switch
		android:id="@+id/sw_status"
		android:layout_width="80dp"
		android:layout_height="30dp"
		android:padding="5dp"
		android:layout_gravity="end"/>

</LinearLayout>
```

java文件中：

```java
private TextView tv_result;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_switch);

        Switch sw_status = findViewById(R.id.sw_status);
        tv_result = findViewById(R.id.tv_result);

        sw_status.setOnCheckedChangeListener(this);

    }

    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        if (isChecked){
            tv_result.setText("switch is on checked for now");
        } else {
            tv_result.setText("switch has been closed");
        }
    }
```



#### 5.2.3 单选按钮 RadioButton

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



### 5.3 文本输入

#### 5.3.1 编辑框EditText

```xml
<EditText
            android:id="@+id/et_phone"
            android:layout_width="0dp"
            android:layout_weight="12"
            android:layout_height="wrap_content"
            android:inputType="phone"
            android:maxLength="11"
            android:hint="请输入11位手机号码"/>
```



#### 5.3.2 焦点变更监听器

```java
private EditText et_phone;
    private EditText et_password;
    private TextView tv_phoneConfirm;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_edit_focus);

        et_phone = findViewById(R.id.et_phone);
        et_password = findViewById(R.id.et_password);
        tv_phoneConfirm = findViewById(R.id.tv_phoneConfirm);

        et_password.setOnFocusChangeListener(this);
    }

    @Override
    public void onFocusChange(View v, boolean hasFocus) {
        if (hasFocus){
            String inputPhone = et_phone.getText().toString();
            if (inputPhone.length() == 11){
                tv_phoneConfirm.setText("✅");
            } else {
                AlertDialog.Builder builder = new 	     
                             AlertDialog.Builder(EditFocusActivity.this);
                builder.setMessage("输入手机号小于11位，请重新输入");
                builder.show();
            }
        }
    }
```



#### 5.3.3 文本变化监听器

- 调用编辑框对象的addTextChangedListener方法注册
- 文本监听器接口名称为 TextWatcher，该接口提供了3个监控方法：
  - 文本改变前触发：beforeTextChanged
  - 文本改变过程中触发：onTextChanged
  - 文本改变后触发：afterTextChanged

```java
et_tvChange = findViewById(R.id.et_tvChange);
et_tvChange.addTextChangedListener(new TextWatcher() {
  @Override
  public void beforeTextChanged(CharSequence s, int start, int count, int after) {}

  @Override
  public void onTextChanged(CharSequence s, int start, int before, int count) {}
  
  @Override
  public void afterTextChanged(Editable s) {
    if (s.length()==10){
      // 判断能否成功获取到文本框的变化
      Log.d("EditTextView", String.valueOf(s));
      
      // 关闭软键盘
      InputMethodManager imm = (InputMethodManager)getSystemService(Context.INPUT_METHOD_SERVICE);
      imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
    }
  }
});
```



### 5.4 对话框

#### 5.4.1 提醒对话框 AlertDialog

```java
AlertDialog.Builder builder = new AlertDialog.Builder(EditFocusActivity.this);
builder.setMessage("输入手机号小于11位，请重新输入");
builder.show();
```



#### 5.4.2 日期对话框 DatePickerDialog

为了能选择日期和时间，Android提供了 **DatePicker** 和 **TimePicker** 组件。



#### 5.4.3 时间对话框 TimePickerDialog



#### 5.4.4 Toast

```java
Toast.makeText(this,"请输入正确位数手机号码",Toast.LENGTH_SHORT).show();
```



## 第六章 数据存储

### 6.1 键值对

#### 6.1.1 共享参数的用法



#### 6.1.2 实现记住密码功能

#### 6.1.3 更安全的数据仓库

### 6.2 数据库

#### 6.2.1 SQL语句的基本语法

#### 6.2.2 数据库管理器 SQLiteDatabase

#### 6.2.3 数据库帮助器 SQliteOpenHelper

#### 6.2.4 优化记住密码功能

### 6.3 存储卡

#### 6.3.1 私有存储空间与公共存储空间

#### 6.3.2 在存储卡上读写文件

#### 6.3.3 运行时动态申请权限

### 6.4 应用组件 Application

#### 6.4.1 Application的生命周期

#### 6.4.2 利用Application操作全局变量

#### 6.4.3 避免方法数过多的问题

#### 6.4.4 利用Room简化数据库操作

### 6.5 共享数据

#### 6.5.1 通过ContentProvider封装数据

- ContentProvider为App存取内部数据提供统一的外部接口，让不同应用之间得以共享数据

<img src="/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-06-13 14.58.31.png" alt="截屏2023-06-13 14.58.31" style="zoom:50%;" align="left"/>

例如app读取通讯录的信息

- Client App将用户的输入内容，通过ContentProvider <a style="color:red;font-weight:bold">跨进程通信</a>传递给 Server App。



#### 6.5.2 通过ContentResolver访问数据

#### 6.5.3 通过ContentResolver读写数据

#### 6.5.4 通过ContentObserver监听短信



## 第七章 高级控件

### 7.1 下拉框

#### 7.1.1 下拉框控件 Spinner

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

#### 7.1.2 数组适配器 ArrayAdapter

- 在root XML文件中添加<Spinner>
- 新建item.xml文件，只添加TextView
- 不需要新建一个Adapter
- 在root Java文件中，新建一个ArrayAdapter，参数包括
  - this
  - R.layout.item指向新建只包含TextView的xml布局文件
  - arrayList，包含了指定数据类型值的List

```java
public class a2ArrayAdapterActivity extends AppCompatActivity {

    List<GoodsInfo> mGoodList = new ArrayList<>();

    private Spinner spinner;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_a2_array_adapter);

        mGoodList = GoodsInfo.getDefaultList();

        ArrayList<String> arrayList = new ArrayList<>();
        arrayList.add("optionA");
        arrayList.add("optionB");
        arrayList.add("optionC");
        arrayList.add("optionD");
        arrayList.add("optionE");
        arrayList.add("optionF");

        ArrayAdapter<String> adapter = new ArrayAdapter<>(this,R.layout.item,arrayList);
        spinner = findViewById(R.id.spinner);
        spinner.setAdapter(adapter);
    }
}
```



#### 7.1.3 简单适配器 SimpleAdapter

- 在xml布局文件中添加spinner

  - ```xml
    <Spinner
      android:id="@+id/spr_withImg"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"/>
    ```

- 新建xml布局文件，使用LinearLayout内含ImageView以及TextView

  - ```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:orientation="horizontal">
    
        <ImageView
            android:id="@+id/smp_apt_img"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="180dp"
            android:src="@drawable/ic_launcher_background"/>
    
        <TextView
            android:id="@+id/smp_apt_tv"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="180dp"
            android:text="this is TextView space"/>
    
    </LinearLayout>
    ```

- 新建 姓名ArrayList 和 路径ArrayList

  - ```xml
    for (int i = 0; i < nameList.size(); i++) {
         HashMap<String,Object> item = new HashMap<>();
         item.put("icon",iconList.get(i));
         item.put("name",nameList.get(i));
         list.add(item);
    }
    ```

- 还是不需要新建一个Adapter java class文件，

```java
SimpleAdapter adapter = new SimpleAdapter(
  this,
  list,
  R.layout.item_with_img,
  new String[]{"icon","name"},
  new int[]{R.id.smp_apt_img,R.id.smp_apt_tv}
);

adapter.setDropDownViewResource(R.layout.item_with_img);
Spinner spr_withImg = findViewById(R.id.spr_withImg);
spr_withImg.setPrompt("请选择款式");
spr_withImg.setAdapter(adapter);
spr_withImg.setSelection(0);
```



### 7.2 列表类视图

#### 7.2.1 基本适配器 BaseAdapter

- 数组适配器，适合只有文字
- 简单适配器，适合只有图像和文字
- 如果存在三个以上的控件，简单适配器会吃力，就需要基本适配器控制
- 要求在新的Adapter适配器java文件中进行控制。

**默认的spinner布局文件**

```xml
<Spinner
   android:id="@+id/spinner"
   android:layout_width="match_parent"
   android:layout_height="wrap_content"/>
```

**新建适配器中的布局文件**

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal"
    tools:context=".b1BaseAdapterActivity">

    <ImageView
        android:id="@+id/bAdapter_iv"
        android:layout_width="0dp"
        android:layout_weight="1"
        android:layout_height="150dp"
        android:scaleType="fitCenter"
        android:src="@drawable/ic_launcher_background"/>

    <LinearLayout
        android:layout_width="0dp"
        android:layout_weight="2"
        android:orientation="vertical"
        android:layout_height="150dp">

        <TextView
            android:id="@+id/bAdapter_name"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"/>

        <TextView
            android:id="@+id/bAdapter_desc"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"/>

    </LinearLayout>

</LinearLayout>
```

**新建适配器java代码**

```java
public class BaseAdapter extends android.widget.BaseAdapter {

    private Context mContext;
    private List<GoodsInfo> list_phone;

    public BaseAdapter(Context context, List<GoodsInfo> phoneList) {
        mContext = context;
        list_phone = phoneList;
    }

    @Override
    public int getCount() {
        return list_phone.size();
    }

    @Override
    public Object getItem(int position) {
        return list_phone.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder holder;

        // 转换视图为空
        if (convertView == null){
            // 创建一个新的视图拥有者
            holder = new ViewHolder();

            // 根据布局文件 item_with_img.xml 生成转换视图对象
            convertView = LayoutInflater.from(mContext).inflate(
                    R.layout.item_base_adapter,null);

            holder.bAdapter_iv = convertView.findViewById(R.id.bAdapter_iv);
            holder.bAdapter_name = convertView.findViewById(R.id.bAdapter_name);
            holder.bAdapter_desc = convertView.findViewById(R.id.bAdapter_desc);
            convertView.setTag(holder);
        } else {
            // 从转换视图中获取之前保存的视图持有者
            holder = (ViewHolder) convertView.getTag();
        }

        GoodsInfo phone = list_phone.get(position);
        holder.bAdapter_iv.setImageResource(phone.pic);
        holder.bAdapter_name.setText(phone.name);
        holder.bAdapter_desc.setText(phone.desc);
        holder.bAdapter_iv.requestFocus();
        return convertView;
    }

    public class ViewHolder{
        public ImageView bAdapter_iv;
        public TextView bAdapter_name;
        public TextView bAdapter_desc;
    }
}
```

**默认的java代码文件**

```java
public class b1BaseAdapterActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b1_base_adapter);

        ArrayList<GoodsInfo> list = GoodsInfo.getDefaultList();
        BaseAdapter baseAdapter = new BaseAdapter(this,list);

        Spinner spinner = findViewById(R.id.spinner);
        spinner.setAdapter(baseAdapter);
    }
}
```









#### 7.2.2 列表视图 ListView 

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



#### 7.2.3 网格视图 GridView



### 7.3 翻页类视图

#### 7.3.1 翻页视图 ViewPager

对于ViewPager，一个页面就是一项。

翻页视图使用页面变更监听器 onPageChangeListener，来监听页面的切换事件。

<mark>ViewPager三个常用方法的说明</mark>

- setAdapter 设置页面项的适配器
- setCurrentItem 设置当前页面，显示哪个页面
- addOnChangeListener 页面变更监听器，需实现3个借口方法
  - onPageScrollStateChanged：页面滑动状态变化时触发
  - onPageScrolled：页面滑动过程中触发
  - onPageSelected：选中页面时，即滑动结束后触发

XML文件中添加ViewPager，

```xml
<androidx.viewpager.widget.ViewPager
   android:id="@+id/vp_content"
   android:layout_width="match_parent"
   android:layout_height="370dp"/>
```



翻页视图包含了多个页面项，要借助翻页适配器展示每一个页面。

实现原理与基本适配器类似，从PagerAdapter派生的翻页适配器，实现方法：

- 构造方法：指定适配器处理数据集合
- getCount：获取页面项个数
- isViewFromObject：判断当前视图是否来自指定对象，返回view == object
- instantiateItem：实例话指定位置的页面，添加到容器
- destroyItem：从容器销毁指定位置的页面
- getPageTitle：获取指定页面的标题文本，搭配翻页标签栏才实现该方法

```java
// 声明一个视图列表
private final List<ImageView> mViewList = new ArrayList<>();

// 声明一个商品信息列表
private List<GoodsInfo> mGoodsList;

// 图像翻页适配器的构造方法，传入上下文与商品信息列表
public ImagePagerAdapter(Context context, List<GoodsInfo> goodsList){
  mGoodsList = goodsList;
  
  // 给每个商品分配一个专用的图像视图
  for (int i = 0; i < mGoodsList.size(); i++) {
    // 创建一个图像视图对象
    ImageView view = new ImageView(context);
    
    view.setLayoutParams(
      new ViewGroup.LayoutParams(
        ViewGroup.LayoutParams.MATCH_PARENT,
        ViewGroup.LayoutParams.WRAP_CONTENT)
    );
    view.setImageResource(mGoodsList.get(i).pic);
    
    // 把该商品的图像视图添加到视图列表
    mViewList.add(view);
  }
}

// 获取页面项的个数
@Override
public int getCount() {
  return mViewList.size();
}

// 判断当前视图是否来自指定对象
@Override
public boolean isViewFromObject(@NonNull View view, @NonNull Object object) {
  return view == object;
}

@Override
public Object instantiateItem(@NonNull ViewGroup container, int position) {
  container.addView(mViewList.get(position));
  return mViewList.get(position);
}

@Override
public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) {
  container.removeView(mViewList.get(position));
}

@Override
public CharSequence getPageTitle(int position) {
  return super.getPageTitle(position);
}
```



#### 7.3.2 翻页标签栏 PagerTabStrip

Android提供了与ViewPager配套翻页标签栏 PagerTabStrip

类似选项卡效果，文本下横线，点击选项卡可切换对应页面。

```xml
// 使用方法
// 在xml页面布局文件 ViewPager节点中添加
<androidx.viewpager.widget.ViewPager
   android:id="@+id/vp_content"
   android:layout_width="match_parent"
   android:layout_height="370dp">

   <androidx.viewpager.widget.PagerTabStrip
      android:id="@+id/pts_tab"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"/>

</androidx.viewpager.widget.ViewPager>
```

翻页适配器中重写getPageTitle方法

```java
@Override
public CharSequence getPageTitle(int position) {
  return mGoodsList.get(position).name;
}
```



#### 7.3.3 简单的启动引导页



### 7.4 碎片 Fragment

**fragment** 与 **activity** 非常相似，

多个 **fragment** 可以在一个单独的 **activity** 中建立多个UI面板，

也可以在多个 **activity** 中重用 **fragment**。

- 创建 Fragment

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

- Fragment产生

![截屏2023-06-15 15.14.44](/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-06-15 15.14.44.png)

- 什么是Fragment

具备生命周期，so可在Acitivity中使用多个Fragment

- 必须委托在Acitivity中才能运行
  - 当一个Activity暂停时，其中所有的Fragment都会暂停。
  - Activity运行时，Fragment可独立当作子Activity使用。

#### 7.4.1 碎片的静态注册

在fragment中创建element，在主页面中：

```xml
<androidx.fragment.app.FragmentContainerView
  android:id="@+id/frg_first"                                            			   android:name="com.example.fragment.BlankFragment1"
  android:layout_width="match_parent"
  android:layout_height="match_parent"/>
```

- 必须要为fragment创建id
- android:name对应创建的fragment的xml文件

#### 7.4.2  碎片的动态注册

- 绑定按钮点击事件

```java
btn_frgReplace.setOnClickListener(this);
```

- 按钮点击事件代码，调用新方法

```java
replaceFragment(new BlankFragment1());
```

- 设置replaceFragment方法

```java
private void replaceFragment(Fragment fragment) {
  // Fragment 管理类
  FragmentManager fragmentManager = getSupportFragmentManager();

  // FragmentTransaction 事务管理类
  // fragment 替换动作由 transaction 来完成
  FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
  fragmentTransaction.replace(R.id.frameLayout,fragment);

  // 提交replace事件
  fragmentTransaction.commit();
}
```

- 配置fragment管理栈

```java
// 实现点击返回回到上一个fragment，非桌面
// fragment 添加到管理栈
fragmentTransaction.addToBackStack(null);
```



#### 7.4.3  改进的启动引导页



#### 7.4.4 Fragment动态添加与管理

- Activity发送信息给Fragment

两个独立的类相互之间进行通信

原生方案：Bundle

bundle无法存放一个JavaBean，可以使用parceLable实现（安卓序列化）。

- 代码实现

```java
// new 一个Bundle进行通信
Bundle bundle = new Bundle();
bundle.putString("msg","msg");

// 实例化，来传递bundle
BlankFragment1 blankFragment1 = new BlankFragment1();
blankFragment1.setArguments(bundle);
```

- Fragment动态添加和管理总结

步骤：

1. 创建一个待处理的fragment
2. 获取FragmentManagement，一般都是通过getSupportFragmentManager()
3. 开启一个事务transaction，一般调用fragmentManager的beginTransaction()
4. 使用transaction进行fragment的替换
5. 提交事务



#### 7.4.5 Fragment与Activity通信接口

Java语言中类与类自己通信常用方案：接口



#### 7.4.6 Fragment生命周期

<img src="/Users/liuyu/Library/Application Support/typora-user-images/截屏2023-06-16 10.18.58.png" alt="截屏2023-06-16 10.18.58" style="zoom:50%;" align="left"/>



## 第八章 自定义控件

### 8.1 视图的构建过程

#### 8.1.1 视图的构造方法



#### 8.1.2 视图的测量方法



#### 8.1.3 视图的绘制方法



### 8.2 改造已有控件

#### 8.2.1 自定义月份选择器

#### 8.2.2 给翻页标签栏添加新属性

#### 8.2.3 不滚动的列表视图

### 8.3 推送消息通知

#### 8.3.1 通知推送Notification

#### 8.3.2 通知渠道NotificationChannel

#### 8.3.3 推送服务到前台

#### 8.3.4 仿微信的悬浮通知

### 8.4 通过持续绘制实现简单动画

#### 8.4.1 Handler的延迟机制

#### 8.4.2 重新绘制视图界面

#### 8.4.3 自定义饼图动画







## 第九章 组合控件

### 9.1 底部标签栏

#### 9.1.1 利用BottomNavigationView实现底部标签栏



#### 9.1.2 自定义标签按钮



#### 9.1.3 结合RadioGroup 和 ViewPager 自定义底部标签栏



### 9.2 顶部导航栏

#### 9.2.1 工具栏Toolbar



#### 9.2.2 溢出菜单 OverflowMenu



#### 9.2.3 标签布局 TabLayout



### 9.3 增强性列表

#### 9.3.1 循环视图 RecyclerView

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



RelativeLayout 与 LinearLayout

- 在LinearLayout中，只能做到一个个按顺序排列；
- 在RelativeLayout中，可以按照自己设置的align或者padding进行随意的排版。

ItemDecoration

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



在Adapter里获取屏幕的宽度 & 单一item的宽度

```JAVA
WindowManager wm = (WindowManager) parent.getContext().getSystemService(Context.WINDOW_SERVICE);
Display display = wm.getDefaultDisplay();
int width = display.getWidth();              // 获取 整个屏幕的宽度
int vWidth = view.getLayoutParams().width; 
```

#### 9.3.2 布局管理器 LayoutManager

#### 9.3.3 动态更新循环视图

### 9.4 升级版翻页

#### 9.4.1 下拉刷新布局 SwipeRefreshLayout

#### 9.4.2 第二代翻页视图 ViewPager2

#### 9.4.3 给ViewPager2集成标签布局



## 第十章 打造安装包

### 10.1 应用打包

#### 10.1.1 导出APK安装包

#### 10.1.2 制作App图标

#### 10.1.3 给APK瘦身

### 10.2 规范处理

#### 10.2.1 版本设置

#### 10.2.2 发布模式

#### 10.2.3 多渠道打包

### 10.3 安全加固

# Context

理解Context

- 可以理解为“上下文”：贯穿整个应用；
- 也可以理解为“运行环境”：它提供了一个应用运行所需要的信息，资源，系统服务等；
- 同样可以理解为“场景”：用户操作 和 系统交互，这一过程就是一个场景，比如Activity之前的切换，服务的启动等都少不了Context。

<img src="/Users/liuyu/Desktop/Android-Study/Screenshots/context体系结构.png" alt="context体系结构" style="zoom: 67%;" align="left"/>















