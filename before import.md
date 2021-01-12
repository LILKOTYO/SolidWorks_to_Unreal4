# 模型导入前的处理

机器人模型（`.SLDPRT工程文件`）在导入到UE4前需要做一些预处理：

## 调整单位

由于**3DS MAX**的默认单位为英寸，UE4中的默认单位为厘米。所以需要在3DS MAX中的单位改为厘米，否则在导入到UE4后会出现比例失调。调整步骤：

* 打开**3DS MAX**，选择菜单栏<kbd>自定义</kbd>-><kbd>单位设置</kbd>
* 点击系统单位设置，系统单位比例，将单位改为厘米，关闭系统单位设置

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/change_unit_01.png)

* 显示单位比例一栏，选择 **公制** ，单位选择厘米

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/change_unit_02.png)

* 确定即可

## 在**3DS MAX**中打开**SolidWorks**的`.SLDPRT工程文件`

打开文件后，首先使用测量工具测量一下模型的大小，因为，如果在**SolidWorks**创建模型时运用的单位不是厘米，模型在导入后会被等比例的放大/缩小若干倍。如果模型大小有变化，则需要等比例放缩到正常的大小。（对于我们的机器人则不用，因为我们在**SolidWorks**建模时边使用了厘米为单位。

接下来需要将模型放置在地平面（x-z平面）上，点击创建工具，

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/create_tool.png)

在俯视图中创建平面：

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/create_plane_01.png)

选中平面（这一步在正视图中操作比较方便），点击对齐工具，然后再选中机器人（对齐工具的逻辑是移动选中的物体去对齐之后选中的物体），进行如下设置：

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/create_plane_02.png)



最终得到结果如下

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/create_plane_03.png)



## 模型分组

为了在UE4中进行控制，需要将模型中可动部分（车轮,wheel）和不可动部分（body）进行分组。

框选机器人模型的对应部分进行编组即可，如果机器人实现有编组则解组，操作在<kbd>菜单</kbd>-><kbd>组</kbd>中完成。我按照机器人主体以及四个轮子将模型的268个零件分为了四组，如图所示（图中左侧选定了body，右侧body部分高亮）：

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/group.png)



## 设置轴心

为了让车轮能够正确绕轴旋转，需要给车轮正确设置轴心。

以轮胎wheel_01为例，选定wheel_01，选择右侧**层次**工具，点击**仅影响轴**，此时便可以在视图中观察到wheel_01的轴心和xyz轴，继续选择**居中到对象**，即可正确设置车轮的轴心。（轴应当是平行和垂直于车轮的，如果不是，使用旋转工具将其调整到正确的方向）

![Aaron Swartz](https://raw.githubusercontent.com/LILKOTYO/SolidWorks_to_Unreal4/master/Pictures/set_axis.png)

