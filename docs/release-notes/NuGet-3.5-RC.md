---
title: 3.5 RC 发行说明
description: NuGet 3.5 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780200"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 发行说明

[NuGet 3.5-Beta2 发行说明](../release-notes/nuget-3.5-Beta2.md)  | [NuGet 3.5-RTM 发行说明](../release-notes/nuget-3.5-RTM.md)

3.5 版本侧重于提高 NuGet 客户端的质量和性能。 此外，我们还提供了一些功能，如对 [后备文件夹](https://github.com/NuGet/Home/issues/2899)的支持、 [PackageType](https://github.com/NuGet/Home/issues/2476) 的支持 `.nuspec` 。

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Bug 修复

* 安装/还原包失败，出现 "包包含多个 `.nuspec` 文件"。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 不管 #3203 如何，nuget 包都会强制将 `.tt` 文件添加到[](https://github.com/NuGet/Home/issues/3203) content 文件夹中

* `project.json`如果 JSON 文件中没有 packOptions 和所有者，nuget 包 .csproj () 崩溃[#3180](https://github.com/NuGet/Home/issues/3180)

* 的 nuget 包 `project.json` 忽略 packOptions 标记，如摘要、作者、所有者等 [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget 包忽略 `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)的输出中的依赖关系

* 使用 rollback 更新多个包会使项目处于损坏状态- [#3139](https://github.com/NuGet/Home/issues/3139)

* 不会为 netstandard 项目添加 ContentFiles 下的任何项目- [#3118](https://github.com/NuGet/Home/issues/3118)

* 无法正确打包面向 .Net Standard 的库目标- [#3108](https://github.com/NuGet/Home/issues/3108)

* 文件-> 新项目-> 类库 (可移植) 项目在 VS2015 和 Dev15 中失败- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 错误-1.0.0-* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package 无法显示但 Install-Package 工作- [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15 上的 "安装包 jquery. 验证" 时出错- [#3061](https://github.com/NuGet/Home/issues/3061)

* 在使用 NuGet 版本3.5.0 的 VS 上安装 VS 2015 update 3 时出现错误- [#3053](https://github.com/NuGet/Home/issues/3053)

* 程序包管理器 UI：更新包后不显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey on delete 命令行在3.5.0 中未被读/发送- [#3037](https://github.com/NuGet/Home/issues/3037)

* 字符串不正确：包的稳定版本不应具有预发行依赖项。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 创建 PCL (net46 和 windows 10) project 获取 NullRef 异常。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 当 allowedVersions 约束限制更高版本时，Nuget 更新应提供信息性消息 [#3013](https://github.com/NuGet/Home/issues/3013)

* 凭据插件已退出，出现错误-1/在将凭据提供程序与多个源一起使用时下载包- [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget 包-缺少有关包依赖项的 Newtonsoft.Js- [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS 上的 ExecuteSynchronizedCore 中的 Bug + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS 不支持 repositoryPath 中的环境变量 ( # A0) - [#2763](https://github.com/NuGet/Home/issues/2763)

* 解决辅助功能问题- [#2745](https://github.com/NuGet/Home/issues/2745)

* 拒绝带有断字符配置文件的便携式框架。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 包管理器应当清楚地说明包详细信息中的选项列表不适用于 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新失败，并出现 "a 附加约束 ..."在 packages.config 中定义可防止此操作。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 从不存在的本地源安装包将引发虚假消息 [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade v" 筛选器显示违反版本约束的升级- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>性能改进

* 性能：提高 ContentModel 目标框架分析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 性能：避免读取 `runtime.json` 没有 rid [#3150](https://github.com/NuGet/Home/issues/3150)的还原文件。 在 CI 计算机上，ASP.NET Web 应用程序的还原从15秒到3秒的缩短。

* 性能：程序包管理器控制台 init.ps1 加载时间 [#2956](https://github.com/NuGet/Home/issues/2956)。 在某些情况下，从132s 到数十的打开 PackageManagerConsole 的时间已改进。

* 解决 NuGet 更新中的 ReSharper 性能问题- [#3044](https://github.com/NuGet/Home/issues/3044)：在示例项目上，安装包的时间从140s 减少到68s。

## <a name="dcrs"></a>DCR

* NuGet 需要让用户知道在基于 dotnet tfm 的 PCL 中升级/安装可能会导致问题 [#3138](https://github.com/NuGet/Home/issues/3138)

* 为 project （tfm = "dotnet"）警告安装/升级失败- [#3137](https://github.com/NuGet/Home/issues/3137)

* 添加 netcoreapp11 和 netstandard17 支持- [#2998](https://github.com/NuGet/Home/issues/2998)

* 将 NuGet-Warning 标题内容打印到 nuget.exe 中的控制台 [#2934](https://github.com/NuGet/Home/issues/2934)

* 将 AssemblyMetadata 特性用于 `.nuspec` 标记替换- [#2851](https://github.com/NuGet/Home/issues/2851)

* 从锁定文件中删除锁定的属性- [#2379](https://github.com/NuGet/Home/issues/2379)

* 不应在安装或更新 #2807 中使用符号包

## <a name="features"></a>功能

* 支持备用包文件夹- [#2899](https://github.com/NuGet/Home/issues/2899)

* 设计和实现包类型的概念以支持工具包- [#2476](https://github.com/NuGet/Home/issues/2476)

* 用于获取全局包文件夹的路径的 API- [#2403](https://github.com/NuGet/Home/issues/2403)

* 本机包更新支持- [#1291](https://github.com/NuGet/Home/issues/1291)
