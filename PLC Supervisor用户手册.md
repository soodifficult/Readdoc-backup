# PLC Supervisor App用户手册
PLC Supervisor App（以下简称PLC Supervisor）为用户提供了便捷的数据采集、数据处理和数据上云功能，支持Snap7、ModbusRTU等多种工业协议解析。
本手册以采集PLC的数据并上传至Thingsboard云平台为例说明如何通过PLC Supervisor App实现PLC数据采集和数据上云。以下将InGateway500简称为“IG500”；InGateway900简称为“IG900”。

## 概览
使用过程中，您需要准备以下项：  
- 边缘计算网关IG500/IG900  
- PLC设备  
- 网线/串口线  
- *更新软件版本所需的固件、SDK和App  
- *Thingsboad演示账号  

整体流程如下图所示：  
- [环境准备](#准备硬件设备及其数据采集环境)
- [数据采集配置（配置PLC Supervisor App）](#配置Plc_Supervisor_App)
- [监控PLC数据](#监控PLC数据)  
- [附录](#附录)

![](images/2020-03-12-22-26-27.png)

<a id="准备硬件设备及其数据采集环境"> </a>  

## 1.准备硬件设备及其数据采集环境
- [硬件接线](#硬件接线)
- [设置LAN网络参数](#设置LAN网络参数)
- [设置WAN网络参数](#设置WAN网络参数)
- [更新软件版本](#更新InGateway设备软件版本)  

<a id="硬件接线"> </a>  

### 1.1 硬件接线
#### 1.1.1 以太网接线
- IG900以太网接线  
  
  接通IG900的电源并按照拓扑使用以太网线连接IG900和PLC。  <br/>
![](images/2020-03-12-14-02-22.png)  
 &nbsp;

- IG500以太网接线  
  
  接通IG500的电源并按照拓扑使用以太网线连接IG500和PLC。  <br/>
![](images/2020-03-12-14-03-03.png)
#### 1.1.2 串口接线
- IG900串口接线  

  接通IG900的电源并按照拓扑连接IG900和PLC。  <br/>
![](images/2020-03-12-14-03-36.png)  

  IG900正上方的端子接线说明如下图：  <br/>
  ![](images/2020-01-09-18-47-30.png)  

- IG500串口接线  

  接通IG500的电源并按照拓扑连接IG500和PLC。  <br/>
![](images/2020-03-12-14-04-05.png)  

  IG500正下方的端子接线说明如下图：  <br/>
  ![](images/2020-03-11-11-38-45.png)
 
<a id="设置LAN网络参数"> </a>  

### 1.2 设置LAN网络参数：在局域网访问PLC
- IG900的GE 0/2口的默认IP地址为`192.168.2.1`。为了使IG900能够通过GE 0/2口访问以太网PLC，需要设置GE 0/2口与PLC处于同一网段，设置方法请参考[在局域网访问IG900](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#lan-ig902)。
- IG500的FE 0/1口的默认IP地址为`192.168.1.1`。为了使IG500能够通过FE 0/1口访问以太网PLC，需要设置FE 0/1口与PLC处于同一网段，设置方法请参考[在局域网访问IG500](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#lan-ig501)。

<a id="设置WAN网络参数"> </a>  

### 1.3 设置WAN网络参数：传输数据至MQTT服务器
- 设置IG900 WAN网络参数，请参考[IG900连接Internet](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#wan-internet)。
- 设置IG500 WAN网络参数，请参考[IG500连接Internet](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#wan-internet)。

<a id="更新InGateway设备软件版本"> </a>  

### 1.4 更新InGateway设备软件版本
如需获取InGateway产品最新软件版本及其功能特性信息，请联系客服。如需更新软件版本，请参考如下链接：
- [更新IG900软件版本](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#id1)
- [更新IG500软件版本](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#id1)

<a id="配置Plc_Supervisor_App"> </a>  

## 2.配置PLC Supervisor App
- [安装并运行PLC Supervisor](#安装并运行PLC_Supervisor)
- [PLC Supervisor数据采集配置](#PLC_Supervisor数据采集配置)
  - [添加PLC设备](#添加PLC设备)
  - [添加变量](#添加变量)
  - [配置变量分组](#配置变量分组)

<a id="安装并运行PLC_Supervisor"> </a>  

### 2.1 安装并运行PLC Supervisor
- IG900如何安装并运行Python App请参考[IG900安装和运行Python App](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#python-app)，PLC Supervisor正常运行后如下图所示： 
  ![](images/2020-02-21-17-57-15.png)
 &nbsp;
- IG500如何安装并运行Python App请参考[IG500安装和运行Python App](https://ingateway-development-docs.readthedocs.io/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html#python-app)，PLC Supervisor正常运行后如下图所示：  
  ![](images/2020-02-21-17-57-15.png)  

<a id="PLC_Supervisor数据采集配置"> </a>  

### 2.2 PLC Supervisor数据采集配置
<a id="添加PLC设备"> </a>  

#### 2.2.1 添加PLC设备
- 添加S7通讯的PLC设备  
  
  点击“添加PLC”按钮，在添加设备页面选择PLC协议为“Snap7”并配置PLC的通讯参数。（除PLC为S7-200 Smart时机架号和槽号需要配置为0，1；其余类型的S7系列PLC默认使用0，0即可）<font color=#FF0000>注意：设备名称不能重复。</font>  

  ![](images/2020-02-27-14-18-01.png)  

  添加成功后如下图所示：  
![](images/2020-02-27-14-32-51.png)  
 &nbsp;
</br>

- 添加ModbusTCP通讯的PLC设备  
  
  点击“添加PLC”按钮，在添加设备页面选择PLC协议为“ModbusTCP”并配置PLC的通讯参数。（端口号和字节序默认为502和abcd；使用时需根据实际情况调整）<font color=#FF0000>注意：设备名称不能重复。</font>  

  ![](images/2020-03-06-15-02-16.png)  

  添加成功后如下图所示：  
  ![](images/2020-03-06-15-02-42.png)  
 &nbsp;
</br>

- 添加ModbusRTU通讯的PLC设备  
  
  点击“添加PLC”按钮，在添加设备页面选择PLC协议为“ModbusRTU”并配置PLC的通讯参数。<font color=#FF0000>注意：设备名称不能重复。</font>  

  ![](images/2020-02-27-14-19-59.png)  

  添加成功后如下图所示：
![](images/2020-03-06-15-03-41.png)  

  如需修改RS232/RS485串口的通讯参数，请在“边缘计算>>PLC Supervisor>>全局参数”页面修改。修改后所有串口设备的通讯参数将自动修改并按照修改后的通讯参数通讯。  
![](images/2020-02-27-14-26-04.png)

<a id="添加变量"> </a>  

#### 2.2.2 添加变量
- 添加Snap7变量  
  
  点击“添加变量”按钮，在弹出框中配置变量参数：
  - 变量名：变量名称<font color=#FF0000>（同一设备下变量名称不能重复）</font>    
  - 寄存器类型：变量寄存器类型，包括I/Q/M/DB四种类型  
  - DB索引：寄存器类型为DB时变量的DB号  
  - 地址：变量的寄存器地址  
  - 数据类型：变量数据类型，包括：  
    - BOOL：True或False  
    - BIT：0或1  
    - BYTE：8位无符号数据  
    - SINT：8位有符号数据  
    - WORD：16位无符号数据  
    - INT：16位有符号数据  
    - DWORD：32位无符号数据  
    - DINT：32位有符号数据  
    - FLOAT：32位浮点数  
    - STRING：8位字符串  
    - BCD ：16位BCD码  
  - 小数位：数据类型为FLOAT时变量小数点后的数据长度，最大6位  
  - 长度：数据类型为STRING时字符串长度，读取1个字符串的长度为1  
  - 位：数据类型为BOOL或BIT时变量的位偏移，可输入0~7中任一数字  
  - 读写权限：  
    - Read：只读，不可写  
    - Write：只写，不可读  
    - Read/Write：可读可写  
  - 采集模式：  
    - Realtime：按照所属分组的采集间隔采集变量并按照上报间隔上报数据  
    - Onchange：变量数值有变化时才采集变量并按照上报间隔上报数据  
  - 单位：变量单位  
  - 描述：变量描述  
  - 所属分组：变量所属的采集组  
   &nbsp;
   
  下图是添加一个地址为%I0.0的开关变量的例子：  </br>
  ![](images/2020-02-27-18-06-40.png)  

  下图是添加一个地址为%IB1的字节变量的例子：  </br>
  ![](images/2020-02-27-18-08-22.png)  

  下图是添加一个地址为%IW3的字变量的例子：  </br>
  ![](images/2020-02-28-16-26-04.png)  

  下图是添加一个地址为%ID4的双字变量的例子：  </br>
  ![](images/2020-02-28-16-27-49.png)  

  下图是添加一个地址为%DB6.DBD18的浮点数变量的例子：  </br>
  ![](images/2020-02-28-16-25-21.png)  
 &nbsp;
 </br>

- 添加Modbus变量  
  
  点击“添加变量”按钮，在添加变量弹出框中配置PLC变量参数：
  - 变量名：变量名称<font color=#FF0000>（同一设备下变量名称不能重复）</font>    
  - 地址：变量的寄存器地址  
  - 数据类型：变量数据类型，包括：  
    - BOOL：True或False  
    - BIT：0或1  
    - WORD：16位无符号数据  
    - INT：16位有符号数据  
    - DWORD：32位无符号数据  
    - DINT：32位有符号数据  
    - FLOAT：32位浮点数  
    - STRING：8位字符串   
  - 小数位：数据类型为FLOAT时变量小数点后的数据长度，最大6位  
  - 长度：数据类型为STRING时字符串长度  
  - 位：地址为`30001~40000`,`310001~365535`，`40001~50000`，`410001~465535`且数据类型为BOOL或BIT时变量的位偏移，可输入0~15中任一数字  
  - 读写权限：  
    - Read：只读，不可写  
    - Write：只写，不可读  
    - Read/Write：可读可写  
  - 采集模式：  
    - Realtime：按照固定采集间隔采集变量并按照上报间隔上报数据  
    - Onchange：变量数值变化后才采集并按照上报间隔上报数据  
  - 单位：变量单位  
  - 描述：变量描述  
  - 所属分组：变量所属的采集组  
   &nbsp;

  下图是添加一个地址为00001的线圈变量的例子：  </br>
  ![](images/2020-03-06-15-33-59.png)  

  下图是添加一个地址为10001的开关变量的例子：  </br>
![](images/2020-03-06-15-35-15.png)  

  下图是添加一个地址为30001的整数变量的例子：  </br>
  ![](images/2020-03-06-15-36-37.png)  

  下图是添加一个地址为40001的浮点数变量的例子：  </br>
  ![](images/2020-03-06-15-37-11.png)

<a id="配置变量分组"> </a>  

#### 2.2.3 配置变量分组
如需为变量配置不同的采集间隔和上报间隔或需要按照不同的MQTT主题上报相应的变量数据时，可在“边缘计算>>PLC Supervisor>>分组”页面添加新分组。  
![](images/2020-02-27-17-03-51.png)

添加分组后，添加变量时可以选择将变量关联到该分组或者在变量列表中选择需要关联的变量添加到指定分组中，分组中的变量会按照分组的采集间隔和上报间隔采集并上报数据。
![](images/2020-02-27-17-05-33.png)  

![](images/2020-02-27-17-06-20.png)

<a id="监控PLC数据"> </a>  

## 3.监控PLC数据
- [本地监控PLC数据](#本地监控PLC数据)
- [在Thingsboard上监控PLC数据](#在Thingsboard上监控PLC数据)  
  
<a id="本地监控PLC数据"> </a>  

### 3.1 本地监控PLC数据
数据采集配置完成后，可以在“边缘计算>>PLC Supervisor>>PLC列表”页面查看数据采集情况。点击PLC列表中的设备卡片可切换需要查看的PLC数据
![](images/2020-02-27-17-14-47.png)  

点击数值栏的按钮可进行写入操作  
![](images/2020-03-06-16-59-18.png)  

![](images/2020-03-06-16-59-44.png)  

修改成功如下图所示  
![](images/2020-03-06-17-01-19.png)

<a id="在Thingsboard上监控PLC数据"> </a>  

### 3.2 在Thingsboard上监控PLC数据
#### 3.2.1 配置Thingsboard
Thingsboard的详细使用方法请查看[Thingsboard入门手册](https://thingsboard.io/docs/getting-started-guides/helloworld/)，您也可以按照[参考流程](#Thingsboard参考流程)进行测试。

#### 3.2.2 配置云服务
进入“边缘计算>>PLC Supervisor>>云服务”页面，勾选启用云服务并配置相应的MQTT连接参数，配置完成后点击提交。
- 服务器地址：`demo.thingsboard.io`
- 端口号：1883
- MQTT客户端ID：任一唯一ID
- MQTT用户名：Thingsboard设备的访问令牌，访问令牌获取方式见[传输PLC数据到Thingsboard设备](#传输PLC数据到Thingsboard设备)
- MQTT密码：任意6~32位密码
- 其余项使用默认配置即可  

配置完成后如下图所示：  </br>
![](images/2020-02-28-17-38-08.png)

提交后点击“高级设置”以配置发布和订阅主题。发布和订阅主题的配置方法请参考[自定义数据格式](#自定义数据格式)。
- 发布主题：
  - 主题：`v1/devices/me/telemetry`
  - Qos(MQTT)：1
  - 分组：需要上传至thingsboard的数据
  - 主函数：入口函数名称，本文档为`test_upload`
  - 函数实现：
    ```python
    from common.Logger import logger #导入打印日志模块logger
    
    def test_upload(data, global_argv, mqtt_publish, save_db): #定义主函数test_upload
        value_dict = {} #定义上报的数据字典value_dict
        for device, val_dict in data['values'].items(): #遍历data中的values字典，该字典中包含设备名称和设备下的变量数据
            for id, val in val_dict.items(): #遍历变量数据，为value_dict字典赋值
                value_dict[id] = val["raw_data"]
            value_dict["timestamp"] = data["timestamp"]
        logger.info(value_dict) #在日志中以info等级打印value_dict
        return value_dict ##将value_list发送给App，由App自行顺序上传至MQTT服务器。最终的value_list格式为{'bool': False, 'byte': 7, 'real': 0.0, 'timestamp': 1583990892.5429199}
    ```

- 订阅主题
  - 主题：`v1/devices/me/rpc/request/+`
  - Qos(MQTT)：1
  - 主函数：入口函数名称，本文档为`test_ctl`
  - 函数实现：
    ```python
    from common.Logger import logger #导入打印日志模块logger
    import json #导入json模块
    
    def test_ctl(topic, payload, send_message_to_partner=None): #定义主函数test_ctl
        logger.info(topic) #打印订阅主题
        logger.info(payload) #打印订阅数据，Thingsboard的下发数据格式为{"method":"setValue","params":true}
        payload = json.loads(payload) #反序列化订阅数据
        if payload["method"] == "setValue": #检测是否为写入数据
            message = {"bool":payload["params"]} #定义下发消息，包括下发的变量名称和变量值
            response_data = [topic.replace('request', 'response'), message] #定义确认数据，包括响应的主题和消息
            send_message_to_partner(message, "write_plc_values", ack, response_data) #调用send_message_to_partner方法，将message字典中的数据下发至指定变量；调用ack方法并发送response_data给ack方法

    
    def ack(data, tail, mqtt_publish): #定义ack方法
        resp_data = tail[1] #定义响应数据
        mqtt_publish(tail[0], json.dumps(resp_data), 0) #调用mqtt_publish将响应数据发送给MQTT服务器
    ```

<a id="附录"> </a>  

## 附录
- [导入导出配置](#导入导出配置)
- [自定义数据格式](#自定义数据格式)
- [其他网关操作](#其他网关操作)
- [Thingsboard参考流程](#Thingsboard参考流程)  

<a id="导入导出配置"> </a>  

### 导入导出配置
PLC Supervisor的数据采集配置总共包含三个CSV格式的配置文件，您可以通过导入导出配置文件快速实现采集配置。各配置文件内容如下：
- device.csv：设备配置文件,详细参数如下
  - device_name：设备名称
  - protocol：通讯协议名称，如`ModbusTCP`
  - ip/serial：以太网设备填写ip地址；串口设备填写RS485或RS232
  - port：以太网设备的通讯端口号
  - rack（仅Snap7设备）：设备机架号
  - slot（仅Snap7设备）：设备槽号
  - slave（仅Modbus设备）：从站地址
  - byte_order（仅Modbus设备）：字节序  

  导出方式为PLC列表页面的设备列表导出
  ![](images/2020-03-10-17-17-06.png)  

  示例配置如下：  

  ![](images/2020-03-10-17-15-00.png)  

  &nbsp;
  </br>
  
- var.csv:变量配置文件，详细参数如下
  - var_name：变量名称
  - device：变量所属设备
  - protocol：通讯协议名称
  - dbnumber（仅Snap7设备）：DB号
  - register_type（仅Snap7设备）：寄存器类型，如`DB`
  - register_addr：寄存器地址
  - register_bit：位偏移
  - data_type：数据类型
  - read_write：读写权限，包括`Read/Write`、`Write`、`Read`
  - float_repr：小数位，1~6
  - mode：采集模式，包括`realtime`、`onchange`
  - unit：单位
  - size：字符串长度
  - desc：描述
  - group：所属分组  

  导出方式为PLC列表页面的变量列表导出
  ![](images/2020-03-10-17-18-01.png)  

  示例配置如下：  

  ![](images/2020-03-10-17-13-54.png)  

  &nbsp;
  </br>
  
- group.csv:分组配置文件，详细参数如下
  - group_name：分组名称
  - polling_interval：采集间隔
  - upload_interval：上传间隔  
 &nbsp;

  导出方式为分组页面的分组导出  </br>
  ![](images/2020-03-10-17-19-04.png)  

  示例配置如下：  

  ![](images/2020-03-10-17-15-33.png)

<a id="自定义数据格式"> </a>  

### 自定义数据格式
- [发布](#发布)
- [订阅](#订阅)  
  
您可使用云服务中的高级设置功能配置MQTT主题、上报数据等参数并支持使用Python语言自定义MQTT发布和订阅主题的数据上报、处理等逻辑。无需二次开发即可实现与多种纯MQTT服务器进行数据上传和下发。

<a id="发布"> </a>  

#### 发布
自定义发布主题中包含以下项：
- 发布名称：自定义发布名称
- 发布主题：与MQTT服务器订阅的数据主题一致
- Qos(MQTT)：建议与MQTT服务器的Qos一致
- 分组：选中分组后，分组下所有变量通过该发布主题和函数实现将变量数据上传至MQTT服务器（可选择多个分组）
- 主函数名称：即入口函数名称，与函数实现中的入口函数名称保持一致
- 函数实现：使用Python代码自定义组包和处理逻辑，主函数的参数包括：
  - data：PLC Supervisor采集到的变量数据，数据类型为dict。数据格式如下  
    ```python
    {
      "timestamp": 1583292673.516777, #数据产生时间戳
      "group_name": "default" #分组名称
      "values": { #数据字典，包括PLC名称，变量名称和变量值等数据
        "S7-1200": { #PLC名称
          "Test1": { #变量名称
            "raw_data": false,  #真实数据
            "str_data": "False",  #字符串格式的真实数据
            "status": 1 #采集状态，非1即为采集异常
          }, 
          "Test2": {
            "raw_data": 13.300000000000001, 
            "str_data": "13.300000000000001", 
            "status": 1
          }
        }
      },  
    }
    ```
  - global_argv：全局参数页面中配置的全局参数项，数据类型为dict。默认如下
    ```python
    {
      "log_level": "INFO",  #日志等级
      "gateway_sn": "xxxxxx" #网关序列号
    }
    ```
  - mqtt_publish：MQTT发布消息方法，用于将指定数据发送到相应的主题并返回发送结果：成功（True），失败（False）。方法参数包含：
    - topic：发送数据至该主题
    - payload：需要发送的数据
    - qos：qos等级（0，1，2）
  - save_data：存储历史数据方法，采用队列的方式存储数据。方法参数包含：
    - data：需要存储的数据
    - group_name：组名
    - userdate：默认为None

以下是两个常见的自定义发布方法用例：
- 用例1（使用return方式上传数据，<font color=#FF0000>禁止mqtt_publish和save_data方法与return同时使用</font>）：
  ```python
  import logging
  """
  在网关中打印日志通常有两种办法。
  1.import logging：使用logging.info(XXX)打印日志，该方法的日志显示不受全局参数页面中的日志等级参数控制。
  2.from common.Logger import logger：使用logger.info(XXX)打印日志，该方法的日志显示受全局参数页面中的日志等级参数控制。
  """

  def test_upload(data, global_argv, mqtt_publish=None, save_data=None): #定义发布主函数
      value_list = [] #定义数据列表
      for device, val_dict in data['values'].items(): #遍历values字典，该字典中包含设备名称和设备下的变量数据
          value_dict = { #自定义数据字典
                        "Device": device,
                        "timestamp": data["timestamp"],
                        "Data": {}
                        }
          for id, val in val_dict.items(): #遍历变量数据，为Data字典赋值
              value_dict["Data"][id] = val["raw_data"]
          value_list.append(value_dict) #依次将设备名称和设备的数据添加到value_list中
      logging.info(value_list) #在App日志中打印value_list
      return value_list #将value_list发送给App，App将自行按照采集时间顺序上传至MQTT服务器。如果发送失败则缓存数据等待连接恢复后按时间顺序上传至MQTT服务器
    ```  
  最终上传至平台的数据格式(value_list)如下：
  ```python
  [
    {
      'Device': 'Modbus', 
      'timestamp': 1583462030.720562, 
      'Data': {'TT1': 4}
      }, 
    {
      'Device': 'S7-1200', 
      'timestamp': 1583462030.720562, 
      'Data': {'Test1': False}
      }
  ]
  ```
- 用例2（使用`mqtt_publish`上传数据并使用`save_data`存储上传失败的数据。上传失败的数据会在连接正常时按时间顺序依次上传）：
  ```python
  import logging
  import json
  """
  在网关中打印日志通常有两种办法。
  1.import logging：使用logging.info(XXX)打印日志，该方法的日志显示不受全局参数页面中的日志等级参数控制。
  2.from common.Logger import logger：使用logger.info(XXX)打印日志，该方法的日志显示受全局参数页面中的日志等级参数控制。
  """

  def test_upload(recv, global_argv, mqtt_publish=None, save_data=None): #定义发布主函数
      value_list = [] #定义数据列表
      for device, val_dict in recv['values'].items(): #遍历values字典，该字典中包含设备名称和设备下的变量数据
          value_dict = { #自定义数据字典
                        "DeviceSN": device,
                        "Time": recv["timestamp"]
                        "Data": {}
                         }
          for id, val in val_dict.items(): #遍历变量数据，为Data字典赋值
              value_dict["Data"][id] = val["raw_data"]
          value_list.append(value_dict) #依次将设备名称和设备的数据添加到value_list中
      if not mqtt_publish("v1/xxx/yyy", json.dumps(value_list), 1): #调用mqtt_publish方法将value_list数据通过主题“v1/xxx/yyy”，qos等级1发送至MQTT服务器并检测是否发送成功
          save_db(value_list, recv["group_name"]) #发送失败则存储数据，等待连接恢复后将按时间顺序上传存储数据
      logger.info(value_list) #在App日志中打印value_list
  ```
  最终上传至平台的数据格式(value_list)如下：
  ```python
  [
    {
      'Device': 'Modbus', 
      'timestamp': 1583462030.720562, 
      'Data': {'TT1': 4}
      }, 
    {
      'Device': 'S7-1200', 
      'timestamp': 1583462030.720562, 
      'Data': {'Test1': False}
      }
  ]
  ```

<a id="订阅"> </a>  

#### 订阅
自定义订阅中包含以下项：
- 订阅名称：自定义名称
- 订阅主题：与MQTT服务器订阅的数据主题一致
- Qos(MQTT)：建议与MQTT服务器的Qos一致
- 主函数名称：与函数实现中的主函数名称保持一致
- 函数实现：使用Python代码自定义组包和处理逻辑，主函数的参数包括
  - topic：订阅的主题，数据类型为string
  - payload：订阅的数据，数据类型为string（一般为json字符串）
  - send_message_to_partner：将接收到的数据发给指定服务的方法  

`send_message_to_partner`方法参数(系统方法)：
- message：需要发送给指定服务的数据，数据类型为dict。当参数operate为"write_plc_values"时消息格式如下
  ```python
  {
    "test1":12.3 #变量名:值
    "test2":"True"
  }
  ```
- operate：目前仅支持"write_plc_values"，用于写入数据到PLC变量
- ack（非必填项）：调用ack方法，一般用于将数据下发结果返回给平台。默认值None
- ack_tail（非必填项）：ack方法的特殊参数，一般用于将下发数据中需要返回给平台的特殊数据传给ack方法。
- timeout（非必填项）：超时时间，默认为60秒

自定义ack方法参数：
- send_result: send_message_to_partner方法的写入结果
  - 写入超时时send_result为None
  - 写入成功时send_result格式参考：`[{'value': 12.300000000000001, 'device': 'Modbus_test', 'var_name': 'SP1', 'result': 'OK'}]`；
  - 写入失败时send_result格式参考：`[{'value': 12.300000000000001, 'device': 'Modbus_test', 'var_name': 'SP1', 'result': 'Failed'}]`；
- tail：send_message_to_partner方法中的ack_tail数据
- mqtt_publish：MQTT发布消息方法（可能受网络影响导致发布失败）

以下是三个常见的自定义订阅方法用例：
- 用例1：下发变量名称和变量值写入PLC数据且不返回写入结果
  ```python
  import logging
  import json
  
  def test_ctl(topic, payload, send_message_to_partner=None): #定义订阅主函数
      logging.info(topic) #打印订阅主题
      logging.info(payload) #打印订阅数据
      #假定payload数据为{"method":"setValue", "TagName":"SP1", "TagValue":12.3}
      payload = json.loads(payload) #反序列化订阅数据
      if payload["method"] == "setValue": #检测是否为写入数据
          message = {payload["TagName"]:payload["TagValue"]} #定义下发消息，包括下发的变量名称和变量值
          send_message_to_partner(message, "write_plc_values") #调用send_message_to_partner方法，将message字典中的数据下发至指定变量
  ```
- 用例2：下发设备名称，变量名称和变量值写入PLC数据且不返回写入结果
  ```python
  import logging
  import json
  
  def test_ctl(topic, payload, send_message_to_partner=None): #定义订阅主函数
      logging.info(topic) #打印订阅主题
      logging.info(payload) #打印订阅数据
      #假定payload数据为{"method":"setValue","Device":"Modbus_test", "TagName":"SP1", "TagValue":12.3}
      payload = json.loads(payload) #反序列化订阅数据
      data_dict = {payload["TagName"]:payload["TagValue"]} #定义下发的数据字典，包含下发的变量名称和变量值
      var_device = payload["Device"] #定义设备名称
      if payload["method"] == "setValue": #检测是否为写入数据
          message = {var_device:data_dict} #定义下发消息，包括设备名称和下发的数据字典
          send_message_to_partner(message, "write_plc_values") #调用send_message_to_partner方法，将message字典中的数据下发至指定变量
  ```
- 用例3：远程写入PLC数据并返回写入结果
  ```python
  import logging
  import json
  
  def test_ctl(topic, payload, send_message_to_partner=None): #定义订阅主函数
      logging.info(topic) #打印订阅主题
      logging.info(payload) #打印订阅数据
      #假定payload数据为{"method":"setValue","Device":"Modbus_test", "TagName":"SP1", "TagValue":12.3}
      payload = json.loads(payload) #反序列化订阅数据
      data_dict = {payload["TagName"]:payload["TagValue"]} #定义下发的数据字典，包含下发的变量名称和变量值
      var_device = payload["Device"] #定义设备名称
      if payload["method"] == "setValue": #检测是否为写入数据
          message = {var_device:data_dict} #定义下发消息，包括设备名称和下发的数据字典
          ack_tail = [topic.replace('request', 'response'), message] #定义确认数据，包括响应的主题和消息
          logging.info(message)
          send_message_to_partner(message, "write_plc_values", ack, ack_tail, timeout = 10) #调用send_message_to_partner方法，将message字典中的数据下发至指定变量；调用ack方法并发送ack_tail给ack方法
  
  def ack(send_result, ack_tail, mqtt_publish): #定义ack方法
      topic = ack_tail[0] #定义响应主题
      if not send_result: #检测下发是否超时
          resp_data = {"Status":"timeout", "Data":ack_tail[1]} #定义下发超时的响应数据
      else:
          resp_data = {"Status":send_result[0]["result"], "Data":ack_tail[1]} #定义下发未超时的响应数据
      mqtt_publish(topic, json.dumps(resp_data), 0) #调用mqtt_publish将响应数据发送给MQTT服务器
  ```

<a id="其他网关操作"> </a>  

### 其他网关操作
关于网关的其他常用操作请查看[IG500快速使用手册](http://doc.ig.inhand.com.cn/zh_CN/latest/IG501%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html)或[IG900快速使用手册](http://doc.ig.inhand.com.cn/zh_CN/latest/IG902%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.html)。

<a id="Thingsboard参考流程"> </a>  

### Thingsboard参考流程
- [添加设备和资产](#添加设备和资产)
- [传输PLC数据到Thingsboard设备](#传输PLC数据到Thingsboard设备)
- [配置可视化仪表板](#配置可视化仪表板)  
   
<a id="添加设备和资产"> </a>  

#### 添加设备和资产
访问`https://demo.thingsboard.io/login`，输入登录账号和密码。如果未注册过账号则需要先注册账号后再登录。  

![](images/2020-02-26-16-27-53.png)  <br/>

登录后，进入属性页面修改语言为简体中文
![](images/2020-02-26-09-50-27.png)

- 添加一个资产
![](images/2020-02-26-10-27-13.png)  

  ![](images/2020-02-26-10-27-40.png)  

  添加成功后如下图所示：  <br/>

  ![](images/2020-02-26-09-52-39.png)  
&nbsp;
</br>

- 添加一个设备
![](images/2020-02-26-09-54-14.png)  

  ![](images/2020-02-26-09-54-27.png)  
&nbsp;

  建立资产与设备的关联
![](images/2020-02-26-09-56-01.png)  

  添加完成后如下图所示
![](images/2020-02-26-09-56-57.png)  
&nbsp;

<a id="传输PLC数据到Thingsboard设备"> </a>  
  
#### 传输PLC数据到Thingsboard设备
资产和设备配置完成后，复制已添加设备的访问令牌并粘贴至网关的云服务页面的用户名参数中以将数据传输至Thingsboard中的Snap7设备。
![](images/2020-02-26-09-58-18.png)  

随后可在设备的最新遥测中查看已上传的数据。
![](images/2020-02-26-10-38-50.png)

<a id="配置可视化仪表板"> </a>  

#### 配置可视化仪表板
- [添加仪表板](#添加仪表板)
- [添加趋势图](#添加趋势图)
- [添加开关](#添加开关)
<a id="添加仪表板"> </a>  

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
&nbsp;

<a id="添加趋势图"> </a>  
- 添加趋势图  
  
  在部件中选择Charts并点击Timeseries-Flot。
![](images/2020-02-26-10-03-51.png)  

  在图表的数据页面为趋势图添加展示数据。
![](images/2020-02-26-10-14-28.png)  

  ![](images/2020-02-26-10-15-50.png)  

  添加完成后如下图所示：
![](images/2020-02-26-10-18-00.png)
&nbsp;

<a id="添加开关"> </a>  
- 添加开关  
  
  点击添加，选择创建新部件以添加一个控制开关。
![](images/2020-02-26-10-21-47.png)  

  在部件中选择Control widgets并点击Switch control。
![](images/2020-02-26-10-20-10.png)  

  随后选择目标设备。
![](images/2020-02-26-10-20-36.png)

  配置完成后调整部件的大小和布局并保存。
![](images/2020-02-26-10-22-40.png)
  <br> </br>
  随后可以通过开关下发控制命令以及通过趋势图查看数据趋势。
![](images/2020-02-26-10-22-59.png)