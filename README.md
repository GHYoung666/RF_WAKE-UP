# RF_WAKE-UP  
NEAR-ZERO RF MEMS SENSING WAKE-UP SYSTEM  
来自本人的srtp项目：“面向无线传感的RF唤醒电路”，仅做笔记使用


## 整体框架
<img width="600" alt="image" src="https://user-images.githubusercontent.com/82877682/210565098-1515ee78-79a0-4408-b6c4-58c8d27c978c.png">  
MEMS开关2可否省去？


## RF天线
采用微带天线


## 阻抗匹配
T型阻抗匹配


## 整流电路
种类：半波整流、单阶倍压整流、二阶倍压整流等。理论上来说结束越高整流效果越好  
- 半波整流：转换效率低
- 单阶倍压整流：实物效果刚好
- 二阶倍压整流：理论上转换效率更高，其输出电压的测试结果低于仿真结果，这可能是元器件数量增多后寄生效应增强以及损耗增大导致的

肖特基二极管：更适合高频电路  
滤波器：微带型滤波器  
整流阵列提高转换效率  
- 采用功合器并联
- 采用多个整流电路串联，使用多层介质基板


<img width="606" alt="image" src="https://user-images.githubusercontent.com/82877682/210563955-82c9d245-179d-4e68-b448-89521b17dbda.png">  
这里的MOS开关是否有效？
