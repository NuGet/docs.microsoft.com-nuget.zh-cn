---
title: NuGet CLI 长路径支持
description: 支持 nuget.exe 长路径的参考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327674"
---
# <a name="long-path-support-nuget-cli"></a>长路径支持 (NuGet CLI)

**适用于:** 所有&bullet; **支持的版本:** 4.8 +

Nuget.exe 4.8 和更高版本支持文件和目录的长路径, 适用于打包、还原、安装和需要文件路径的大多数其他方案。

## <a name="required-operating-system"></a>所需操作系统

-   Windows 10 (版本1607或更高版本)
-   如果将 .NET Framework 升级到版本4.6.2 或更高版本, 则 Windows 10 (2015 年7月版或版本 1511)。
-   Windows Server 2016 (所有版本)

## <a name="enable-win32-long-paths-group-policy"></a>启用 "Win32 长路径" 组策略

需要通过设置组策略在这些系统上启用长路径支持。

逐步
1. 启动**组策略编辑器**-在 "开始" 搜索栏中键入 "编辑组策略", 或从 "运行" 命令运行 "gpedit.msc" (Windows-R)。
2. 在**本地组策略编辑器**中, 启用 "本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> 启用其他 NuGet 工具以支持长路径
>
> -   Dotnet CLI 支持长路径, 而不考虑操作系统或版本。
> -   Visual Studio 或 msbuild t:restore 尚不支持长路径。
> -   使用 NuGet 库执行还原和其他命令的软件将支持 Nuget.exe 在同一系统上的长路径, 前提是它们还在其 windows 清单中设置 longPathAware, 并通过 App.config[将 UseLegacyPathHandling 配置为 false查看详细信息](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

