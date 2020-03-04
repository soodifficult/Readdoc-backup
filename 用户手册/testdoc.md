# 标题1
内容1  

内容2  

![](images/2019-11-29-16-18-51.png)  

内容3

自定义发布方法的参数：
| 参数 | 类型 |  描述 | 参数说明 |
| :---:| :---: | :---: | :---: |
| data | dict | PLC Supervisor处理后的需要上传的数据 | 数据格式：{'timestamp': <数据产生时间戳>,'values': {'<变量名>': {"raw_data": <真实数据>, "str_data": "<本条数据字符串格式>", "status": <状态，非1即采集异常>}},'group_name': '<组名>'}
| global_argv | dict | 配置的全局参数 | 默认值：{"log_level": "INFO", "gateway_sn": "xxxxxx"}, log_level：日志等级（"INFO","DEBUG","WARNING","ERROR",），gateway_sn：设备序列号。|
| mqtt_publish | function | MQTT发布消息方法 | 方法参数：(topic, payload, qos), 返回值：成功（True），失败（False）|
| save_data | function | 存储历史数据方法 | 方法参数：(data, group_name, userdata=None), 此方法采用队列的方式存储数据。|