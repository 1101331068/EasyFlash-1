# EasyFlash 使用说明

---

## 1、介绍

EasyFlash是一款开源的轻量级嵌入式Flash存储器库，主要为MCU(Micro Control Unit)提供便捷、通用的上层应用接口，使得开发者更加高效实现基于的Flash存储器常见应用开发。该库目前提供 **两大实用功能** ：

 - **Env** 让变量轻松实现掉电保存，支持 **写平衡** 模式，无需担心变量长度、磨损平衡等问题
 
 使用 **键值对(key-value)** 方式将变量存储到Flash中。在产品上，能够更加简捷的实现 `设定参数` 或 `运行日志` 等信息掉电保存的功能。
 - **IAP** 在线升级再也不是难事儿
 
 该库封装了IAP(In-Application Programming)功能常用的接口，支持CRC32校验，同时支持Bootloader及Application的升级。

### 1.1、文件结构

|源文件                                 |描述   |
|:------------------------------        |:----- |
|\flash\src\flash_env.c                 |Env（常规模式）相关操作接口及实现源码|
|\flash\src\flash_env_wl.c              |Env（磨损平衡模式）相关操作接口及实现源码|
|\flash\src\flash_iap.c                 |IAP 相关操作接口及实现源码|
|\flash\src\flash_utils.c               |EasyFlash常用小工具，例如：CRC32|
|\flash\src\flash.c                     |目前只包含EasyFlash初始化方法|
|\flash\port\flash_port.c               |不同平台下的EasyFlash移植接口及配置参数|
|\demo\non_os\stm32f10x                 |stm32f10x裸机的demo|
|\demo\rtt\stm32f10x                    |stm32f10x基于RT-Thread的demo|
|\demo\stm32f4xx                        |stm32f4xx平台下的demo|

### 1.2、资源占用

```
最低要求： ROM: 6K bytes     RAM: 0.5K bytes + (Env大小)

Demo平台：STM32F103RET6 + RT-Thread 1.2.2 + Env(2K bytes)
实际占用： ROM: 6K bytes     RAM: 2.6K bytes
```

### 1.3、支持平台

目前已移植硬件平台有 `stm32f10x`与 `stm32f4xx` 系列的片内Flash，这个也是笔者产品使用的平台。其余平台的移植难度不大，在项目的设计之初就有考虑针对所有平台的适配性问题（64位除外），所以对所有移植接口都有做预留。移植只需修改 `\flash\port\flash_port.c` 一个文件，实现里面的擦、写、读及打印功能即可。

欢迎大家 **fork and pull request**([Github](https://github.com/armink/EasyFlash)|[OSChina](http://git.oschina.net/armink/EasyFlash)|[Coding](https://coding.net/u/armink/p/EasyFlash/git)) 。开源软件的成功离不开所有人的努力，也希望该项目能够帮助大家降低开发周期，让产品更早的获得成功。

## 2、流程

### 2.1、环境变量

下图为人工通过控制台来调用环境变量的常用接口，演示了环境变量 `"temp"` 从创建到保存，再修改，最后删除的过程。这些接口都支持被应用层直接调用。

![easy_flash_env](https://cloud.githubusercontent.com/assets/1734686/5886463/46ad7efa-a3db-11e4-8401-75c00a4c35ba.gif)

### 2.2、在线升级

下图演示了通过控制台来进行IAP升级软件的过程，使用的是库中自带的IAP功能接口，演示采用的是串口+Ymodem协议的方式。你还也可以实现通过CAN、485、以太网等总线，来实现远程网络更新。

![easy_flash_iap](https://cloud.githubusercontent.com/assets/1734686/5886462/40f7d62c-a3db-11e4-866a-ba827c809370.gif)

## 3、文档
具体内容参考`\docs\`下的文件。

## 4、版权
采用 GPL v3.0 开源协议，细节请阅读项目中的 LICENSE 文件内容。


