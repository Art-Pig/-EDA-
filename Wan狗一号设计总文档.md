# Wan狗一号设计总文档

## 1.设计思路

设计目的：毕业设计作品，简历所需项目经历；

先将其能动了，再考虑其他功能吧。再具体加上一些模块就好了；PCB设计加上插口，之后要加具体功能直接用杜邦线插上引脚就好了；

### 1.01 外观

模仿罗威纳的流线体造型，外观大体以橄榄绿为基准，参考主流机器狗外观；

**罗威纳**

![**罗威纳犬**](https://p1.ssl.qhimg.com/t01cd8a5c2084893401.jpg)

![羅威納犬剪影圖案素材 | PNG和向量圖 | 透明背景圖片 | 免費下载 - Pngtree](https://png.pngtree.com/png-clipart/20231226/original/pngtree-rottweiler-dog-silhouette-vector-png-image_13939148.png)

![德系罗威纳犬价格罗威纳犬好养吗_工作犬](https://th.bing.com/th/id/R.bc0c9422b519414bf5630f34dc173a3c?rik=2Iz1AxR2BTZmZg&riu=http%3a%2f%2f5b0988e595225.cdn.sohucs.com%2fimages%2f20180812%2fbccb74eff15646789077cea874ba8c11.jpeg&ehk=Pbni6ILCk4dcUgqJI%2fGfsmsg%2fhYusTBTnAcjroFGyc8%3d&risl=&pid=ImgRaw&r=0)

![Собаки поводыри. 9 пород собак для незрячих людей | ТОП САМЫХ ЛУЧШИХ | Дзен](https://th.bing.com/th/id/OIP.5UFLQ7n9iHeLCfA_JqZjKAHaIO?w=900&h=1000&rs=1&pid=ImgDetMain)

![Fond d'écran rottweiler gratuit fonds écran chiens rottweiler](https://th.bing.com/th/id/R.12547c9292683a09fee3667a6d60babe?rik=fhgLmoKEahZUYg&riu=http%3a%2f%2fwww.fond-ecran.net%2ffonds%2frottweiler_001.jpg&ehk=lMAbHaYpW47wqlhlmITvjnZFlNlWavmrhyza1CkT4zM%3d&risl=&pid=ImgRaw&r=0)

**橄榄绿**

![小米橄榄绿SU7汽车壁纸1920x1080高清大图_彼岸桌面](https://th.bing.com/th/id/R.48f267d75ff098c661f9d59af89a4e5d?rik=TeLDsRQCNZFhWA&riu=http%3a%2f%2fimg.netbian.com%2ffile%2f2024%2f0115%2f001326cGXSH.jpg&ehk=wEJ4xYSsTJh9sZ%2bvSA3J1RA7nheivzjTil93kMMbqxs%3d&risl=&pid=ImgRaw&r=0)

![小米汽车SU7整车外观实拍高清大图_小米汽车SU7 2024款 Max 双电机全轮驱动橄榄绿第2张图片大全_太平洋汽车](https://img.pcauto.com.cn/images/upload/upc/tx/auto5/2312/28/c25/399342183_1703754845454.jpg)

![小米汽车SU7官方图赏 - Xiaomi 小米 - cnBeta.COM](https://img1.mydrivers.com/img/20231228/38734a62c0ec40f0ba2d2687fe950542.jpg)

### 



**主流机器狗：**

![image-20240527094301001](C:\Users\user1\AppData\Roaming\Typora\typora-user-images\image-20240527094301001.png)





![image-20240527094333821](C:\Users\user1\AppData\Roaming\Typora\typora-user-images\image-20240527094333821.png)





![image-20240527094755073](C:\Users\user1\AppData\Roaming\Typora\typora-user-images\image-20240527094755073.png)





### 1.02 功能

| 功能         | 硬件模块                        | 实现途径           |
| ------------ | ------------------------------- | ------------------ |
| LED控制      | stm32                           | GPIO 控制，TIM时钟 |
| OLED显示     | stm32                           | SPI协议            |
| 蜂鸣器       | stm32                           | 时钟频率           |
| 关节舵机     | ESP32（内部集成WiFi，蓝牙）     | PWM                |
| 光敏传感器   | OLED有一个背光接口，集成一下    | 集成               |
| 温度传感器   | 原理是电压变化+模数转换直接集成 | 集成               |
| 湿度传感器   | 模数转换                        | 集成               |
| 超声波传感器 | stm32                           |                    |
| 激光雷达     |                                 |                    |
| 人脸识别     | 摄像头                          | OpenCV             |
| 充放电功能   | 电源设计                        | 嘉立创             |
| 过热保护     | 温度传感器+断电+奖速，锁频率    |                    |
| 散热功能     | 散热组                          | 集成               |
| 散热风扇     | 风扇                            | 温控+PWM转速       |



## 2.参考资料





## 3.硬件部分

### 3.00.00

转思路，没时间了，直接买模块，直接设计一个直插式模块就好了，除非没有我们想要的的PCB

### 3.01 模块使用

#### 3.01.01 舵机操作

1.控制角度由信号线所决定，并且角度的调节则由脉冲宽度调节（PWM）

2.足运动时的快慢跟舵机的响应速度有很大的关系

3.调试时，舵机的电源线和地线用电源仪器控制，信号线接到stm32;

4.脉冲有一个周期，用定时器实现；

5.PWM使用示波器查看

6.像这种电压，一定要先测量一下电源是否稳定，刚刚电脑连上单片机，直接把电脑干黑屏了

参考链接

[各型号舵机参考代码](https://blog.csdn.net/m0_63235356/article/details/136054702?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171678694516800215035789%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171678694516800215035789&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-136054702-null-null.142^v100^pc_search_result_base6&utm_term=MG995&spm=1018.2226.3001.4187)

[舵机小白入门](https://blog.csdn.net/mantoureganmian/article/details/127592585?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171677903716800178599116%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171677903716800178599116&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-127592585-null-null.142^v100^pc_search_result_base6&utm_term=%E8%88%B5%E6%9C%BA&spm=1018.2226.3001.4187)

#### 3.01.02 光敏传感器的使用

1.集成光敏电阻+0809ADC芯片；

2.想一下同时做过热保护，哪里容易发热；

3.看一下别人做的；

4.在集成到自己的板子上；

5.资料手册里面有参考电路，之后就是测电压，看是否符合文档的合理电压范围；

#### 3.01.03 ESP32与STM32

1.ESP32直接集成有WiFi和蓝牙模块，那么直接用usart通信与stm32相连，这样的话stm32为主，esp32为次；

2.控制主要还是由stm32负责，esp32负责联网传达控制器的信息给主控元件；

### 



#### 3.01.04 最小系统板

##### 3.01.04.01 电源设计

5V转3.3V，参考电路，

USB转TTL







1.STM32，PCB最小系统板设计

### 3.02 模块设计

#### 3.02.01 STM32最小系统板设计

1.看别人的板子，比较主流的芯片

#### 3.02.02 基于电阻设计传感器

#### 3.02.03 摄像头设计+OpenCv

#### 3.02.03 稳压电源设计

#### 3.02.04 舵机扩展板设计

#### 3.02.05 控制器设计

#### 3.02.06 激光雷达

#### 3.02.06 稳压模块

每个舵机加上单独的稳压模块

​																																	

[^202405301623]: 
[^202405301623]: 



## 4.机械结构设计



## 5.资料参考



### 5.01 斯坦福大学开源四足机器人

[学校官网：]: https://pupper.readthedocs.io/en/latest/	"学校"

### 5.02 MIT 迷你豹

## 7.调试过程



### 7.01 STM32F407VET6-2.4G WIFI模块-舵机



![image-20240601143358441](C:\Users\user1\AppData\Roaming\Typora\typora-user-images\image-20240601143358441.png)





