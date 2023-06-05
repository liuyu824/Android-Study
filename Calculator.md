# 23.5.16 计算器逻辑

创建 LinkedList<Integer> numberList 填充每一个输入的数字

创建 LinkedList<String> operatorList 填充每一个输入的运算符



对 ➕➖✖️➗，使用同一种if语句，

numberList.length() - operatorList() = 1 才代表了正常的表达式。

# 23.5.24 完善计算器逻辑 & BUG

#### 1. java代码中给按钮设置高度

```java
// 原写法
Button btn_ac = findViewById(R.id.btn_ac);
btn_ac.setHeight(width);

// 现写法
((Button)findViewById(R.id.btn_ac)).setHeight(width);
```

**考虑：**创建 **btn_ac** 对象，再进行 **setHeight()** 方法，但是除此之外整体代码没有任何使用。是不是占用内存了？

**改变：**不新建对象，直接进行设置。（需要转换为Button，要不默认为View）



#### 2. 数字太长没有分隔符，不方便阅读

想法：每三位数之间，以 [ , ]分开，例如：999,999,999

- 存在小数相同，小数为不需要以 [ , ]分开，例如：999,9.77777

解决办法：

- 设置一个新的全局变量 bitPushNumber，用于记录整数位有几位数字了

- 如果存在小数点，不进行操作；

- 如果不存在小数点，每点击一次，**integerBit+1**；

- 当 **integerBit == 3** 时，showText加入 **","**，并将 integerBit 重新设置为0；

  

#### 3. java代码中 那句巨长的类型转换

```java
// Math.round()方法为四舍五入
// 更改前
pushNumber = (double) Integer.parseInt((String.valueOf(Math.round(pushNumber))));
// 更改后
pushNumber = (double) Math.round(pushNumber);
```

更改前存在原因：最开始没有考虑小数时，pushNumber为Int类型，需要先转换为String，再转换为Int。

考虑小数运算后，直接点了提示，没自己改。



#### 4. 设置每一次数值不能超过9位数（包括小数点后）

新建一个integer类型的对象，用于捕捉点击数字按钮的次数。

在default判断中（即点击数字按钮时），对全局添加一个if语句，

如果integerBit<=8(因为从0开始)，那么就不进行任何操作。



#### 5. 操作乘除运算符，使用了remove()，容易造成混乱

**extra: **偶然发现了加减同样的问题，

- 倒序运算，如果 A/B×C，会先运算 B×C，变成 A/(B×C)
- 与原意不符

解决办法：采用正序运算，不使用remove()，

- 运算过的数字赋值0，运算过的运算符赋值 "+"
- 为什么没有采用新建两个空列表，每一次运算往里放值
  - 如果连续乘除，不方便运算。

**不可以！**因为当有两个乘除想连时，就会出现乘0除0的情况。

**新思路2.0：**逆序先算除，再逆序算乘，再算加减。

**不可以！**因为就算先算除，还是会出现两个连除的情况，逆序有问题。

**新思路3.0：**先算除，算完后把除号改为乘号，除数改为1。再算乘，加减。

还是没想出来如果不用remove该怎么做。



#### 6. 锁定竖屏

 ```xml
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
 ```



#### 7. 百分号显示在屏幕上

```xml
case "%":
	if (pushNumber != null){
		pushNumber = pushNumber/100;
    pushShowText += "%";
    calculateTV.setText(showText+pushShowText);
    break;
}
```



# 23.5.25 完善计算器逻辑 & BUG

#### 1. 写删除按钮的逻辑

思路：

- 当pushNumber为空时，不进行任何操作，防止崩
- 当pushNumber为整数时：
  - 当pushNumber为长度大于1的整数时（非个位数）：使用 StringBuffer 的 deleteCharAt() 方法删除最后一位字符
  - 当pushNumber为长度等于1的整数时（为个位数）：使pushNumber == 0.0（若赋值为null，会引发后续运算崩）；
- 当pushNumber非整数时：
  - 使用相似的StringBuffer方法，删除最后一位字符
  - 当只剩最后一位字符了，例如【88.7】删除后为【88.】
    - 判断方式为 pushNumber == Math.round(pushNumber)了
    - 直接连【.】一并删除，将整数赋值给pushNumber。
    - 这样的话，后续再进行删除时，将直接按照一个整数的标准进行删除。



#### 2. 点击完等号后，还能继续对结果进行加减乘除运算

- 将resultNumber赋值给pushNumber。
- 测试时候出现的问题：
  - 普通输入已经限制了输入值不能大于9位数；
  - 这里也需要限制，因为这种情况没有包含在那种条件中。
  - 想尝试也用stringBuffer的办法移除多于9位的数字
    - 没解决：过大的运算，例如【999,999,999 × 999,999,999】。
    - 最后显示 9.99999998E17。这种情况如果截了，结果就变了，变成小数了。



#### 3. resultTV上的结果也按照三位逗号分割

完成了乘除为整数的resultTV



# 23.5.26 完善计算器逻辑 & BUG

#### 1. resultTV上的结果最多只显示9位数字（包括小数点后）



#### 2. 完善点击+/-号后，calculateTV显示问题

原始：比较直接，直接对showText添加pushNumber，会造成定义的三位一逗号无法使用。

现在：对保留了三位一逗号的 pushShowtext对象进行修改。showText和pushNumber分开。

问题：之前没有考虑到，前面有负号时，也会把负号作为一个字符，导致【-,222,222】



#### 3. 完善逗号也被当作字符问题

- 判断addNum的double值，即pushNumber是否小于0；
- 如果小于0，即为负数，数字前有负号；
- 后续使用insert方法添加逗号，考虑的所在位置+1。



#### 4. 点击两次正负号，数字前面有两个负号，应删除负号显示正数

```java
// 尝试直接对pushShowText进行更改
// 添加判断语句
// 如果显示负数，删除负号，而非2个负号
if (pushNumber > 0){
	StringBuilder sb_pushShowText = new StringBuilder(pushShowText);
	sb_pushShowText.deleteCharAt(0);
	pushShowText = String.valueOf(sb_pushShowText);
} else if (pushNumber < 0){
	pushShowText = "-"+pushShowText;
}
```



#### 5. 测试里还存在的问题

- (已改) 点击完%，还能点击数字
- (已改) 回退后，没有相应的减少integerBit
- 点击完%后，再点击回退键有崩溃的情况
- 删除后显示0
- logd的TAG设置成固定的

