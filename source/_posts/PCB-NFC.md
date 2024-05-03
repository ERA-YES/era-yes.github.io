---
layout: blog
title: PCB-NFC
date: 2023-07-18 12:47:27 
updated: 2023-12-08 12:58:33
tags:
    - Github
    - 生活
cover: https://cdn.jsdelivr.net/gh/ERA-YES/PicBed@main/PBC-NFC/1.jpg
highlight_shrink: true
recommend: True
---

# 台州路桥中学PCB-NFC校园卡

> ## EraYes制作
>  按照路中地图绘制，忽略部分细节，但保留了大部分代表性建筑，画了nfc线圈，焊接ic卡后基本可实现校园卡全部功能。
>  正面电路都是装饰，无实际作用。背面是nfc线圈和个性化自定义空间
>  工程内提供了空卡、线圈、地图、带注记的地图和我定制的个性化卡供参考
>  无原理，地图就是原理

## 结束BB
前面都是写给别人看的，这里是写给自己人的

最初想改造校卡是半学期前的事了，那时候就买来电烙铁之类的准备动手，再一个星期后我就把自己的校卡拆了，然后就搞坏了。。。

后来这件事就又搁置了一段时间，知道最近在b站上刷到了用PCB板改装校卡的视频，恰好最近又在玩开发板之类的，这种DIY就深深地吸引了我，然后就花了整整两天来画这张地图。

### **说说这张地图的漏洞吧**
> - 我当初画的时候忘记画钟楼了(emm。但后来想到钟楼的占地面积极小，而且板子也不可以凸出来一块，所以就舍弃掉了。
> - 然后就是食堂画小了，因为把新男舍的比例搞错了，而女舍又是直接复制的男舍，所以就挤得食堂没地方了~~
> - 食堂旁边的一排电阻其实是车啦
> - 还有就是操场前，篮球场边，那块一直拆了建、建了拆的地方我也不知道是干什么的，所以没画😑
> - 之所以把名字写在滨海大池塘就是因为就那里最空，并不是相当青蛙😶
> - 别问我科技楼为什么这么丑，以为官方地图更丑🙄

**吐槽一句**，虽然不一定看得出来，但最搞人心态的是大礼堂那块的同心圆和圆扇，最然板子打印出来几乎就看不清了，但我细画了好久，那真的折磨了我好久

**再吐槽一句**，虽然地图上男舍后面是开放的，但我们都知道那怎么回事，所以我特地封上了。

### 关于背面
背面特地预留的所以空间就是个性自定义用的，你当然可以像我一样画，有一个细节是我C++代码的头文件是万能头，那懂得就都懂了。

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    cout<<
    "Hello World!"
    << endl;
    return 0;
}
```
### 终于到货了
我本来一直盯着物流消息，但消息一直显示在珠海揽收，直到突然收到丰巢的消息才知道原理嘉立创最新物流信息是显示在底下的，我还傻傻得一直看顶上。。。。一直以为它在珠海。。。
**嘿嘿，高兴**
![](https://cdn.jsdelivr.net/gh/ERA-YES/PicBed@main/PBC-NFC/2.jpg)


### 焊接
虽然说玩开发板是焊接过ic芯片，但这种芯片确实很难贴的严密，而且我还烫到手了😥，起了个大水泡。

{% link 嘉立创开源链接 , 开源在嘉立创，但好像没过审 , https://oshwhub.com/era-yes/tai-zhou-lu-qiao-zhong-xue-pcb-nfc-xiao-yuan-ka %}

{% link Github开源链接 , 所以我也在Github开源了 , https://github.com/ERA-YES/PCB-NFC %}

{% link 嘉立创在线编辑器] , 好在在线编辑可以看 , https://pro.lceda.cn/editor#id=a84dde7ac0c249679c607b19cff67770 %}

### 修改
焊完后出大BUG了，正面过孔的线没连，飞线也没连上，这几张卡就相当于废了，吓得我连滚带爬去改了板子，现在也不用焊盘了，而是做一个金属化过孔放芯片，这样能大大减小焊接的难度而且也更美观，毕竟凹下去一块总比吐出来一块感觉要好。

![](https://github.com/ERA-YES/-PCB-NFC-/blob/main/%E5%B0%81%E9%9D%A2.png?raw=true)
![](https://github.com/ERA-YES/-PCB-NFC-/blob/main/%E5%9C%B0%E5%9B%BE%E5%8E%9F%E5%9B%BE.jpg?raw=true)
![校徽](https://github.com/ERA-YES/-PCB-NFC-/blob/main/%E6%A0%A1%E5%BE%BD.jpg?raw=true)
