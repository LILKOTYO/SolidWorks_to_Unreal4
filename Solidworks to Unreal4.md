# UE4导入异构机器人3D模型

目前主要发现三种方法：

## 转化格式为`.FBX`

将机器人模型从**SolidWorks**中导出，格式为`.SLDPRT工程文件`，然后将其导入到**3DS MAX**中。

在下一步导入到UE4之前，需要对模型进行建立骨骼和蒙皮等操作，详见文件`before import.md`，[链接](https://github.com/LILKOTYO/SolidWorks_to_Unreal4/blob/master/before%20import.md)

> 发现问题：
>
> * 导入时间较长，复杂模型导入到UE4时会卡死。  



## 转化格式为`.udatasmith` 

**DataSmith**是一系列工具和插件的集合，可以将使用各种行业标准设计应用创建的完整预构建场景和复杂资源导入虚幻引擎。项目中它的作用是将SolidWorks的模型文件导入到UE4中。

**3DS MAX**的文件无法直接导入到UE4中，所以首先需要安装**DataSmith**的导出器插件，步骤如下（只需要执行一次）：

* 安装UE4提供的**DataSmith**的**Autodesk 3ds Max导出器**，[下载链接](https://www.unrealengine.com/zh-CN/datasmith/plugins)。
* 打开UE4，打开任意一个项目，选择<kbd>菜单</kbd>-><kbd>设置</kbd>-><kbd>插件</kbd>，在弹出的页面中搜索并找到***DataSmith Importer***，将其启用。
* 重启UE4即可生效。

插件生效后，将`.STL文件`导入到**3DS MAX**中，然后导出为`.udatasmith文件`，最后再打开UE4，将其通过<kbd>菜单</kbd>-><kbd>DataSmith</kbd>导入到UE4中。

> 发现问题：
>
> * 目前可以比较顺利地将模型导入到UE4中，但是由于不是直接导入**SolidWorks**工程文件，而是经过了多次导入导出转换格式，或许会存在数据损失，模型失真；
> * 导入base_link到UE4中时报错，”*无法找到某某网格体* “，暂不清楚报错原因及其影响。



## 直接导入**SolidWorks**中的`.SLDPRT工程文件`

首先需要激活**DataSmith**的CAD插件，步骤如下（只需要执行一次）：

* 打开UE4，打开任意一个项目，选择<kbd>菜单</kbd>-><kbd>设置</kbd>-><kbd>插件</kbd>，在弹出的页面中搜索并找到**DataSmith CAD Importer**，将其启用。
* 重启UE4使其生效。

接下来**SolidWorks**将工程文件导出为`.SLDPRT工程文件`，打开UE4，将其通过<kbd>菜单</kbd>-><kbd>DataSmith</kbd>导入到UE4中。

> 发现问题：
>
> 暂时导入进的模型打开后没有任何显示，是一个空白Actor，原因暂不清楚。