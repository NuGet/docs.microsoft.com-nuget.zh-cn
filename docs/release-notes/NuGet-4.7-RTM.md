---
title: NuGet 4.7 RTM 发行说明
description: NuGet 4.7.0 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 79be74f9c54e27bf2c08e83c7adf81d1f96ce79a
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508158"
---
# <a name="nuget-47-rtm-release-notes"></a>NuGet 4.7 RTM 发行说明

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)。

## <a name="summary-whats-new-in-this-release"></a>摘要：此版本中的新增功能

* 我们已增强包签名，以便启用[存储库签名包](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* 在 Visual Studio 版本 15.7 中，我们已引入功能改为[迁移使用 packages.config 格式的现有项目以使用 PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference)。

## <a name="known-issues"></a>已知问题

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用

#### <a name="issue"></a>问题

首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。 这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。

#### <a name="workaround"></a>解决方法

执行以下 NuGet 操作之一：
* 打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`
* 打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`
* 运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`
* 生成还会触发 NuGet 还原的项目

现在应能够看到迁移选项。 请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题

.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。 [本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。

## <a name="top-issues-fixed-in-this-release"></a>此版本中已修复的主要问题

### <a name="bugs"></a>Bug

* NuGet 在 .Net Core 项目系统中遇到死锁（新回归）。 - [#6733](https://github.com/NuGet/Home/issues/6733)
* 包：如果 TfmSpecificPackageFile 与组合路径一起使用，则 PackagePath 构造不正确 - [#6726](https://github.com/NuGet/Home/issues/6726)
* 包：除非显式设置 ispackable，否则 Web API 项目无法创建包。 - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI 和 PMC 需要 30 分钟才能看到新包（nuget.exe 可以立即看到） - [#6657](https://github.com/NuGet/Home/issues/6657)
* 签名：SignatureUtility.GetCertificateChain(...) 不会检查所有链状态 - [#6565](https://github.com/NuGet/Home/issues/6565)
* 签名：改进 DER GeneralizedTime 处理 - [#6564](https://github.com/NuGet/Home/issues/6564)
* 签名：安装经篡改的包时，VS 不显示 NU3002 错误 - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary 区分大小写 - [#6500](https://github.com/NuGet/Home/issues/6500)
* 安装/更新还原代码和还原代码路径不一致 - [#3471](https://github.com/NuGet/Home/issues/3471)
* 解决方案 PackageManager 版本组合框可以通过键盘选择分隔符 - [#2606](https://github.com/NuGet/Home/issues/2606)
* 无法为源加载服务索引 `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException：响应状态代码指示不成功：403（已禁止） - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* 发出 X-NuGet-Session-Id 标头以跨请求关联[功能建议] - [#5330](https://github.com/NuGet/Home/issues/5330)
* 公开方法来等待运行通过 IV API 在 Visual Studio 中运行的还原操作。 - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint 将避免追加服务 URL 后缀 - [#6586](https://github.com/NuGet/Home/issues/6586)
* 将提交哈希添加到信息版本 - [#6492](https://github.com/NuGet/Home/issues/6492)
* 签名：启用存储库签名/副署删除 - [#6646](https://github.com/NuGet/Home/issues/6646)
* 签名：去除存储库签名/副署的 API - [#6589](https://github.com/NuGet/Home/issues/6589)
* VS 中的登录源信息 - [#6527](https://github.com/NuGet/Home/issues/6527)
* 仅在 TFM 和 RID 上筛选 /tools，以便可将设置 XML 置于 /tools 文件夹中 - [#6197](https://github.com/NuGet/Home/issues/6197)
* 当包命令排除开头的文件时发出警告。  - [#3308](https://github.com/NuGet/Home/issues/3308)

[此版本中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
