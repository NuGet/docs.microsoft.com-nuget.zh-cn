---
title: NuGet 5.2 RTM 发行说明
description: NuGet 5.2 的发行说明，包括新功能、bug 修复和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776214"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装 

<sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装

## <a name="summary-whats-new-in-52"></a>摘要：5.2 中的新增功能

* 修复了由于 Linux & Mac 上的路径问题而导致不定期 NuGet 操作失败的严重 bug [#7341](https://github.com/NuGet/Home/issues/7341)

* 提高了使用 Visual Studio 中的 NuGet 包管理器 UI 浏览包时的 UI 响应能力，尤其是对于慢速源而言， [#8039](https://github.com/NuGet/Home/issues/8039)

* [#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和身份验证插件的 (的锁定文件的可靠性修补程序， ([#8300](https://github.com/NuGet/Home/issues/8300)[、#8271、](https://github.com/NuGet/Home/issues/8271)[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)[#7845) ](https://github.com/NuGet/Home/issues/7845)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* Perf：程序包管理器控制台： UI 延迟更新 "默认项目" combobox 选定的值- [#8235](https://github.com/NuGet/Home/issues/8235)

* 性能： PM UI 中的性能改进- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf：在 PMC 中读取默认项目时的 UI 延迟- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf： [vsfeedback] 针对本地包源的 "NuGet 更新" 选项卡冻结- [#6470](https://github.com/NuGet/Home/issues/6470)

* 插件：如果插件无法启动或提前终止，NuGet 将等待完全握手超时 [#8300](https://github.com/NuGet/Home/issues/8300)

* 插件：提高诊断插件启动故障- [#8271](https://github.com/NuGet/Home/issues/8271)

* 插件：内置插件 nuget.exe 发现问题- [#8269](https://github.com/NuGet/Home/issues/8269)

* 插件：缓存文件不是只读的 [#8210](https://github.com/NuGet/Home/issues/8210)

* 插件： "任务已取消。" 在还原过程中具有身份验证插件的错误- [#8198](https://github.com/NuGet/Home/issues/8198)

* 无法在 linux 平台上间歇地发现插件缓存- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile：使用 ATF 时，由于目标 framework 相等性检查错误，它具有 false NU1004 [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile：如果锁定文件为空或格式不正确，则不遵循 "--锁定模式" 还原标志 [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile：不包含包中的自定义程序集名称的小写项目锁定文件- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile：在锁定文件中使项目引用小写 [#7840](https://github.com/NuGet/Home/issues/7840)

* 还原：安装经过篡改的签名包将导致多次失败的安装尝试 (重复输出) - [#8175](https://github.com/NuGet/Home/issues/8175)

* VS：解决方案用户选项在 NuGet 更新后未能反序列化- [#8166](https://github.com/NuGet/Home/issues/8166)

* UnitTest 项目中的 dotnet 包返回错误- [#8154](https://github.com/NuGet/Home/issues/8154)

* 为 VS 安装程序创建 NuGet 包组-修复某些 VSIX 安装问题- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild 不应设置 NoBuild。 - [#7801](https://github.com/NuGet/Home/issues/7801)

* 当 nuspec 文件包含显式程序集引用元素[#7638](https://github.com/NuGet/Home/issues/7638)时，新选项 "-SymbolPackageFormat snupkg" 将生成错误。

* NuGet (498，5) ：错误：找不到路径 "/tmp/NuGetScratch" 的一部分 [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR:**

* 添加一个 msbuild 属性，该属性指示支持 PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference 通过 FrameworkReference 禁用依赖项流- [#7988](https://github.com/NuGet/Home/issues/7988)

* 用于在包外提供 runtime.js的机制- [#7351](https://github.com/NuGet/Home/issues/7351)

**[此版本中已修复的所有问题的列表-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


