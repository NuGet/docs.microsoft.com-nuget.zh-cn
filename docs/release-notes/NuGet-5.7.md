---
title: NuGet 5.7 发行说明
description: NuGet 5.7 的发行说明，包括新功能、bug 修复和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364149"
---
# <a name="nuget-57-release-notes"></a>NuGet 5.7 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装

## <a name="summary-whats-new-in-57"></a>摘要：5.7 中的新增功能

### <a name="features-added-in-this-release"></a>此版本中添加的功能

* 添加了对 NuGet 包引用的 extern 别名支持- [#4989](https://github.com/NuGet/Home/issues/4989)

* 通过允许它们共享数据源并减少 resfreshing，在已安装和更新选项卡之间进行切换更快 [#8294](https://github.com/NuGet/Home/issues/8294)

* 通过调用 MSBuild 静态图形 api ( # A0) - [#9644](https://github.com/NuGet/Home/issues/9644) ，提高还原速度

* 为 PackageReference 项目添加了 Visual Studio 部分还原 (无操作 + +) - [#9513](https://github.com/NuGet/Home/issues/9513)

* 对于每个 HTTP 请求返回的结果数超过请求数的结果包源，Visual Studio 包管理器 UI 会出现故障的情况。 - [#8478](https://github.com/NuGet/Home/issues/8478)

* 添加了[#9236](https://github.com/NuGet/Home/issues/9236) VS PackageVersion 中非 SDK 样式项目的信息集成

* 添加了对 nuget.exe 更新的支持 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* 在%APPDATA%\NuGet 目录中添加了对多个配置文件的支持- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths 现在会将 NuGet 源包纳入帐户 [#9431](https://github.com/NuGet/Home/issues/9431)

* 添加了 INuGetProjectService GetInstalledPackagesAsync 扩展性 API- [#9702](https://github.com/NuGet/Home/issues/9702)

* 添加了互操作 API 以枚举回退文件夹，而无需解决方案/项目- [#9395](https://github.com/NuGet/Home/issues/9395)

* 添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**漏洞**

* 在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。 - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* 如果更改了程序集名称，则在使用 assemblyinfo 时，如果更改了程序集名称，NuGet.exe 将引发在 .csproj 包中忽略占位符和特性[#4234](https://github.com/NuGet/Home/issues/4234)的异常 "

* HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持

* NuGet。索引5.6.0 预览版3和更高版本使用不同的公钥令牌- [#9481](https://github.com/NuGet/Home/issues/9481)

* 在创建 NuGet 包期间遵循 TreatWarningsAsErrors- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM]多个 p2p 项目的假包降级- [#9549](https://github.com/NuGet/Home/issues/9549)

* "浏览" 选项卡并不与搜索框左对齐- [#9559](https://github.com/NuGet/Home/issues/9559)

* 安装的版本与安装了多个版本的包 id 的解决方案级别 PM UI 中的嵌入图标不一致- [#9321](https://github.com/NuGet/Home/issues/9321)

* 泄漏： PartCreationPolicy (CreationPolicy) SolutionRestoreManager RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* 避免在无操作还原中读取资产文件- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086)

* 减少 JObject 依赖项，从而提高 PackageMetadataResourceV3 的内存性能 [#9719](https://github.com/NuGet/Home/issues/9719)

**设计更改请求：**

* `<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)

* 将 IntervalTrackers 记录为 ETW 事件- [#9593](https://github.com/NuGet/Home/issues/9593)

* 在 restore 上添加了信息性消息，通知 CPVM 用户该功能处于预览中- [#9340](https://github.com/NuGet/Home/issues/9340)

* 填充资产文件中解决方案资源管理器包/项目可传递依赖项- [#9580](https://github.com/NuGet/Home/issues/9580)

* "已安装的包" 选项卡不应将包列表分页- [#6995](https://github.com/NuGet/Home/issues/6995)

**[此版本中已修复的所有问题的列表-5。7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>社区参与

感谢所有有助于使此 NuGet 版本非常出色的参与者！

|谁|Pr|问题|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持|
|[Joseph Musser (jnm2) ](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|`<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad) ](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet 无法从需要客户端证书的 HTTPS 源还原- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok) ](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim 未来的校对- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek) ](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Marc-olivier Spinelli (marc-olivier-Spinelli) ](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。 - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项|
