---
title: NuGet CLI 长路径支持
description: nuget.exe 长路径支持的参考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238187"
---
# <a name="long-path-support-nuget-cli"></a> (NuGet CLI) 的长路径支持

**适用于：** 所有 &bullet; **支持的版本：** 4.8 +

NuGet.exe 4.8 和更高版本支持文件和目录的长路径，适用于打包、还原、安装和需要文件路径的大多数其他方案。

## <a name="required-operating-system"></a>所需操作系统

-   Windows 10 (版本1607或更高版本) 
-   如果将 .NET Framework 升级到4.6.2 或更高版本，则 Windows 10 (7 2015 月发行版或 1511) 版本。
-   Windows Server 2016 (所有版本) 

## <a name="enable-win32-long-paths-group-policy"></a>启用 "Win32 长路径" 组策略

需要通过设置组策略在这些系统上启用长路径支持。

步骤：
1. 在 "开始" 搜索栏中启动 **组策略编辑器** "" 编辑组策略 "，或从" 运行 "命令 (Windows-R) 运行" gpedit.msc "。
2. 在 **本地组策略编辑器** 中，启用 "本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> 启用其他 NuGet 工具以支持长路径
>
> -   Dotnet CLI 支持长路径，而不考虑操作系统或版本。
> -   Visual Studio 或 `msbuild -t:restore` 尚不支持长路径。
> -   使用 NuGet 库执行还原和其他命令的软件将支持在 NuGet.exe 工作的同一系统上的长路径，如果它们也 `longPathAware` 在 windows 清单中设置并 `UseLegacyPathHandling` 通过配置为 `false` via App.Config [查看详细信息](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)