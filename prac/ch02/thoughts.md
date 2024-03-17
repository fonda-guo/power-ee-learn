# PWM modulation

## date 3-16

H桥中PWM的特性：

基于经典全桥结构的调制方法，有**Bipolar（双极性）、unipolar（单极性）、Hybrid（混合）**，各有利弊，但是都是对SPWM的权衡与利用，对于如下经典H桥结构：

![image-20240316220410779](E:\document\learn ee\ch02\pics\image-20240316220410779.png)

唯一的硬性限制就是$S_1(S_4)$和$S_2(S_3)$不能同时闭合（短路），软性限制为$S_1(S_4)$和$S_2(S_3)$不要同时断开（此时A点无电压，系统断路，在上图所示的结构下，暂时没发现这种做法的意义），其余开关特性往往依赖于调节方法。

针对H桥的前半部分为调制，后半部分为滤波。针对前半部分而言，其输出为AB两点间的电压，即$U_{AB}$，也是H桥部分最应该关心的部分。根据上述软性限制可知，通过描述$S_1 \& S_3$的开关状态即可得到$U_{AB}$。

换言之，采用SPWM对$S_1$进行调制的过程中，通过对PWM的分析即可知$U_{AB}$状态。更近一步的，可以用$SPWM_{s_1} - SPWM_{s_2}$来表述$U_{AB}$对输入电压的三种状态-1，0，1。

对于**Bipolar**的SPWM之差，显然可以表示为$SPWM_{s_1} - \overline{SPWM_{s_1}}$（互补开关），那么对于SPWM而言，1不变，0变-1；

对于**Unipolar**而言，就很有意思，$S_1 \& S_3$由对称的一组sin波产生的，原波形和做差之后的波形如下。

![image-20240316225501548](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240316225501548.png)



![image-20240316230249519](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240316230249519.png)

![image-20240316230315921](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240316230315921.png)

第一减第二得到第三，有零。如果有中心对称假设（SPWM为1的时刻是关于三角波下顶点对称的,需要满足一定的频率假设），那么对于$U_{AB}$而言，如果$SPWM_{s_1}$的占空比为$D_{s_1}$，则输出为$2D_{s_1}-1$，下面这个频率极端一点的情况，就不太对劲，与周期的最小公倍数有关。

![image-20240316233601883](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240316233601883.png)

![image-20240316233722693](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240316233722693.png)

对于**Hybrid**而言，相当于$SPWM_{s_1}$的一半周期减下来（-1），但是这样效果并不好：

![image-20240317135248092](C:\Users\13991\AppData\Roaming\Typora\typora-user-images\image-20240317135248092.png)

由此可有两种变体但是都是需要将三角波作为[0,1]再对称到[-1,0]的操作，原因有待细究，感觉跟反向能量中和有关系。

## Date 3-17

新的拓扑，HMA
