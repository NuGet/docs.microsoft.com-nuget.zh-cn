---
title: "如何在 NuGet 中管理包缓存 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "如何管理计算机上存在的不同 NuGet 包缓存，安装或还原包时会用到这些包缓存。"
keywords: "NuGet 包缓存, 包缓存, NuGet 缓存, 管理缓存, 本地 NuGet 缓存, 全局 NuGet 缓存, NuGet 局部变量命令, 清除缓存"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>管理 NuGet 缓存

NuGet 管理多个本地缓存，以避免下载计算机上已经存在的包并提供离线支持。 在没有网络连接的情况下安装或重新安装包时，NuGet 2.8+ 自动回退到缓存。

可通过[局部变量命令](../tools/cli-ref-locals.md)使用缓存位置：

```
nuget locals all -list
```

典型输出如下所示：

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

如果安装包时遇到问题或想要确保从远程库安装包，请使用 `locals -clear` 选项：

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

请注意，目前仅支持从 NuGet 命令行管理缓存，而不支持在 Visual Studio 中或通过包管理器控制台管理缓存。 此外，NuGet 3.6 及更高版本中不支持管理 2.x 缓存。

使用 `nuget locals` 时可能出现以下错误：

* **清除本地资源失败：无法删除一个或多个文件**
* **目录不为空**

这表明你无权删除缓存中的文件，或缓存中的一个或多个文件正被另一进程使用，必须关闭这些文件，然后才能进行删除。
