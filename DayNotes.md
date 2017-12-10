[TOC]

### Daily Notes

##### MIT, Introduction to Linear Algebra

##### Segementing motion capture data...

- [ ] data processing with Data glove 

##### Data Structure And Algorithms

- [ ] open course of ZheJiang University,  PTA, online testing

##### Probability And Statistics

- [ ] 概率论与数理统计，陈希孺

##### Mage Linux 

- [ ] 鸟哥私房菜



##### Short term

- [ ] Pattern Classification weekly report
- [ ] 3Blue1brown's linear algebra






#### 2017-12-05

[How to open a directory/folder and a URL through Terminal](https://askubuntu.com/questions/17062/how-to-open-a-directory-folder-and-a-url-through-terminal)

> // open a directory on Ubuntu
>
> ~$ nautilus  /path/to/that/folder
>
> // to open URL
>
> ~$ google-chrome  https://google.com    

[something with Git sync](https://www.cnblogs.com/yujihang/p/6601984.html)

>将仓库中的改动同步到本地, 在git-bash中进入项目目录下, 使用git pull命令





#### 2017-05-22

这中间一个月真是坑自己，二建笑话。

外刊发现最后被坑100块。


#### 2017-04-27

- [x] 整理恶魔奶爸的 live 《如何说一口流利的英语》



#### 2017-04-25

##### MIT, Introduction to Linear Algebra

- [ ] Chapter X

##### Segementing motion capture data...

- [x] data processing with demo
- [ ] data processing with Data glove 

##### Data Structure And Algorithms

- [ ] open course of ZheJiang University,  PTA, online testing
- [x] **Prepare for the Mid-test**, due to 22th, April

##### Probability And Statistics

- [ ] 概率论与数理统计，陈希孺

##### Mage Linux 

- [ ] 鸟哥私房菜



##### Short term

- [ ] Pattern Classification weekly report
- [ ] 3Blue1brown's linear algebra





#### 2017-04-13

##### MIT, Introduction to Linear Algebra

- [ ] Chapter X

##### Segementing motion capture data...

- [ ] data processing with demo

##### Data Structure And Algorithms

- [ ] open course of ZheJiang University,  PTA, online testing
- [ ] **Prepare for the Mid-test**, due to 22th, April 

##### Probability And Statistics

- [ ] 概率论与数理统计，陈希孺





#### 2017-03-29

1. what is the difference between `string::size_type` and `string::size_t` ?
2. ​



#### 2017-03-29

- [x] 模式识别02-贝叶斯分类器
- [ ] 数据手套的动作分割方法了解、以 Matlab 来做
- [ ] 人机交互最新成果、论文调研





#### 2017-03-23

给 Mac 安装 opencv， 失败，还给弄了好久。

#### 2017-03-20

##### Next Day: 

- [x] GRT 初步。

- [x] ROS-Beginner Level tutorials 继续刷至20

- [x] 模式识别 实验报告

- [x] **论文调研，kinect和数据手套 的结合 做手势识别，或者数据手套结合那个定位手柄**。

      研究内容：1、数据融合算法；2、动作识别；3、基于识别的人机交互；4、系统实验验证

      ​



##### Naive Bayes Algorithms

*朴素贝叶斯法*：

1. **朴素贝叶斯法对 条件概率分布 作了 条件独立性 的假设。**

2. 典型的生成学习方法，属于生成模型，因为其实际上学习到生成数据的机制。

3. 生成方法由训练数据学习联合概率分布$P(X, Y)$, 然后求得后验概率$P(Y|X)$.

   利用训练数据学习 $P(Y|X)$ 和 $P(Y)$ 的估计，得到联合概率分布：$$P(X, Y) = P(Y)P(X|Y)$$

   概率估计方法可以是 极大似然估计 和 贝叶斯估计。



##### 找方博和孙老师多交流

多向人请教

##### 组会开完、查资料

人工智能 发展现状 高校所做的成果

计算机视觉

智能医疗

物联网

自动驾驶与智能交通

机器人、类脑计算达到世界前沿水平

自然语言处理

AR、 VR

智能交互





#### 2017-03-19

##### Next Day: 

- [ ] 数据手套 基础知识

- [x] GRT 平台搭好，先用下，
- [ ] 视觉方面搜搜前沿论文
- [x] ROS-Beginner Level tutorials
- [ ] 模式识别 实验报告




##### 手势识别

静态 还是 动态 ？

​	有做静态的也有动态的，方博之前基于数据手套的也是15种静物的手势识别。

​	动态的偏难些，及时性，有效位置（手势起点与终点）

​	若是工作量足够毕业要求还是以做静态更合适些。

基于 视觉 还是基于 穿戴设备-数据手套 ？

​	数据手套方面实验室能够提供一定的前期基础，毕竟方博是做这个的。

​	视觉方面，实验室倒是也有 Kinect 设备来获取深度图像。只是识别等算法应该蛮难的，方法创新上也会卡。

​	**多刷点论文钻研下 视觉识别 方面的算法及实现**

应用方向 ？

​	结合什么场景，来体现工作量。



#####  Ubuntu

上午尝试在 Ubuntu 上配置 shadowsocks ，可惜最终并未能成功。搜查教程等按部就班操作，所做的操作应该无误。

可能的原因：

1. 因没有清华的校园帐号，只能通过连接实验室配置的 PPTP 类型的 VPN 来上网，不知是否与 shadowsocks 配置造成冲突。
2. 在 shadowsocks-qt5 中 Test Latentce 出现 Error ，时有 接通现象

暂想尝试的解决方案： 

购置带 VPN 穿透功能的路由器来接通实验室 VPN 在其上再来配置 shadowsocks。



更新：Ubuntu 配置 shadowsocks 问题已解决，自己的配置没问题，应该是谷歌抽风。

将办公桌整理好，主机放下面。





