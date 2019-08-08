---
title: GPUImage3 添加Vertex参数
layout: post
date: '2019-08-09 00:45:00'
tags: Metal
---

---
#### 前两个月看了《当一个Android开发玩抖音玩疯了之后》之后，对这几款滤镜非常感兴趣，然后又看到了雷曼同学的《在iOS中使用GLSL实现抖音特效》，越发想把这几款滤镜写到自己demo中，但是我不会写OpenGLES，更不会GLSL，也只是刚开始学习Metal。  

#### 我尝试搞这几个滤镜，结果第一个就卡住了，，，缩放滤镜是针对顶点着色器的，结果我找GPUImage3的Api，发现没找到，，，看别人的demo发现都是片元着色器，这个时候的我也看不懂MSL那些参数是啥意思，作为图形门外汉的我只能开始了漫长的啃MSL过程。。。

#### 看了好久。。。然后终于知道大概语法了，也发现GPUImage3的问题了，，，它压根没提供顶点着色器的缓存对应关系，，，没办法了，只能先看懂GPUImage3怎么给片元着色器提供这个功能的然后再自己添加给编码器提供顶点着色器缓存的功能了。经过一顿乱找，一两天过去了，我也终于看懂大概了，下面是最终实现方法。
------
### **下面是给GPUImage3增加的 渲染过程给编码器添加顶点着色器参数缓存功能的实现:**
   
**1. BasicOperation 加属性 vertexUniformSettings**

![]({{ "/images/post/1-BasicOperation加属性.png" | absolute_url }})


**2. 在获取参数表的方法里添加vertex相关 这里可以看到 GPUImage3 片元着色器的参数是规定为struct的**

![]({{ "/images/post/2-获取参数表方法.png" | absolute_url }})


**3. 创建给编码器添加vertex参数缓存区的方法  position 0  texturecoord 1  新参数就默认 index=2 了**

![]({{ "/images/post/3-编码器设置缓存区.png" | absolute_url }})


**4. 在编码过程方法里添加vertex 参数缓存**

![]({{ "/images/post/4-编码过程调用设置缓存区方法.png" | absolute_url }})


**5. 在滤镜链添加的过程里将vertex参数缓存区对应创建好**

![]({{ "/images/post/5-滤镜链添加过程里传递顶点缓存表.png" | absolute_url }})

   
### **实现之后的使用方法:**

**1. 滤镜类**

![]({{ "/images/post/6-滤镜类.png" | absolute_url }})


**2. 滤镜着色器**

![]({{ "/images/post/7-滤镜着色器.png" | absolute_url }})


**3. 实例化滤镜**

![]({{ "/images/post/8-初始化滤镜.png" | absolute_url }})