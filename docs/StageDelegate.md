理解egret的舞台
==========================
egret的舞台类Stage是一个显示对象，是游戏最根层的容器，其主要的属性通过StageDelegate进行设置。

egret的坐标系
--------------------------
egret和flash一样，采用左上角作为世界坐标系（0,0)点


egret的屏幕适配策略
------------------------

egret有非常简单易懂的屏幕适配策略，核心三个关键词为**游戏尺寸，坐标系尺寸，适配策略**
### egret的游戏尺寸
egret通过 stageDelegate.setFrameSize( clientWidth , clientHeight ) 来指定游戏尺寸。
在移动设备中，这个值是移动设备的屏幕像素分辨率。
**在不同的移动设备中，此值是不一样的。**

### egret的坐标系尺寸
egret通过 stageDelegate.setDesignSize ( designWidth , designHeight ) 来指定游戏的坐标系大小。
egret建议开发者将此值设置为 480 * 800。
**在不同的设备中，此值是恒定的。**

### egret的适配策略
当 FrameSize 和 DesignSize成等比关系时（例如 FrameSize为 720 * 1200，DesignSize为 480 * 800 ），游戏会进行整体缩放。
但是当FrameSize的宽高比和DesignSize的宽高比不一致时，如果整体缩放，会导致游戏由于 scaleX / scaleY 不一致导致显示失真，为了解决这个问题，egret引入了适配策略的概念。

egret默认支持两种适配策略，分别是 FIX\_WIDTH 和 FIX\_HEIHT

当开发者选择 FIX\_WIDTH策略时，egret会把计算 FrameSize.width / DesignSize.width ， 然后在高度上同样乘以这个比率，使得游戏继续保持等比缩放。这样会导致以下问题
* 当 FrameSize宽高比小于DesignSize宽高比时，部分内容会无法显示
* 当 FrameSize宽高比大于DesignSize宽高比时，游戏边界外部内容会显示出来

为了解决上述两个问题，egret要求开发人员要尽量避免使用绝对坐标进行游戏开发，而是采用相对坐标进行定位，具体请参见 自动布局 一章【todo】
