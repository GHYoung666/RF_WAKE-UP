# RF_WAKE-UP  
NEAR-ZERO RF MEMS SENSING WAKE-UP SYSTEM  
来自本人的srtp项目：“面向无线传感的RF唤醒电路”，仅做笔记使用

## 想法  
- [ ] 框架闭环供电
- [ ] MPPT功率点追踪
- [ ] 误触发检测
- [ ] 加入储能元件
- [ ] 能否节省开关

## 整体框架
### 原框架  
<img width="500" alt="image" src="https://user-images.githubusercontent.com/82877682/210565098-1515ee78-79a0-4408-b6c4-58c8d27c978c.png"> <img width="500" alt="image" src="https://user-images.githubusercontent.com/82877682/210563955-82c9d245-179d-4e68-b448-89521b17dbda.png">

### 闭环结构 
<img width="501" alt="image" src="https://user-images.githubusercontent.com/82877682/210812233-2bb20b64-0a09-4640-8e08-741edfc66cc9.png">  
不知道什么原因，Multisim上的仿真存在一些问题，MOS开关和继电器开关不一样，软件把MOS开关断开时当成一个普通电阻来看了，因此该结构可行性未知

## RF天线
采用微带天线


## 阻抗匹配
T型阻抗匹配


## 整流电路
**种类**：半波整流、单阶倍压整流、二阶倍压整流等。理论上来说阶数越高整流效果越好  
- 半波整流：转换效率低
- 单阶倍压整流：实物效果刚好
- 二阶倍压整流：理论上转换效率更高，其输出电压的测试结果低于仿真结果，这可能是元器件数量增多后寄生效应增强以及损耗增大导致的
- 全栅交叉耦合整流器FGCC：未知，似乎对于低功率信号转换效率更高

**肖特基二极管**：更适合高频电路  
**滤波器**：微带型滤波器  
**整流阵列**：提高转换效率  
- 采用功合器并联
- 采用多个整流电路串联，使用多层介质基板


## 能量采集（energy harvester）  
BQ25504芯片是一个适用于能量收集应用并具有电源管理功能的超低功耗升压转换器，其冷启动最小输入电压为330mV，最小输入功耗为15µW，而热启动阶段最小输入电压为130mV，而输出升压可以在2.2V至5.25V。其升压过程包括冷启动过程以及热启动过程，当冷启动升压阶段结束后，主升压充电器开启，升压效率提高。并且具有可编程动态**最大功率点跟踪**（MPPT），可以动态调节输入阻抗，从而实现针对能量源的最大功率传输并保护输入源不受损坏。同时还具有对输出端电池电压的从监测保护，并且可以输出电池工作状态。

在VIN_DC引脚和GND之间有ROC2和ROC1串联的电阻网络，而VOC_SAMP在ROC2与ROC1电阻之间，即BQ25504对VIN_DC进行采样，并存储在VREF_SAMP外接的电容上，进而控制改变芯片输入阻抗，使得能量源接入升压模块时可以最大功率的能量传输。VIN_DC开路电压通过外部电阻进行编程，并由外部电容（CREF）保持。

对于限大功率点为80%开路电压的太阳能电池，可将电阻分压器设置为VIN_DC电压的80%，此时该网络会将VIN_DC控制在采样的基准电压附近，而对于RF能量来说，最大功率点可能需要重新进行建模确定。此外，此芯片可以通过MCU提供外部基准电压，产生一个更为复杂的MPPT算法。

![image](https://user-images.githubusercontent.com/82877682/210732741-61c3a9ac-489c-429c-8206-066cdd6048e3.png)
![image](https://user-images.githubusercontent.com/82877682/210732772-0a89b7da-cbff-484a-837e-c45913631ceb.png)

上图为框架及MPPT功率点设置


