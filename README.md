# API_ML_AI

# 产品需求文档

发布日期 | 2018/12/29
---|---
Epic | 卡路里助手
文件现状|完成
文件主人 |孙思盼
领头设计者 |孙思盼
领头开发者 |孙思盼
领头测试者|孙思盼


####  Goals: 目标
目标用户通过拍摄图片获取食物的相关卡路里和营养信息。

# 第一部分：需求概述
#### 1.背景概述
&emsp;&emsp;近几年，出现大量智能手机app为核心的减肥应用都有食物追踪功能，研究发现，目前市面上存在的该类型app，用户需要记录该食物是哪一天吃的，哪一餐吃的，吃的是什么食物，吃了多少。繁琐的操作使得用户需要花费一定的时间去对每天摄入的食物进行记录，久而久之会选择放弃。


#### 2.产品介绍-价值宣言
卡路里助手用户通过智能手机拍摄食物图片上传，系统通过深度学习的算法，结合视觉分析和图像识别技术，反馈给用户相关的食物信息，包括热量和具体的营养成分，从而做到为用户分析日常饮食的健康指标。


####  3.产品核心价值（最小可用产品）-用户痛点

想要通过记录每天饮食摄入数据来控制体重的人群，以往食物追踪设备中繁琐的输入操作，花费了他们一定的时间，他们迫切希望有类似功能但更为便捷的产品。

比如：（场景）30分钟的用餐时间，用户需要花时间在记录饮食上，耗时耗力并且产生的结果仅仅只是参考的作用。

#### 4.产品使用场景
&emsp;&emsp;在任何场合，可以快速通过拍摄图片来获取食物的相关卡路里和营养信息，不需要繁琐的输入操作。


用户（想要保持身材） | 场景需求| 重要程度
---|---|---
职场女性 |吃饭时间，快速记录当天食物的信息| 重要
在校大学生|建立完整的饮食档案，避免繁琐的输入| 重要
家庭妇女|繁杂的家务结束后，享用吃饭时间，同时想记录自己的饮食记录| 重要


#### 5.这如何和我的产品整体策略发生关联？
&emsp;&emsp;产品的目标策略提出，目的是为了解决繁琐的输入操作，为用户带来全新的操作体验。同时产品以小程序的形式进行设定，也是基于目前市面上大量同质化app占据了一定的市场比例，但是能在这场战役中真正脱颖而出的app却少之又少，因此小程序的推广可能能更好的让用户产生愿意尝试一下的心理。



# 第二部分 产品规划
#### 1.假设（Assumptions:） 

1. 用户拍摄图片，主要是在使用移动智能手机的情境下；
2. 图片中食物的卡路里获取调用有关的食物卡路里api；
3. 技术：深度学习的算法，结合视觉分析和图像识别；
4. 需要依靠有强大的数据库来判断获取食物的热量信息。

#### 2.需求 requirements:

|#| title| 用户案例 |重要程度|笔记 |
| ------ | ------ | ------ |------ |------ |
|# | 卡路里识别功能|  用户给食物拍照，系统自动计算热量|重要：免去了繁琐的输入| 获取照片、食物与标定物的检测、以及体积与卡路里估算|


#### 3.预期输入-输出：
问题（question）| 结果（outcome）
---|---
 输入食物照片|输出食物相关的热量和营养含量|
 
#### 4.API测试-图片输入输出/可行性分析
#####  4.1API:[百度菜品识别API](https://cloud.baidu.com/product/imagerecognition/fine_grained)


案例1：
- 输入：牛肉河粉
- 输出：牛肉粉，置信度为0.866，每100g热量含量
- 判断：正确
- 检测时间：约3秒
![]![](https://github.com/sunsipan/API_ML_AI/blob/master/images/2.png)

案例2
- 输入：多种食物
- 输出：非菜
- 判断：无法识别
- 时间：小于2秒
![image]![](https://github.com/sunsipan/API_ML_AI/blob/master/images/1.png)

#####  4.2API:[调用百度菜品API代码测试](https://cloud.baidu.com/doc/IMAGERECOGNITION/ImageClassify-API.html#.E8.AF.B7.E6.B1.82.E8.AF.B4.E6.98.8E)
##### 代码测试（第一次）
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/python.jpg)
结果：代码测试，出现了110错误，accent token无效；目前还没有解决。

##### [代码测试（第二次）](https://github.com/sunsipan/API_ML_AI/blob/master/API-test.ipynb)
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/API-test.JPG)
结果：通过调用百度AI中的菜品识别，读出在本地端食物图片的相关信息。

#####  4.3API:[阿里云图像识别](https://data.aliyun.com/ai?spm=5176.12127922.1238513.3.30306c06Elegza#/image-tag)
- 输入：牛肉河粉
- 输出：图像标签
- 判断：#
- 检测时间：约3秒


![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/aliyun-1.JPG)


#### API使用比较：
- 百度菜品API，只能识别单一的菜色，对于多食物的照片无法识别；提供食物的热量信息，并且提供每100g该食物的热量。
- 阿里云图像识别API，目前还没有提供关于食物识别热量的API,输入的图片只反馈图片的相关标签。
- 两个平台的API都没有提供食物的体积估算。
- 总结：基于百度菜品识别API的功能下，需要寻找如何解决能处理多菜色的图片，以及食物体积估算的技术。

#### API使用风险报告
1. 目前国内食物热量相关的API在自己能查询的条件下，除了公开的百度菜品API可以实现食物热量测算外，其他平台的API都不能提供相关的热量测算，比如：[爱集合数据-食材大全API](http://www.xjihe.com/service/apiintro/3)
、[万维易源-菜谱大全（食谱）](https://www.showapi.com/api/view/1164/1)、[阿里云图像识别](https://data.aliyun.com/ai?spm=5176.12127922.1238513.3.30306c06Elegza#/image-tag)。
2. **识别单一的菜色**：百度菜品API，用户输入一张带有食物的照片，输出食物的热量信息，并且提供每100g该食物的热量信息；
3. 可替代解决方案：（在无法调用更为庞大的食物库，以及查询到能做到体积估算的API前提下）基于深度学习的目标检测算法-[技术采用Faster R-CNN](https://www.cnblogs.com/dudumiaomiao/p/6560841.html),来标记目标位置和类别，采用[GrabCut图像分割方法](https://blog.csdn.net/wi162yyxq/article/details/61619075)进行体积估算。-[参考资料](https://github.com/sunsipan/API_ML_AI/blob/master/create_pdf.pdf)

![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/卡路里.JPG)



# 第三部分产品设计
#### 下载-[食物卡路里识别功能交互原型](https://sunsipan.github.io/Calorie1/start.html#g=1&p=index)
### 产品信息结构图：
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/%E5%8D%A1%E8%B7%AF%E9%87%8C%E5%8A%A9%E6%89%8B-%E4%BA%A7%E5%93%81%E4%BF%A1%E6%81%AF%E7%BB%93%E6%9E%84%E5%9B%BE.png)

### 产品功能结构图：
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/卡路里助手.png)

### 核心流程图
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/核心流程图.jpg)

### 原型-部分功能说明
##### 1. 弹窗-授权微信登陆

![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/wetchat.png)




##### 2.关于卡路里小程序相关信息
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/about.png)



##### 3.拍照页面-核心
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/核心页面2.png)
![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/核心页面.png)


##### 4.用户分享页面

![image](https://github.com/sunsipan/API_ML_AI/blob/master/images/share.png)







