---
title: NuGet CLI 长路径支持
description: Nuget.exe 长路径支持的引用
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547821"
---
# <a name="long-path-support-nuget-cli"></a>长路径支持 (NuGet CLI)

**适用于：** 所有&bullet;**支持的版本：** 4.8 +

NuGet.exe 4.8 及更高版本支持长路径的文件和目录的方案，如包、 还原、 安装和大多数其他情况下需要文件路径。

## <a name="required-operating-system"></a>所需的操作系统

-   Windows 10 （版本 1607 或更高版本）
-   Windows 10 （2015 年 7 月版本或版本 1511年） 如果您升级到版本 4.6.2 的.NET Framework 或更高版本。
-   Windows Server 2016 （所有版本）

## <a name="enable-win32-long-paths-group-policy"></a>启用"Win32 长路径"组策略

需要通过设置组策略启用长路径支持这两个系统上。

步骤：
1. 启动**组策略编辑器**-键入开始搜索栏中的"编辑组策略"或运行命令 (Windows-R) 运行"gpedit.msc"。
2. 在中**本地组策略编辑器**，启用"本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> 启用其他 NuGet 工具以支持长路径
>
> -   Dotnet CLI 支持长路径而不用考虑操作系统或版本。
> -   Visual Studio 或 msbuild /t: restore 尚不支持长路径。
> -   软件使用 NuGet 库执行还原和其他命令，将支持长路径在同一系统上，NuGet.exe 适用于，如果他们还设置在其 windows longPathAware 清单并为 false，通过 App.Config配置UseLegacyPathHandling[请参阅详细信息](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

