# 标题测试
PLC Supervisor App（以下简称PLC Supervisor）为用户提供了便捷的数据采集、数据处理和数据上云功能，支持Snap7、ModbusRTU等多种工业协议解析。
本手册以采集PLC的数据并上传至Thingboard云平台为例说明如何通过PLC Supervisor App实现PLC数据采集和数据上云。以下将InGateway500简称为“IG500”；InGateway900简称为“IG900”。

[采集接线1](#ig500tt1)
[采集接线3](#ig500tt3)
d1  

d1  

d1  

d1  

d  

1d  

1d  

1d  

1d  

1d  


1d  

1d  


1  

d1  

d1  

d1   
d1  

d1  

d1  
d1  ****

d1  
d1  


d1  

d1  


d1  

d1  


## 1.准备硬件设备及其数据采集环境<h2 id="ig500tt1"></h2>

### 1.1 硬件接线
#### 以太网数据采集接线
- IG900以太网接线  
  
  接通IG900的电源并按照拓扑使用以太网线连接IG900和PLC。  <br/>
![](images/2020-02-21-14-52-40.png)  

- IG500以太网接线  
  接通IG500的电源并按照拓扑使用以太网线连接IG500和PLC。  <br/>
![](images/2020-02-21-14-53-05.png)
- IG900串口接线  

  接通IG900的电源并按照拓扑连接IG900和PLC。  <br/>
![](images/2020-02-21-16-56-55.png)  

  IG900正上方的端子接线说明如下图：  
![](images/2020-01-09-18-47-30.png)  
## 2.准备软件<a name="ig500tt3"></a>