/*********************************************************************************************/

【*】 程序简介 

本例程使用开发板接入OneNET，并且上报温湿度数据
 
实验中使用MQTT协议传输数据(依赖TCP协议) ，开发板作为MQTT Client

/*********************************************************************************************/

【 ！！】注意事项：
 接口：板子左侧的“USB TO UART”接口
 跳线帽：使用跳线帽连接 RX<--->A9,TX<--->A10 (出厂默认已连接,在SWD下载接口下方位置)。
 串口波特率：115200
 
需要有DHT11温湿度传感器
 
由于本例程是提交到dp主题的，因此串口无输出内容

需要观看本实验现象,请在浏览器打开次连接：https://open.iot.10086.cn/iotbox/appsquare/appview?openid=c673cc3ee3e436d298494aba2e5c08b8

由于本例程是对所有人开放,如果同时有人使用这个例程连接到OneNET的话,服务器将会断开已经连接的客户端,而非例程错误,请悉知
 
 /*********************************************************************************************/
 
【 ！】实验操作：
电脑端使用串口调试助手，选择电脑与STM32相连的COM口，设置为115200-N-8-1，
复位开发板，即可接收STM32串口发送给电脑的数据。

网络连接模型如下：
	 电脑<--网线-->路由<--网线-->开发板

在开发板的dht11接口接上DHT11温湿度传感器

请将电脑上位机设置为TCP Client.输入开发板的IP地址(如192.168.0.122)

修改对应的宏定义:IP_ADDR0,IP_ADDR1,IP_ADDR2,IP_ADDR3

/*********************************************************************************************/

【！！】默认情况：

本例程将使用DHCP动态分配IP地址,如果不需要则在lwipopts.h中将LWIP_DHCP定义为0

本地IP地址是:192.168.0.198	

OneNET IP地址/域名

  "mqtt.heclouds.com"     //服务器域名
  "183.230.40.39"     //服务器IP地址

端口号:6002

基本信息(根据在阿里云创建的设备进行修改，具体参考书籍第24章 连接到 OneNET):

#if    LWIP_DNS
#define   HOST_NAME       "mqtt.heclouds.com"     //服务器域名
#else
#define   HOST_NAME       "183.230.40.39"     //服务器IP地址
#endif


#define   HOST_PORT     6002    

#define   CLIENT_ID     "518725049"         //
#define   USER_NAME     "217537"     //用户名
#define   PASSWORD      "12345"  //秘钥

#define   TOPIC         "temp_hum"      //订阅的主题
#define   TEST_MESSAGE  "test_message"  //发送测试消息


/*********************************************************************************************/

【*】 引脚分配

串口（TTL-USB TO UART）：
CH340的收发引脚与STM32的发收引脚相连。
	RX<--->PA9
	TX<--->PA10
以太网：
	PC1     ------> ETH_MDC
	PA1     ------> ETH_REF_CLK
	PA2     ------> ETH_MDIO
	PA7     ------> ETH_CRS_DV
	PC4     ------> ETH_RXD0
	PC5     ------> ETH_RXD1
	PB11     ------> ETH_TX_EN
	PG13     ------> ETH_TXD0
	PG14     ------> ETH_TXD1 
/*********************************************************************************************/

【*】 时钟

A.晶振：
-外部高速晶振：25MHz
-RTC晶振：32.768KHz

B.各总线运行时钟：
-系统时钟 = SYCCLK = 180Mhz
-HCLK = 180Mhz
-PLLCLK = 180Mhz
-PCLK2 = 90MHz
-PCLK1 = 45MHz
 
C.浮点运算单元：
  使能

/*********************************************************************************************/

【*】 版本

-程序版本：1.0
-发布日期：2019-5

-版本更新说明：首次发布

/*********************************************************************************************/

【*】 联系我们

-野火论坛    :http://www.firebbs.cn
-淘宝店铺    :http://firestm32.taobao.com

/*********************************************************************************************/