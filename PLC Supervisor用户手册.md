# PLC Supervisor App用户手册
PLC Supervisor App（以下简称PLC Supervisor）为用户提供了便捷的数据采集、数据处理和数据上云功能，支持Snap7、ModbusRTU等多种工业协议解析。
本手册以采集PLC的数据并上传至Thingboard云平台为例说明如何通过PLC Supervisor App实现PLC数据采集和数据上云。以下将InGateway500简称为“IG500”；InGateway900简称为“IG900”。
## 1.准备硬件设备及其数据采集环境
### 1.1 硬件接线
#### 1.1.1 以太网数据采集接线
- IG900以太网接线  
  
  接通IG900的电源并按照拓扑使用以太网线连接IG900和PLC。  <br/>
![](images/2020-02-21-14-52-40.png)  

- IG500以太网接线  
  
  接通IG500的电源并按照拓扑使用以太网线连接IG500和PLC。  <br/>
![](images/2020-02-21-14-53-05.png)
#### 1.1.2 串口接线
- IG900串口接线  

  接通IG900的电源并按照拓扑连接IG900和PLC。  <br/>
![](images/2020-02-21-16-56-55.png)  

  IG900正上方的端子接线说明如下图：  

  ![](images/2020-01-09-18-47-30.png)  

- IG500串口接线  

  接通IG500的电源并按照拓扑连接IG500和PLC。  <br/>
![](images/2020-02-21-17-29-54.png)  

  IG500正下方的端子接线说明如下图：  <br/>
  ![](images/2020-02-21-17-30-20.png)
### 1.2 设置LAN网络参数：在局域网访问PLC
- IG900的GE 0/2口的默认IP地址为192.168.2.1。为了使IG900能够通过GE 0/2口访问以太网PLC，需要设置GE 0/2口与PLC处于同一网段，设置方法请参考[在局域网访问IG500](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#lan-ig501)。
- IG500的FE 0/1口的默认IP地址为192.168.1.1。为了使IG500能够通过FE 0/1口访问以太网PLC，需要设置FE 0/1口与PLC处于同一网段，设置方法请参考[在局域网访问IG900](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#lan-ig902)。

### 1.3 设置WAN网络参数：传输数据至MQTT服务器
- 设置IG500 WAN网络参数，请参考[IG500连接Internet](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#wan-internet)。
- 设置IG900 WAN网络参数，请参考[IG900连接Internet](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#wan-internet)。

### 1.4 更新InGateway设备软件版本
如需获取InGateway产品最新软件版本及其功能特性信息，请联系客服。如需更新软件版本，请参考如下链接：
- [更新IG500软件版本](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#id1)
- [更新IG900软件版本](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#id1)

## 2.配置PLC Supervisor App
### 2.1 安装并运行PLC Supervisor
- IG500如何安装并运行Python App请参考[IG500安装和运行Python App](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#python-app)，PLC Supervisor正常运行后如下图所示：  
  

- IG900如何安装并运行Python App请参考[IG900安装和运行Python App](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#python-app)，PLC Supervisor正常运行后如下图所示： 
  ![](images/2020-02-21-17-57-15.png)

### 2.2 配置PLC Supervisor
#### 2.2.1 添加PLC设备
- 添加Snap7通讯的PLC设备  
  
  点击“添加PLC”按钮，在添加设备页面配置PLC的通讯参数。（机架号和槽号除S7-200 Smart需要配置为0，1；其余类型的S7系列PLC默认使用0，0即可）
  
- 添加ModbusTCP通讯的PLC设备
- 添加ModbusRTU通讯的PLC设备
#### 2.2.2 添加变量
- 添加Snap7变量
- 添加Modbus变量

#### 2.2.3 配置变量分组

#### 2.2.3 监控PLC数据

## 3.监控PLC数据
### 3.1 本地监控PLC数据
### 3.2 在MQTT服务器上监控PLC数据
#### 3.2.1 配置云服务

#### 3.2.2 配置Thingsboard
Thingsboard的配置方法可以参考[Thingsboard入门手册](https://thingsboard.io/docs/getting-started-guides/helloworld/)，也可以参考以下流程：  

- 步骤1：添加设备和资产  
  
  访问https://demo.thingsboard.io/login，输入登录账号和密码。如果未注册过账号则需要先注册账号后再登录。
![](images/2020-02-24-17-30-44.png)  <br/>
登录后，进入属性页面修改语言为简体中文
![](images/2020-02-26-09-50-27.png)

  - 添加一个资产
  ![](images/2020-02-26-10-27-13.png)
![](images/2020-02-26-10-27-40.png)
添加成功后如下图所示：
![](images/2020-02-26-09-52-39.png)

  - 添加一个设备
![](images/2020-02-26-09-54-14.png)
![](images/2020-02-26-09-54-27.png)

  建立资产与设备的关联
![](images/2020-02-26-09-56-01.png)
添加完成后如下图所示
![](images/2020-02-26-09-56-57.png)

- 步骤2：传输PLC数据到设备  
  
  资产和设备配置完成后，复制已添加设备的访问令牌并粘贴至网关的云服务页面的用户名参数中以将数据传输至Thingsboard中的Snap7设备。
![](images/2020-02-26-09-58-18.png)
随后可在设备的最新遥测中查看已上传的数据。
![](images/2020-02-26-10-38-50.png)

- 步骤3：配置可视化仪表板  
  - 添加仪表板  
  
    点击添加仪表板，选择创建新的仪表板
![](images/2020-02-26-10-40-22.png)
![](images/2020-02-26-10-40-58.png)
添加完成后单击配置仪表板
![](images/2020-02-26-10-00-23.png)
点击进入编辑模式
![](images/2020-02-26-10-00-45.png)
为仪表板添加实体别名
![](images/2020-02-26-10-01-13.png)
在添加别名页面按下图配置：
![](images/2020-02-26-10-02-41.png)
配置完成后保存配置。
![](images/2020-02-26-10-03-00.png)
保存后，为仪表板中添加部件。
![](images/2020-02-26-10-03-23.png)

  - 添加趋势图  
  
  在部件中选择Charts并点击Timeseries-Flot。
![](images/2020-02-26-10-03-51.png)
在图表的数据页面为趋势图添加展示数据。
![](images/2020-02-26-10-14-28.png)
![](images/2020-02-26-10-15-50.png)
添加完成后如下图所示：
![](images/2020-02-26-10-18-00.png)

  - 添加开关  
  
  点击添加，选择创建新部件以添加一个控制开关。
![](images/2020-02-26-10-21-47.png)
在部件中选择Control widgets并点击Switch control。
![](images/2020-02-26-10-20-10.png)
随后选择目标设备。
![](images/2020-02-26-10-20-36.png)

配置完成后调整部件的大小和布局并保存。
![](images/2020-02-26-10-22-40.png)
随后可以通过开关下发控制命令以及通过趋势图查看数据趋势。
![](images/2020-02-26-10-22-59.png)


# 自定义数据格式
## 发布
用户自行配置发布名称，主题，mqtt_qos、变量来源以及组包逻辑。被选中的分组中的所有变量将按照分组的上报间隔定期组包上传至云平台。  

输出日志使用from common.Logger import logger（common在哪里？是我们设备自带的依赖库？）
发布中包含的参数：
- data：PLC Supervisor采集数据后发送至MQTT代理
- global_argv：全局变量的key value，日志等级（log_level）,序列号（gateway_sn）
- mqtt_publish：自定义什么时候向云端推送什么数据
- save_db：存储历史数据

## 订阅
用户自行配置订阅名称，主题，mqtt_qos、变量来源以及解析数据报文和组包逻辑。接收平台下发的数据并解析处理后发给指定的程序。  

输出日志使用from common.Logger import logger

订阅中包含的参数：
- topic：平台下发过来的topic
- payload：平台下发过来的数据
- send_message_to_partner：
  - message：发送给PLC Supervisor的数据包
  - partner：
  - operate：默认为"write_plc_values"，即写入数据到PLC
  - ack_callback：
  - timeout：