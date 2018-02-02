---
title: "NuGet 3.2 RC 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.2 RC 的发行说明。"
keywords: "NuGet 3.2 RC 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b19f62217ed79689ce067107dd64dfffe2c59291
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC 发行说明

[NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 发行说明](../release-notes/nuget-3.2.md)

发布 NuGet 3.2 候选发布版 2015 年 9 月 2 日为一个集合的改进和 3.1.1 修补程序版本。  此外，这些是在被发布到新 dist.nuget.org 存储库的第一次的第一个版本。

## <a name="new-features"></a>新增功能

* 实时所在的文件夹中的项目现在可以具有不同`project.json`该特定于每个项目的文件夹中的文件。  对于每个项目，将`project.json`文件`{ProjectName}.project.json`，NuGet 将正确引用并相应地为每个项目中使用该内容。  这样可支持新功能[1102年](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config`现在支持为相对路径-globalPackagesFolder [1062年](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>命令行的更新

这是支持的 NuGet v3 服务器的 nuget.exe 客户端的第一个版本，并且还原项目包使用托管`project.json`文件。

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>没有大量的经过身份验证的源问题已解决在此版本中以提高与客户端交互。

* 安装 / 还原交互仅提交到经过身份验证数据源的初始请求凭据[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)
* 推送命令不能解决从配置的凭据[1248年](https://github.com/NuGet/Home/issues/1248)
* 用户代理和标头现在提交到 NuGet 存储库有助于统计信息跟踪- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>我们做了大量改进，可尝试使用远程的 NuGet 存储库时更好地处理网络故障：

* 改进错误消息时无法连接到远程源- [1238年](https://github.com/NuGet/Home/issues/1238)
* 更正了 NuGet 还原命令时出现错误条件的正确返回 1 [1186年](https://github.com/NuGet/Home/issues/1186)
* 现在重试网络连接最多 5 次尝试 HTTP 5xx 失败-对于每个 200ms年[1120年](https://github.com/NuGet/Home/issues/1120)
* 改进的服务器重定向响应处理期间推送命令- [1051年](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`现在支持从作为自变量-Nuget.Config 的 URL 或存储库名称[1046年](https://github.com/NuGet/Home/issues/1046)
* 缺少的程序包在还原过程中不存储库位于现在报告为错误而不是警告[1038年](https://github.com/NuGet/Home/issues/1038)
* 更正的 Unix/Linux 方案-\r\n multipartwebrequest 处理[776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>有大量的各种命令出现问题的修复：

* 推送命令不会再之前对包源-PUT GET [1237年](https://github.com/NuGet/Home/issues/1237)
* 列表命令不再重复版本号- [1185年](https://github.com/NuGet/Home/issues/1185)
* 包使用的生成参数现在正确支持 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)
* 已更正的问题，尝试包 F # 项目生成使用 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)
* 当包已经存在-还原现在否 ops [1040年](https://github.com/NuGet/Home/issues/1040)
* 改进的错误消息时`packages.config`文件格式不正确- [1034年](https://github.com/NuGet/Home/issues/1034)
* 更正与还原命令`-SolutionDirectory`开关来使用相对路径- [992](https://github.com/NuGet/Home/issues/992)
* 改进的更新命令，以支持解决方案范围更新- [924](https://github.com/NuGet/Home/issues/924)

在 NuGet GitHub 中找不到在此版本中解决的问题的完整列表[命令行里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。

## <a name="visual-studio-extension-updates"></a>Visual Studio 扩展更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 中的新增功能

* 新的上下文菜单项已添加到解决方案资源管理器使包得以还原而不生成解决方案的解决方案节点上 ([1274年](https://github.com/NuGet/Home/issues/1274))。

![新还原包上下文菜单项](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新和修补在 Visual Studio 中

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>经过身份验证的源的修补程序汇总中的扩展以及解决。  以下身份验证项还已扩展中得到解决:

* 现在正确将 NuGet v3 正确，身份验证源而不是 v2 已经过身份验证源- [1216年](https://github.com/NuGet/Home/issues/1216)
* 在项目中使用的身份验证凭据的已更正的请求`project.json`以及与 v2 馈送-通信[1082年](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>网络连接有影响的用户界面在 Visual Studio 中，并且我们使用了下列修补程序来解决此：

* 改进的包版本的本地缓存维护[1096年](https://github.com/NuGet/Home/issues/1096)
* 连接到源不再尝试将其视为 v2 源-v3 时更改失败行为[1253年](https://github.com/NuGet/Home/issues/1253)
* 现在阻止安装失败时使用多个包源的安装包[1183年](https://github.com/NuGet/Home/issues/1183)

我们改进与生成操作的交互的处理：

* 现在继续生成项目，如果为单个项目失败-还原包[1169年](https://github.com/NuGet/Home/issues/1169)
* 将包安装到解决方案中的另一个项目依赖于项目强制解决方案重新生成的[981](https://github.com/NuGet/Home/issues/981)
* 更正失败的包安装到项目的正确回滚更改[1265年](https://github.com/NuGet/Home/issues/1265)
* 更正无意中的删除`developmentDependency`属性中的包`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)
* 调用`install.ps1`现在拥有适当的`$package.AssemblyReferences`传递的对象[1245年](https://github.com/NuGet/Home/issues/1245)
* 处于错误状态的项目时的 UWP 项目中的包不再阻止卸载[1128年](https://github.com/NuGet/Home/issues/1128)
* 包含多种解决方案`packages.config`和`project.json`而无需第二个现在正确生成项目生成操作- [1122年](https://github.com/NuGet/Home/issues/1122)
* 如果链接或位于不同的文件夹的正确定位 app.config 文件[1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)
* UWP 项目现在可以安装未列出的包- [1109年](https://github.com/NuGet/Home/issues/1109)
* 虽然解决方案并不处于保存状态的程序包还原现在允许[1081年](https://github.com/NuGet/Home/issues/1081)


处理对配置文件已更正的更新：

* 从上的后续版本的包不能再删除的目标文件传递`project.json`托管的项目- [1288年](https://github.com/NuGet/Home/issues/1288)
* 无法再在 ASP.NET 5 解决方案生成的期间修改 Nuget.Config 文件[1201年](https://github.com/NuGet/Home/issues/1201)
* 允许包更新的过程中无法再更改版本约束[1130年](https://github.com/NuGet/Home/issues/1130)
* 锁定文件现在继续处于锁定状态生成的期间[1127年](https://github.com/NuGet/Home/issues/1127)
* 正在修改`packages.config`和不在更新的过程中重写该[585](https://github.com/NuGet/Home/issues/585)


与 TFS 源代码管理的交互将有所改进：

* 不再失败的包的绑定到 TFS 的安装[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)
* 已更正的 NuGet 用户界面，以允许 TFS 2013 集成- [1071年](https://github.com/NuGet/Home/issues/1071)
* 更正对包还原正确来自的包文件夹的引用[1004年](https://github.com/NuGet/Home/issues/1004)

最后，我们还改进这些项：

* 针对日志消息的详细程度减小`project.json`托管项目的[1163年](https://github.com/NuGet/Home/issues/1163)
* 现在在用户界面中的正确显示安装的包版本[1061年](https://github.com/NuGet/Home/issues/1061)


问题解决有关在 NuGet GitHub 中找不到 Visual Studio 扩展的完整列表[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>已知问题

我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)