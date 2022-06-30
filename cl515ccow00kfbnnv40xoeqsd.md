## 5G模块建立网络连接-移远RM500U-CN
How to use 5G modules to establish Internet connection
(Take Quectel RM500U-CN as an example)

# 5G模块建立网络连接-移远RM500U-CN

## 概要

移远RM500U-CN + 官方转接板

Windows 10 + Quectel_Windows_USB_Driver(U)_For_ECM_RNDIS_**V1.08** + QFlash_V5.9_CN

固件RM500UCNAAR01**A16**M2G_01.001.01

## 手动拨号上网

`1. Quectel_RG200U-CN&Rx500U-CN_网卡拨号应用指导_V1.1.pdf `

`2. Quectel_RG50xQ&RM5xxQ系列_AT命令手册_V1.0.pdf`

### 驱动类型

#### 兼容性

不同的协议在不同的操作系统下有不同的兼容性，如下表格

![image-20220630221359570](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630221359am9nRQimage-20220630221359570.png)

macOS/iPadOS的兼容性类似于Linux，已验证NCM免驱可用

#### 配置

![image-20220630221135516](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630221135BTZ83Fimage-20220630221135516.png)

![image-20220630221301923](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630221302UOFqhCimage-20220630221301923.png)

```bash
AT+QCFG="usbnet",3 
## Windows 调试
AT+QCFG="usbnet",5 
## macOS/iPadOS 使用
```

### NAT方式

执行 **AT+QCFG="nat",0** 配置拨号模式为网卡模式; 

或者执行 **AT+QCFG="nat",1** 配置拨号模式为路由模式; 

或者执行 **AT+QCFG="nat",2** 配置拨号模式为网桥模式。

```bash
AT+QCFG="nat",0
```

### Ethernet 网卡

执行 **AT+QCFG="ethernet",1** 开启 Ethernet 网卡;

或者执行 **AT+QCFG="ethernet",0** 关闭 Ethernet 网卡。

![image-20220630221815848](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630221815LuV5kSimage-20220630221815848.png)

其中Ethernet依赖于PCIe转接，在本应用中无影响

**:warning: 需要重启`AT+CFUN=1,1`**

### 拨号上网

![image-20220630222034499](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630222034yY5wIZimage-20220630222034499.png)

![image-20220630222049168](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630222049LnIBo9image-20220630222049168.png)

![image-20220630222059014](https://cdn.jsdelivr.net/gh/TANG617/images@master/20220630222059d5dUiCimage-20220630222059014.png)

```bash
AT+QNETDEVCTL=1,3,1
# （貌似）一号槽位是运营商默认的APN配置
# （理论上）x,3,x 会上电自动拨号并连接（但是并不会）
```

