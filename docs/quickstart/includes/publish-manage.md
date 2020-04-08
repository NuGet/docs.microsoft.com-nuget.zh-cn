---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495983"
---
从 nuget.org 上的配置文件中，选择“管理包”，查看刚刚发布的包。  同样也会收到确认电子邮件。 请注意，包可能需要一些时间才能编入索引并显示在可供他人查看的搜索结果中。 在该时间段，包页面会显示以下消息：

![此包未编制索引。 它将显示在搜索结果中，并可在索引编制完成后用于安装/还原。](../media/QS_Create-03-NotIndexed.png)

这就是所有的操作！ 刚刚已将第一个 NuGet 包发布到 nuget.org，其他开发人员可在自己的项目中使用它。

如果你已在本演练中创建一个实际上并不使用的包（例如使用空的类库创建的包），则应取消列出将在搜索结果中隐藏的包： 

1. 在 nuget.org 上，选择用户名（在该页的右上角），然后选择“管理包”  。

1. 找到你需要在“已发布”下取消列出的包，然后选择右侧的回收站图标： 

    ![在 nuget.org 上为包列表显示的回收站图标](../media/qs_create-vs-03-trash-can.png)

1. 在随后的页面上，清除标记有“在搜索结果中列出(包名)”的框，然后选择“保存”：  

    ![在 nuget.org 上清除包的“列表”复选框](../media/qs_create-vs-04-unlist.png)