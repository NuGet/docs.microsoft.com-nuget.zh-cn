---
title: "3.5 RC 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.5 RC 的发行说明。"
keywords: "NuGet 3.5 RC 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 发行说明

[NuGet 3.5 beta2 之前发行说明](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 发行说明](../release-notes/nuget-3.5-RTM.md)

3.5 版本侧重于提高质量和性能的 NuGet 客户端。 此外，如果我们发送的几个功能，如支持[回退文件夹](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)中支持`.nuspec`和的详细信息。

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>Bug 修复

* 包的安装/还原失败，"包包含多个`.nuspec`文件。" - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget 包强制增加`.tt`文件复制到内容文件夹无论- [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 包 csproj (与`project.json`) 发生崩溃，如果没有 packOptions 和在 JSON 文件的所有者[#3180](https://github.com/NuGet/Home/issues/3180)

* 适用于的 nuget 包`project.json`忽略摘要、 作者、 所有者等-之类的 packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)

* nuget 包将忽略输出中的依赖关系`.nuspec`为`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)

* 在任何下的文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)

* 无法打包面向.Net 库标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)

* 文件-> 新建项目-> 类库 （可移植） VS2015 和 Dev15-中的项目失败[#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 错误-1.0.0-* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 查找包无法显示，但安装包工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)

* 错误时 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 当已安装的 VS 2015 update 3 上使用的 NuGet 版本 3.5.0 错误发生的 VS [#3053](https://github.com/NuGet/Home/issues/3053)

* 包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete 命令行上不是读取/以发送 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正确的字符串： 稳定程序包版本不应具有在预发布的依赖项。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 创建 （net46 和 windows 10） 的 PCL 项目 get NullRef 异常。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新应提供信息性消息的 allowedVersions 约束的限制更高版本时[#3013](https://github.com/NuGet/Home/issues/3013)

* 凭据插件退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)

* nuget 包-缺少 Newtonsoft.Json 的包依赖关系- [# 2876年](https://github.com/NuGet/Home/issues/2876)

* 在 Linux/MacOS + Mono-上 ExecuteSynchronizedCore bug [# 2860年](https://github.com/NuGet/Home/issues/2860)

* VS 中 repositoryPath 不支持环境变量 （nuget.exe 一样）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 修复可访问性问题- [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 使用连字符连接的配置文件的可移植框架会被拒绝。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 包管理器应使它清楚该详细信息不适用于的包中的选项列表`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新失败，出现...的其他约束中定义 packages.config 会阻止此操作。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 从本地源中不存在将引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)

* "升级版提供"筛选器以显示与版本约束中的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>性能改进

* 性能： 改善 ContentModel 目标框架分析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 性能： 避免读取`runtime.json`没有 Rid 的还原的文件[#3150](https://github.com/NuGet/Home/issues/3150)。 在 CI 计算机上还原减少超额 15 秒到 3 秒的 ASP.NET Web 应用程序的示例。

* 性能： Package Manager Console init.ps1 加载时间[# 2956年](https://github.com/NuGet/Home/issues/2956)。 在某些情况下从 132s年到 10 次为单位，时间才能打开 PackageManagerConsole 得到改进。

* 解决在 NuGet 更新-ReSharper 性能问题[#3044](https://github.com/NuGet/Home/issues/3044)： 上的示例项目中，安装包所花的时间减少从 140s年到 68s。

## <a name="dcrs"></a>DCR

* NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)

* 错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 添加 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 打印 NuGet 警告标头内容控制台中 nuget.exe- [# 2934年](https://github.com/NuGet/Home/issues/2934)

* 利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)

* 从锁定文件的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)

* 符号包不应曾经使用在安装或更新 #2807

## <a name="features"></a>功能

* 对回退包文件夹的支持[# 2899年](https://github.com/NuGet/Home/issues/2899)

* 设计和实现包类型的概念，以支持工具包- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* 若要获取的全局包文件夹的路径的 API [# 2403年](https://github.com/NuGet/Home/issues/2403)

* 本机包更新支持- [# 1291年](https://github.com/NuGet/Home/issues/1291)
