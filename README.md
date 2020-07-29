# smart-home-building-notes
记录一下智能家居改造的过程

* 需求
* 选型
* 方案设计对比
* 方案实施
* 智能场景
* 花费
* 下一步
* FAQ

<br><br>

## 需求
* 最好能够支持Homekit
* 照明
* 窗帘
* 影音
* 空调
* 晾衣架
* 其它设备控制

<br><br>


## 选型
目前国内屋内智能家居领域的厂商众多。这里只关注一些产品易用的品牌和厂商。这类产品的好处是易上手，好配置，开箱即用，无需太多复杂的电路改造。

| 品牌 | 智能家居平台 | 语音助手 | 优点 | 缺点 | 备注 |网址|
| --- | --- | --- | --- | --- | --- | --- |
| 小米 |米家App、Homekit|小爱、Siri|价格相对较低，生态好|没有墙壁开关||
| 绿米（aqara）|米家App、Aqara App、Homekit|小爱、Siri|产品设计较好、有实体体验店|价格相对小米偏高|小米孵化企业，后来单飞，大部分产品与小米互相兼容|[官网](https://www.aqara.com/)|
| 小燕 | 小燕App, Homekit | 小爱、Siri、Alexa、Google Assistant、天猫、小度等 | 没有用过，不做评价 | 没有用过，不做评价 ||[官网](https://www.xiaoyan.io/)|
|欧瑞博|自家App|自家设备|没用过，但看官网的感觉是深耕行业多年，功能强大，产品颜值高。墙壁中控很帅|产品生态封闭，颜值很高但是不够百搭。|知名度在装修界很高|[官网](https://www.orvibo.com/)
|Yeelight|Yeelight App, Homekit, 米家App|小爱、Siri、Alexa、Google Assistant等|灯具色温亮度无极调整，显色度比较好||只做智能灯具产品|[官网](https://www.yeelight.com/)|

最后选用了绿米加yeelight的产品。原因：
* 支持米家和Homekit双平台
* 通过小米的小爱音箱(带红外遥控的)或者万能遥控器可以控制传统电器
* 产品设计较好，比较百搭
* 网络上教程资源比较丰富
* 原来装修的灯带和筒射灯不支持调色温和亮度。而且色温只有3000k，偏黄。

<br><br>

## 方案设计对比
### 智能家居总体架构
![总体架构图](https://github.com/kuang1987/smart-home-building-notes/blob/master/images/arch.png)
### 设备分类
#### 按照功能
|分类|设备|功能|
|---|---|---|
|家庭中枢|小爱音箱<br>HomePod<br>Apple TV<br>iPad<br>等等|主要用于远程控制。有些中枢会集成网关功能，比如小爱音箱pro自带了蓝牙Mesh网关和万能红外遥控功能|
|网关|小米多模网关<br>Aqara网关<br>其它品牌网关|主要是通讯协议转换|
|传感器|人体传感器<br>门窗传感器<br>温湿度传感器<br>烟雾传感器<br>等等|主要感知外界信息|
|控制器|智能灯<br>墙壁开关<br>窗帘电机<br>红外遥控器<br>等等||

#### 按照通信协议
|分类|优势|劣势|
|---|---|---|
|WiFi|便于连接，无需网关|信号受距离和房间结构影响较大|
|Zigbee|物联网主流协议，信号好|需要网关|
|蓝牙Mesh|主要用于智能灯具分组|传输距离短|
|红外/射频|控制传统电器|不能感知状态，只能单向控制|

### 灯光控制
|方案|优势|劣势|
|---|---|---|
|替换原开关为智能墙壁开关|无需换灯，价格相对便宜|开关造型可能与原装修不搭，需要替换原开关|
|更换智能灯具|灯具灵活分组，亮度色温可调|成本较高。成品灯具像吊灯、落地灯、吸顶灯造型较少。智能灯泡只有常规螺口。||


### 窗帘控制
|方案|优势|劣势|
|---|---|---|
|智能窗帘电机|安装简单。支持开关到某个位置，支持手动轻拉后自动开关|价格高、多数电机需要预置插座。锂电池版成本高|
|遥控窗帘点击|成本低|需要预留插座、使用红外/射频控制、难以实现开关某个位置|  

\* Tips： 如果想节省成本，在有主帘和纱帘的情况下，可以只安装一条电动轨道，然后用魔术贴连接主帘和纱帘。

### 传统电器控制
主要通过红外遥控和射频遥控进行控制，无法感知被控制设备的状态。  
\* Tips: 小爱同学pro和小米的万能遥控器本身只支持红外遥控，但可以通过加装射频板或者外界射频发射器实现对射频以及其他遥控的支持。  


### 空调控制
对于常规空调，使用红外遥控。
对于重要空调，aqara和其它品牌有专门的VRF智能控制器，可接入智能家居系统，控制全屋内机。但是价格较贵。

<br><br>

## 方案实施
这里按照房内的区域进行说明

### 全屋
|产品|功能|备注|
|---|---|---|
|小爱音箱pro| <ul><li>米家系智能中枢</li><li>语音助手</li><li>红外、射频遥控器</li></ul>|小爱音箱pro需加射频模块，[教程](https://github.com/kuang1987/smart-home-building-notes/blob/master/subs/%E5%B0%8F%E7%88%B1%E9%9F%B3%E7%AE%B1PRO%E5%B0%84%E9%A2%91%E6%A8%A1%E5%9D%97.md)|
|Apple TV 4k|<ul><li>Homekit中枢</li></ul>|[ATV4k教程](https://github.com/kuang1987/apple-tv-tutorial) 这个之前已经入了，所以就直接用ATV做Homekit中枢。另外可以用HomePod或者iPad作为中枢。如果不需要HomeKit支持，可略过|
|Aqara网关|Zigbee网关|也可购买小米多模网关，小米和Aqara的Zigbee设备大部分互相兼容。小米多模网关目前不支持Aqara B1(锂电池版窗帘电机)|
|Yeelight网关|Wifi和蓝牙Mesh网关|主要用于将yeelight的蓝牙灯具接入homekit和米家app。小爱音箱pro也有蓝牙mesh的功能，但是只可以将yeelight的蓝牙灯具接入米家app|

### 客厅
#### 灯光控制
* 客厅的灯光改造采用的方案是结合开关改造和灯具改造。  

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|双键开关|普通双键开关<br><ul><li>餐厅灯</li><li>入户射灯</li></ul>|Aqara单火双键开关<br><ul><li>餐厅灯</li><li>客厅主灯</li></ul>||
|三键开关|普通三键开关<br><ul><li>客厅主灯</li><li>客厅灯带</li><li>客厅筒/射灯</li></ul>|Yeelight凌动开关<br><ul><li>客厅灯带</li><li>客厅筒/射灯</li><li>入户筒灯</li></ul>|这个开关其实可换可不换。如果使用原来的开关，则始终保持开的状态即可；Yeelight的凌动开关的好处是支持物理“开关”的情况下，保持灯具始终在线|
|客厅灯带|普通灯带|Yeelight泛影灯带|泛影灯带不支持Homekit，后续需要“黑科技”支持|
|入户射灯|西顿射灯|Yeelight M2色温筒灯||
|客厅射灯|西顿射灯*7|<ul><li>Yeelight M2色温筒灯\*4</li><li>Yeelight M2色温射灯\*3</li></ul>|<ul><li>4个筒灯用于电视背景墙和沙发背景墙上方组成灯组</li><li>1个射灯放置于餐边柜上方</li><li>一个放置于钢琴上方</li><li>1个在北次卧和次卫中间的过道处</li></ul>|
|餐边柜灯带|无|小米Zigbee智能插座|灯带通过智能插座直接接入弱电箱的插排|


* 原始装修的灯光布局和开关控制示意图如下  
![客厅原始灯光布局](https://github.com/kuang1987/smart-home-building-notes/blob/master/images/living_room_origin.png)
* 改造后如下  
![客厅改造后灯光布局](https://github.com/kuang1987/smart-home-building-notes/blob/master/images/living_room_new.png)

#### 窗帘控制
|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|窗帘轨道|无|Aqara Zigbee开合帘专用轨道||
|窗帘电机|无|Aqara Zigbee窗帘电机|根据邻居的建议，从弱电箱插座经过餐边柜顶部检修口沿客厅吊顶引了一路电|

#### 影音控制
|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|投影仪|红外遥控器|米家APP控制||
|投影幕布|433射频遥控器|米家APP控制|需通过小爱音箱射频模块学习|
|回音壁|红外遥控器|米家APP控制||

### 主卧
主卧目前只改造了窗帘。某天碰到小米有品B1电机优惠，咬牙拿下。  

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|窗帘轨道|无|Aqara B1窗帘轨道||
|窗帘电机|无|Aqara B1锂电版电机|支持Aqara的魔方控制器旋转控制开合度|
|窗帘控制|无|Aqara 魔方控制器|摇一摇窗帘全开；旋转控制关闭|

### 主卫
原装修中主卫一共有两个筒灯，两条灯带，以及一个冷暖风机，使用一个四键开关控制。

<p float="left">
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/restroom/switch.jpg" width="200"/>
</p>

（原谅我见识少，没见过如此高端的设计）

主卫的改造方案是保持原开关不动，将筒灯和灯带更换为智能灯，并使用门窗传感器和人体传感器实现人来开灯，人走灯灭。

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|四键开关|||不对开关做改造。需要保持“总开”和“风机关”状态。|
|射灯|西顿射灯|Yeelight筒灯||
|灯带|普通灯带|Yeelight泛影灯带||
|开门感应|无|Aqara门窗传感器||
|人体感应|无|Aqara人体传感器\*2|进门处和浴缸角上|

土豪可选设备
[Yeelight智能浴霸](https://item.taobao.com/item.htm?id=598800994949&ali_refid=a3_430582_1006:1164600006:N:OhaGUK3q6w3cdSmtmM63%2B72Ozm4nW%2FMy:2044d30204d6e9d09d6fd324655eb333&ali_trackid=1_2044d30204d6e9d09d6fd324655eb333&spm=a230r.1.14.1#detail)

### 次卫
思路基本和主卫一致。  

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|四键开关|||不对开关做改造。需要保持“总开”和“风机关”状态。|
|干区射灯|西顿射灯|Yeelight筒灯||
|干区灯带|普通灯带|Yeelight泛影灯带||
|干区人体感应|无|Aqara人体传感器||
|湿区射灯|西顿射灯|Yeelight筒灯||
|湿区开门感应|无|Aqara门窗传感器||
|湿区人体感应|无|Aqara人体传感器\*2|进门出和淋浴房内。注意人体传感器无法透过玻璃等介质感应|

土豪可选设备
[Yeelight智能浴霸](https://item.taobao.com/item.htm?id=598800994949&ali_refid=a3_430582_1006:1164600006:N:OhaGUK3q6w3cdSmtmM63%2B72Ozm4nW%2FMy:2044d30204d6e9d09d6fd324655eb333&ali_trackid=1_2044d30204d6e9d09d6fd324655eb333&spm=a230r.1.14.1#detail)

### 厨房
替换原有单键开关为智能开关，并结合人体传感器实现人来开灯，人走灯灭  

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|单键开关|普通单键开关|Aqara单火单键||
|人体感应|无|Aqara人体传感器|橱柜吊柜下角|

### 工作阳台
替换原有单键开关为智能开关，并结合人体传感器实现人来开灯，人走灯灭  

|项目|改造前|改造后|备注|
|---|----------|-----------|---|
|单键开关|普通单键开关|Aqara单火单键||
|人体感应|无|Aqara人体传感器|墙角|

<br><br>

## 智能场景
### 添加设备
这里先大致介绍一下在米家APP中添加设备的流程。

* 下载米家app，注册小米账号并登陆
* 下载小爱音箱app，并绑定小米账号。然后小爱音箱将会作为一个设备出现在米家app中
* 添加Aqara网关。在米家app中点击右上角按钮，搜索Aqara网关，点击后根据提示进行操作。
* 添加米家和绿米支持的设备。在米家app中点击右上角按钮，搜索Aqara网关，点击后根据提示进行操作。
* 下载yeelight app。绑定小米账号。
* 在yeelight app中添加yeelight网关。点击右上角按钮，选择Mesh网关，根据提示进行操作。
* 在yeelight app中添加yeelight设备。点击右上角按钮，选择要添加的设备，根据提示进行操作。
* 在yeelight中添加的设备将自动出现在米家app中
* 将设备重新命名，然后规划房间
* 对于智能灯带和智能筒射灯，可以通过添加灯组实现统一控制。

<p float="left">
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/1.jpg" width="200" height="400" />
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/2.jpg" width="200" height="400" />
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/3.jpg" width="200" height="400" />
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/4.jpg" width="200" height="400" />
</p>
<p float="left">
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/5.jpg" width="200" height="400" />
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/6.jpg" width="200" height="400" />
<img src="https://github.com/kuang1987/smart-home-building-notes/blob/master/images/devices/7.jpg" width="200" height="400" />
</p>

### 添加场景
米家app里添加智能场景也相对较为简单。玩法众多，这个全靠自己发挥想象力摸索。大致分为几类：
* 手动触发。设置手动触发并给该场景命名后，可以使用该名字通过小爱同学进行控制。同时，ios中的米家app也支持给智能场景增加siri的shortcut，设置后可以使用siri进行控制。
* 传感器触发。温湿度传感器，人体传感器，门窗传感器等都可以作为触发设备。比如实现人来开灯，人走灯灭等。
* 定时触发。

### 我目前的一些场景举例
|场景|类型|动作|
|---|---|---|
|会客模式|手动触发|客厅筒射灯及灯带全部开启并调至最大亮度、白光色温|
|餐厅模式|手动触发|开启餐边柜灯带、餐厅射灯、餐厅灯，关闭其它灯|
|睡觉模式|手动触发|开启入户射灯，关闭其他所有灯|
|电影模式|手动触发|降下幕布、打开投影仪和音箱、关闭客厅窗帘、将客厅灯调至最暗、色温黄光|
|主卫灯光|传感器触发|开门亮灯，人体传感器感应到移动亮灯，人体传感器2分钟内没有感应到移动灭灯|
|主卧窗帘|传感器触发|魔方控制器摇一摇窗帘全开；旋转控制关闭|


<br><br>

## 花费
![缩略图](https://github.com/kuang1987/smart-home-building-notes/blob/master/images/expense.png)

[花费excel](https://github.com/kuang1987/smart-home-building-notes/blob/master/subs/expense.xlsx)


<br><br>

## 下一步
* 升级黑群晖到DSM6.2，安装docker，跑homebridge，将更多的设备接入到homekit。
* 卧室的窗帘轨道已全部预留为电动轨道。待双十一申请预算后下手。
* 卧室的灯光控制方案只需将开关替换为智能开关即可。
* 空调智能接入。方便后续远程控制。

<br><br>

## FAQ
1. 墙壁开关如何改色？
去建材市场的开关店询问；如果是Aqara产品可在Aqara实体店改色，费用为50一个。

2. 为什么选择换掉客厅灯而不是只改开关？
最近比较流行“无主灯”设计，刚好开发商装修留的灯带和筒灯位置相对比较合理，个人觉得平时确实不需要开很多灯，用不同的灯光营造不同的氛围，可以使人更加“专注”；不是特别喜欢原来灯的色温（3000k）；客厅主灯和餐厅灯为了装饰效果还是买了，但是都是亮度色温可以调整的，可以通过遥控器接入智能。

TBD。。。
