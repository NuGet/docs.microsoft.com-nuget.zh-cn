---
title: NuGet 5.1 RTM 发行说明
description: 包括新功能、 bug 修复和 Dcr NuGet 5.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842579"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>随 Visual Studio 2019 一起安装.NET Core 工作负载 

<sup>2</sup>作为可选安装随.NET Core 工作负载的 Visual Studio 2019

## <a name="summary-whats-new-in-51"></a>摘要:什么是 5.1 中的新增功能

* 支持要跳过包推送，如果已存在，更好地集成 CI/CD 工作流- [# 1630年](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio 现在提供了方便指向包的 nuget.org 库页- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 新的.NET Core 3.0 是资产的支持，如[目标包](https://github.com/dotnet/cli/issues/10006)和[运行时包](https://github.com/dotnet/cli/issues/10007)
  * NuGet 包和还原的支持 FrameworkReferences 启用目标和运行时包引用- [#7342](https://github.com/NuGet/Home/issues/7342)
  * 支持"仅下载"包方案具有 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * 排除运行时和目标从搜索结果和还原的包关系图使用 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 插件： 插件期间的异常详细信息丢失[#8057](https://github.com/NuGet/Home/issues/8057)

* PackageReference 范围排他下限不适如果下限中存在，其中一个源。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)

* 包锁定文件的项目图发生更改时，请重新生成锁文件- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bug:Nuget 包获取自动删除- [#8017](https://github.com/NuGet/Home/issues/8017)

* 添加用于返回 FrameworkReference 目标类似于 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 缓存：RepositoryResources 资源未缓存的版本控制的方式- [#7997](https://github.com/NuGet/Home/issues/7997)

* 日志记录： 异常调用堆栈未报告详细- [#7955](https://github.com/NuGet/Home/issues/7955)

* 更改为使用 HTTPS-的所有 NuGet Docs Url [#7950](https://github.com/NuGet/Home/issues/7950)

* 提高 NU3024 警告消息- [#7933](https://github.com/NuGet/Home/issues/7933)

* 锁定文件未更新时删除了-packagereference [#7930](https://github.com/NuGet/Home/issues/7930)

* 验证 licenseurl 和许可证 nuspec-中的元素时改进错误 case 处理[#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI-右键单击选项卡标头，并单击"打开文件位置"错误-生成[#7913](https://github.com/NuGet/Home/issues/7913)

* 插件： 日志时插件进程退出的[#7907](https://github.com/NuGet/Home/issues/7907)

* 插件： 在日志记录的日期时间值的高冲突率[#7899](https://github.com/NuGet/Home/issues/7899)

* 上与 LicenseExpression-任何 nuspec 失败 Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode:意外的 NU1004 ProjectReference 引用具有自定义程序集名称的项目时[#7889](https://github.com/NuGet/Home/issues/7889)

* 更详细的错误消息时插件启动失败，异常- [#7857](https://github.com/NuGet/Home/issues/7857)

* 执行操作时 NoOp 还原，避免 *。 在 obj 目录-dgspec.json 写[#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true 无法生成在大小写不匹配的属性[#7843](https://github.com/NuGet/Home/issues/7843)

* 设置： 在包源路径中的非法字符可以导致 VS 崩溃- [#7820](https://github.com/NuGet/Home/issues/7820)

* 如果删除锁定文件，还原不会生成 NoOp-上的锁定文件[#7807](https://github.com/NuGet/Home/issues/7807)

* 许可证 URL 和许可证会导致读取错误与元数据- [#7547](https://github.com/NuGet/Home/issues/7547)

* 未经处理的异常中 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe 返回退出代码为零的参数无效- [#7178](https://github.com/NuGet/Home/issues/7178)

* 更新错误和警告文档以反映相关的签名方案- [#6498](https://github.com/NuGet/Home/issues/6498)

* 资产文件应该使用相对路径来更轻松地-启用移动项目[#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* 插件： 启用诊断日志记录- [#7859](https://github.com/NuGet/Home/issues/7859)

* 请 Tizen 6 映射到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[在此版本的 5.1 RTM 中已解决所有问题的列表](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
