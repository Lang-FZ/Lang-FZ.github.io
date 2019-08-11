---
title: GPUImage3 Camera的一些注意点
layout: post
date: '2019-08-11 16:40:00'
tags: Metal
---

---
#### 第一步图片的滤镜功能学会之后开始研究镜头的拍照部分，在GPUImage3 Camera文件里面看到很多需要注意的点。  
----
   
### **1. Camera 的delegate没加weak，然后delegate继承自class**
![]({{ "/images/post/delegate-weak.png" | absolute_url }})
![]({{ "/images/post/protocol-class.png" | absolute_url }})
### **2. 镜头切换功能还没写，需要在两个地方修改，location的set方法和imageOrientation，下面是实现方式**
![]({{ "/images/post/camera-location.png" | absolute_url }})
![]({{ "/images/post/imageOrientation.png" | absolute_url }})

### **使用的时候只需要**
![]({{ "/images/post/transferLens.png" | absolute_url }})