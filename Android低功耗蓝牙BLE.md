## Android低功耗蓝牙 BLE

bluetooth low energy

17 物联网

17.1 短距离通信

17.1.1 WI-FI管理器

两种上网方式：数据连接 && WI-FI

连接管理器 ConnectivityManager 只能判断能否上网，不能获取 Wi-Fi 连接详细信息；

使用WI-FI连接时，需要 无线网络管理器WifiManager 获取具体信息。

WifiManager对象 从系统服务 Context.WIFI_SERVICE获取。

- isWifiEnabled：判断wlan功能是否开启
- setWifiEnabled：开启或关闭wlan功能（从Android11开始，该方法已经失效）
- getWifiState：获取当前的wifi连接状态

| WifiManager类的连接状态 | 说明          |
| ----------------------- | ------------- |
| WIFI_STATE_DISABLED     | 已断开Wi-Fi   |
| WIFI_STATE_DISABLING    | 正在断开Wi-Fi |
| WIFI_STATE_ENABLED      | 已连上Wi-Fi   |
| WIFI_STATE_ENABLING     | 正在连接Wi-Fi |
| WIFI_STATE_UNKOWN       | 连接状态未知  |

- getConnectionInfo：获取当前Wi-Fi的连接信息
  - 返回一个WifiInfo对象，通过该对象各个方法获取更具体Wi-Fi设备信息。
  - getSSID：Wi-Fi路由器MAC
  - getRssi：Wi-Fi信号强度
  - getLinkSpeed：连接速率
  - getNetworkId：Wi-Fi的网络编号
  - getIpAddress：手机的IP地址，整数，需要自己转换为常见的IPv4地址
  - getMacAddress：手机的MAC地址
- startScan：开始扫描周围的Wi-Fi信息
- getScanResults：获取Wi-Fi的扫描结果
- calculateSignalLevel：根据信号强度计算信号等级
- getConfiguredNetworks：获取已配置的网络信息
- addNetwork：添加指定的Wi-Fi连接
- enableNetwork：启用指定的Wi-Fi连接
- disableNetwork：禁用指定的Wi-Fi连接
- disconnect：断开当前的Wi-Fi连接

查看网络连接与室内定位需要申请相关权限，打开AndroidManifest.xml补充配置：

```java
<!--  室内Wi-Fi定位需要以下权限  -->
<!--  定位  -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<!--  Wi-Fi权限  -->
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>

<!--  获取网络状态  -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

<!--  需要RTT功能  -->
<uses-permission android:name="android.hardware.wifi.rtt"/>
```



