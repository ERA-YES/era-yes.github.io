---
layout: blog
title: vlfii
date: 2023-07-18 13:23:17 
updated: 2023-12-08 12:58:33
tags:
    - Python
    - Github
categories: Python
cover: https://pic.imgdb.cn/item/64bf58e81ddac507cc90f555.webp
recommend: True
---
# Vlfii

### 玩小鸟飞飞F700随手写的
### 图形化用起来太难受了
### 幸好他们的源码是xml，那我就能霍霍啦

{% link Vlfii , Github开源链接 , https://github.com/ERA-YES/Vlfii%}

小鸟飞飞图形化编程的文本编程，针对于小鸟飞飞图形化编程群控软件，采用python构建，可直接引用为库运行，目前已实现大部分常用函数，正在更新中

### 使用注意
建议将库文件与源代码文件放在同一目录下

使用前设置无人机列表、文件名、音乐名等:
```python
from vlfii import *
import vlfii

#默认ip从"192.168.31.101"递增，传入第三参数以调整
vlfii.DRONE = [
    [x1, y1, ["192.169.31.109"]],
    [x2, y2],
    [x3, y3],
    [x4, y4],
    [x5, y5],
]
vlfii.FILE = "output"
vlfii.TEST = False

music("好听的音乐")
```
所有代码写完后:
```python
save()
```
最后运行程序，在程序同一目录下就会生成"output.vlfii"

**注意，在使用群控软件打开后，需要一次点击飞机以让程序生成文本代码，否则将会报错**

**我之所以没实现这部分的逻辑就是因为没有这些代码程序能照常打开，而且软件能自动生成**

### 下表为图形化代码块与函数的对于关系
|代码块|函数|参数|说明|返回值|
|---|---|---|---|---|
|开始|start|-|-|-|
|Start at|StartTime|time = "00:00", color = "#cccccc"|-|-|
|结束Start at代码块|End|-|-|-|
|延时|Delay|time = 1000|-|-|
|解锁|Unlock|-|-|-|
|上锁|Lock|-|-|-|
|水平速度 水平加速度|Horizontal|hSpeed = 100, hAcc = 100|-|-|
|垂直速度 垂直加速度|Vertical|vSpeed = 100, vAcc = 100|-|-|
|角速度|AngularVelocity|w|-|-|
|起飞  cm|TakeOff|alt = 120|-|-|
|降落|Land|-|-|-|
|直线移至|MoveToCoord|x, y, z = 120|-|-|
|X, Y, Z方向移动|RelativePosition|x, y, z|-|-|
|飞机灯光变为|LedAllOn|color="#ffffff"|-|-|
|熄灭飞机灯光|LedAllOff|-|-|-|
|飞机在delay毫秒内逐渐变为color，亮度为bright，然后dur毫秒内变暗|LedAllBreath|color, delay = 1000, dur = 1000, bright = 1|-|-|
|机身在delay毫秒内逐渐变为color，亮度为bright，然后dur毫秒内变暗|LedBodyBreath|color, delay = 1000, dur = 1000, bright = 1|-|-|
|机身灯光先变为color，亮度为bright，持续dur,再关闭delay|LedBodyBlink|color, dur, delay, bright|-|-|
|机身灯光变为|LedBodyOn|color="#ffffff"|-|-|
|直线移至，飞机灯光变为|WaypointRGB|x, y, z, color|-|-|
|四个机臂灯光变为color1, color2, color3, color4, 然后灯光True/False时针方向旋转，转一圈时间为delay|LedDroneArmHorse|color1, color2, color3, color4, clock, delay|-|-|
|四个机臂同亮脉冲color1, color2, color3, color4，频率frequency|LedDroneArmPulse|color1, color2, color3, color4, frequency|-|-|
|结束一架飞机并转向下一架|finish|-|-|-|

### 新增功能
|函数|参数|说明|返回值|
|---|---|---|---|
|Start|-|`start`的别名，用于转换|-|
|Arm|-|`Unlock`的别名，用于转换
|Takeoff|-|`TakeOff`的别名，用于转换|-|
|Move|-|`Move`的别名，用于转换|-|
|MoveToCoord_AutoDelay|x, y, z = 120, time = 0|传入目标坐标，增减时间|[时间, 距离]|
|Move_Circle|x, y, z = 120, n = 8, r = 100, time = 0|飞圆心为传入坐标的n个点的半径为r的圆|int tot 总时间|
|Move_CircleFind|A, B, z = 120, n = 16, dir = 1, time = 0|直接从B点开始飞圆心为A点的圆|int tot 总时间|
|Circle|n, r, dir = 1|返回一个被n均分的圆|list c|
|Circle_FindPoint|A, B, n, dir = 1|返回圆心A点，经过B点的圆|list p|
|music|name|设定代码的音乐，接受文件名|-|
|Time|-|计算以返回当前时间|str "MM:SS"|

**函数介绍较简单，更多请在代码里查看**

### 转换器
**VlfiiConverter**
> 复制`小鸟飞飞图形化编程群控软件`右侧生成的文本源代码，运行`VlfiiConverter.py`，程序将会直接输出转换后的python程序，此程序在引用本Vlfii库是，可以直接运行并生成代码。
- 在安装`pyperclip`库后程序将直接将转换后的代码粘贴入剪贴板

命令行运行此程序以安装`pyperclip`库
```
pip install pyperclip
```

**!注意，生成的代码在`from Vlfii import *`时才有效**

### 库内部变量
|变量名|属性|值|功能|
|---|---|---|---|
|__STATEMENT|私有值|-|表示当前状态|
|__FATHER|私有值|-|表示父标签|
|__WEB_XML|私有值|-|表示WebXml标签|
|__XML|私有值|-|表示Xml标签|
|__DRONE_NUM|私有值|-|当前代码框的无人机编号|
|__hSpeed|私有值|-|记录当前无人机的水平速度|
|__hAcc|私有值|-|记录当前无人机的水平加速度|
|TIME|公共|整型|记录当前时间|
|FILE|公共|字符串|输出文件名|
|POS|公共|列表|飞机当前坐标|
|DRONE|公共|列表|无人机列表|
|TEST|公共|布尔值|调试模式开关，开启时生成文件不可用|
|blue|公共|"#33ccff"|蓝色|
|yellow|公共|"#ffff00"|黄色|
|orange|公共|"#ff6600"|橙色|
|grey|公共|"#c0c0c0"|灰色|


#### 源码，想看就看吧，写的比较屎，之后会重构的
#### 太长了，还是上Github看吧

```python
import xml.etree.ElementTree as ET
import xml.dom.minidom as minidom
import math

__STATEMENT = None
__FATHER = None
__WEBXML = None
__XML = None
__DRONE_NUM = 0
__hSpeed = 0
__hAcc = 0
FILE = "output"
POS = [0, 0, 0]
DRONE = []
TEST = False


blue = "#33ccff"
yellow = "#ffff00"
orange = "#ff6600"
grey = "#c0c0c0"

root = ET.Element("FiiConfig", {"xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
                                "xmlns:xsd": "http://www.w3.org/2001/XMLSchema"})

FlightType = ET.SubElement(root, "FlightType")
FlightType.text = "F700"

CommunicationMode = ET.SubElement(root, "CommunicationMode")
CommunicationMode.text = "Qr"

ComName = ET.SubElement(root, "ComName")

MapInfo = ET.SubElement(root, "MapInfo")
Width = ET.SubElement(MapInfo, "Width")
Width.text = "400"
Height = ET.SubElement(MapInfo, "Height")
Height.text = "400"

MusicInfo = ET.SubElement(root, "MusicInfo")
Name = ET.SubElement(MusicInfo, "Name")
Format = ET.SubElement(MusicInfo, "Format")
Format.text = "mp3"

Flights = ET.SubElement(root, "Flights")

def music(name):
    Name.text = name

def start():
    global __FATHER, __XML, __WEBXML, DRONE, POS
    i = __DRONE_NUM
    FlightView = ET.SubElement(Flights, "FlightView")
    Ip = ET.SubElement(FlightView, "Ip")
    Ip.text = "192.168.31.10{}".format(i+1)
    InitPos = ET.SubElement(FlightView, "InitPos")
    X = ET.SubElement(InitPos, "X")
    X.text = str(DRONE[i][0])
    Y = ET.SubElement(InitPos, "Y")
    Y.text = str(DRONE[i][1])
    POS = [*DRONE[i], 0]
    Code = ET.SubElement(FlightView, "Code")
    __WEBXML = ET.SubElement(FlightView, "WebXml")
    __XML = ET.SubElement(__WEBXML, "xml", {"xmlns":"https://developers.google.com/blockly/xml"})
    block = ET.SubElement(__XML, "block", {"type":"Goertek_Start", "x":"300", "y":"100"})
    __FATHER = block
Start = start

def _next():
    global __FATHER
    next = ET.SubElement(__FATHER, "next")
    __FATHER = next

def _type(t):
    return {"type":"Goertek_"+t}

def _name(n):
    return {"name":n}

def _field(b, n, t):
    field = ET.SubElement(b, "field", _name(n))
    field.text = str(t)

def _block(n):
    global __FATHER
    if __FATHER.tag != "next" and __FATHER.tag != "statement":
        _next()
    b = ET.SubElement(__FATHER, "block", _type(n))
    __FATHER = b
    return b

def StartTime(time = "00:00", color = "#cccccc"):
    global __FATHER, __STATEMENT
    b = _block("StartTime")
    _field(b, "time", time)
    _field(b, "color", color)
    statement = ET.SubElement(b, "statement", _name("functionIntit"))
    __STATEMENT = b
    __FATHER = statement

def End():
    global __FATHER
    next = ET.SubElement(__STATEMENT, "next")
    __FATHER = next

def UnLock():
    '''
    解锁
    '''
    global __FATHER
    b = ET.SubElement(__FATHER, "block", _type("UnLock"))
    __FATHER = b
Arm = UnLock

def Lock():
    _block("Lock")
Disarm = Lock

def Delay(time = 1000):
    b = _block("Delay")
    _field(b, "delay", 0)
    _field(b, "time", time)

def Horizontal(hSpeed = 100, hAcc = 100):
    '''
    水平
    '''
    global __hAcc, __hSpeed
    b = _block("Horizontal")
    _field(b, "hSpeed", hSpeed)
    _field(b, "hAcc", hAcc)
    __hSpeed = hSpeed
    __hAcc = hAcc

def Vertical(vSpeed = 100, vAcc = 100):
    b = _block("Vertical")
    _field(b, "vSpeed", vSpeed)
    _field(b, "vAcc", vAcc)

def AngularVelocity(w):
    b = _block("AngularVelocity")
    _field(b, "w", w)

def TakeOff(alt=120):
    global POS
    b = _block("TakeOff")
    _field(b, "alt", alt)
    POS[2] = alt
Takeoff = TakeOff

def Land():
    b = _block("Land")

def RelativePosition(x, y, z):
    global POS
    b = _block("Move")
    _field(b, "X", x)
    _field(b, "Y", y)
    _field(b, "Z", z)
    POS[0] += x
    POS[1] += y
    POS[2] += z

def MoveToCoord(x, y, z = 120):
    global POS
    b = _block("MoveToCoord")
    _field(b, "X", x)
    _field(b, "Y", y)
    _field(b, "Z", z)
    POS = [x, y, z]
Move = MoveToCoord

def MoveToCoord_AutoDelay(x, y, z = 120, time = 0):
    global POS
    b = _block("MoveToCoord")
    _field(b, "X", x)
    _field(b, "Y", y)
    _field(b, "Z", z)
    v = __hSpeed
    a = __hAcc
    d = math.sqrt((x - POS[0])**2 + (y - POS[1])**2 + (z - POS[2])**2)
    t = v / a
    D = (v**2) / (2 * a)
    if d > 2 * D:
        T = 2 * t + (d - 2 * D) / v
    else:
        T = 2 * math.sqrt(d / a)
    T = round(T * 1000)
    d = round(d)
    T = T + time
    Delay(T)
    POS = [x, y, z]
    return T, d

def Circle(n, r, dir = 1):
    c = []
    angle = dir * 2 * math.pi / n
    for i in range(n):
        theta = i * angle
        p = []
        p.append(round(r * math.cos(theta)))
        p.append(round(r * math.sin(theta)))
        c.append(p)
    c.append([r, 0])
    return c

def Move_Circle(x, y, z = 120, n = 8, r = 100, d = 1400, dir = 1):
    '''
    dir: 1 or -1
    '''
    for [dx, dy] in Circle(n, r, dir):
        MoveToCoord(x + dx, y + dy, z)
        Delay(d)

def Move_Circle_AutoDelay(x, y, z = 120, n = 8, r = 100, dir = 1, time = 0):
    tot = 0
    for [dx, dy] in Circle(n, r, dir):
        tot += MoveToCoord_AutoDelay(x + dx, y + dy, z, time)[0]
    return tot

def LedAllOn(color="#ffffff"):
    b = _block("LedAllOn")
    _field(b, "color", color)

def WaypointRGB(x, y, z, color):
    MoveToCoord(x, y, z)
    LedAllOn(color)

def LedAllOff():
    _block("LedAllOff")

def LedBodyOn(color="#ffffff"):
    b = _block("LedBodyOn")
    _field(b, "color", color)

def LedAllBreath(color, delay = 1000, dur = 1000, bright = 1):
    b = _block("LedAllBreath")
    _field(b, "dur", dur)
    _field(b, "color", color)
    _field(b, "bright", bright)
    _field(b, "delay", delay)

def LedBodyBreath(color, delay = 1000, dur = 1000, bright = 1):
    b = _block("LedBodyBreath")
    _field(b, "dur", dur)
    _field(b, "color", color)
    _field(b, "bright", bright)
    _field(b, "delay", delay)

def LedBodyBlink(color, dur, delay, bright):
    b = _block("LedBodyBlink")
    _field(b, "color", color)
    _field(b, "birght", bright)
    _field(b, "dur", dur)
    _field(b, "delay", delay)

def LedDroneArmHorse(color1, color2, color3, color4, clock, delay):
    b = _block("LedDroneArmHorse")
    _field(b, "color1", color1)
    _field(b, "color2", color2)
    _field(b, "color3", color3)
    _field(b, "color4", color4)
    _field(b, "clock", clock)
    _field(b, "delay", delay)

def LedDroneArmPulse(color1, color2, color3, color4, frequency):
    b = _block("LedDroneArmPulse")
    _field(b, "color1", color1)
    _field(b, "color2", color2)
    _field(b, "color3", color3)
    _field(b, "color4", color4)
    _field(b, "frequency", frequency)

def finish():
    global __DRONE_NUM
    if not TEST:
        str_xml = str(ET.tostring(__XML, encoding='utf-8', method="xml"))
        __WEBXML.clear()
        __WEBXML.text = str_xml[2: (len(str_xml) - 1)]
    __DRONE_NUM += 1

def save():
    rough_str = ET.tostring(root, encoding='utf-8', xml_declaration=True)
    reparsed = minidom.parseString(rough_str)
    new_str = reparsed.toprettyxml(indent='  ')
    f = open('{}.vlfii'.format(FILE), 'w', encoding='utf-8')
    f.write(new_str)
    f.close()

if __name__ == "__main__":
    DRONE = [
        [160, 160],
        [1, 1],
        [2, 2],
        [3, 3]
    ]
    start()
    StartTime()
    UnLock()
    Delay()
    Horizontal()
    Vertical()
    TakeOff()
    MoveToCoord(260, 160)
    Delay(2000)
    Land()
    Delay(2500)
    End()
    StartTime()
    LedBodyOn()
    LedAllOn()
    Lock()
    finish()
```
