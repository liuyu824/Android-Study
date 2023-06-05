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



##### 公共方法dip2px

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



#### 3.3.4 ScrollView

滚动视图有两种：

**ScrollView，垂直方向**的滚动视图：

- layout_width属性设置为 match_parent
- layout_height属性设置为 wrap_content

**HorizontalScrollView，水平方向**的滚动视图：

- layout_width属性设置为 wrap_content
- layout_height属性设置为 match_parent 



### 3.4 按钮触控

#### 3.4.1 按钮控件Button

```xml
<Button
	//属性列表/>
```



#### 3.4.2 点击事件和长按事件





#### 3.4.3 禁用与恢复按钮



### 3.5 图像显示

#### 3.5.1 图像视图 ImageView



#### 3.5.2 图像按钮 ImageButton



#### 3.5.3 同时展示文本与图像



