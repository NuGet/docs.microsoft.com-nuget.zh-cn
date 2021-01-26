---
title: NuGet 5.1 RTM 发行说明
description: NuGet 5.1 的发行说明，包括新功能、bug 修复和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780129"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装 

<sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装

## <a name="summary-whats-new-in-51"></a>摘要：5.1 中的新增功能

* 支持跳过包推送（如果它已存在，以便更好地与 CI/CD 工作流集成）， [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio 现在提供了一个方便的链接，指向包的 nuget.org 库页 [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 支持新的 .NET Core 3.0 资产，例如 [目标包](https://github.com/dotnet/cli/issues/10006) 和 [运行时包](https://github.com/dotnet/cli/issues/10007)
  * 针对 FrameworkReferences 的 NuGet 包和还原支持启用目标和运行时包引用- [#7342](https://github.com/NuGet/Home/issues/7342)
  * 支持 "仅下载" 包方案和 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * 使用 PackageType 从搜索结果中排除运行时和目标包 & 还原图形- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 插件：在创建插件期间丢失异常详细信息- [#8057](https://github.com/NuGet/Home/issues/8057)

* 如果某个源上存在下限，则具有互斥下限的 PackageReference 范围将不起作用。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* 提高 IsPackableFalseError 消息 [#8021](https://github.com/NuGet/Home/issues/8021)

* 包锁定文件-在项目关系图发生更改时重新生成锁定文件- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bug：已自动删除 Nuget 包- [#8017](https://github.com/NuGet/Home/issues/8017)

* 添加用于返回 FrameworkReference 的目标，类似于 CollectPackageDownloads 和 CollectPackageReferences [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 缓存： RepositoryResources 资源未按版本控制方式缓存- [#7997](https://github.com/NuGet/Home/issues/7997)

* 日志记录：不会报告异常调用堆栈详细详细信息- [#7955](https://github.com/NuGet/Home/issues/7955)

* 更改所有 NuGet 文档 Url 以使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* 提高 NU3024 警告消息 [#7933](https://github.com/NuGet/Home/issues/7933)

* 删除 packagereference 时锁定文件未更新- [#7930](https://github.com/NuGet/Home/issues/7930)

* 改善在 nuspec 中验证 licenseurl 和 license 元素时处理的错误情况处理 [#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI-右键单击选项卡标题，并单击 "打开文件位置" 会导致错误- [#7913](https://github.com/NuGet/Home/issues/7913)

* 插件：插件进程退出时的日志- [#7907](https://github.com/NuGet/Home/issues/7907)

* 插件：记录日期时间值的高冲突率- [#7899](https://github.com/NuGet/Home/issues/7899)

* System.xml.linq.xnode.readfrom 在具有 LicenseExpression [#7894](https://github.com/NuGet/Home/issues/7894)的任何 nuspec 上失败

* RestoreLockedMode：当 ProjectReference 引用具有自定义 AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)的项目时，意外 NU1004

* 如果插件启动失败并出现异常，则提供更好的错误消息- [#7857](https://github.com/NuGet/Home/issues/7857)

* 执行 NoOp 还原时，请避免 * .dgspec.js在 obj 目录中写入 [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true 生成属性时失败，大小写不匹配- [#7843](https://github.com/NuGet/Home/issues/7843)

* 设置：包源路径中的非法字符会导致与[#7820](https://github.com/NuGet/Home/issues/7820)崩溃

* 如果删除了 "锁定文件"，则还原不会在 NoOp 上生成锁定文件- [#7807](https://github.com/NuGet/Home/issues/7807)

* 许可证 URL 和许可证会导致元数据的读取错误- [#7547](https://github.com/NuGet/Home/issues/7547)

* V2FeedParser 中的未处理异常- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe 返回无效参数的退出代码零- [#7178](https://github.com/NuGet/Home/issues/7178)

* 更新错误和警告文档，以反映与签名相关的方案- [#6498](https://github.com/NuGet/Home/issues/6498)

* 资产文件应使用相对路径来更轻松地移动项目- [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* 插件：启用诊断日志记录- [#7859](https://github.com/NuGet/Home/issues/7859)

* 使 Tizen 6 映射到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[此版本中已修复的所有问题的列表-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
