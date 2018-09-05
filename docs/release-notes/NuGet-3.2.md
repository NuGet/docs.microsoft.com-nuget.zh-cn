---
title: NuGet 3.2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549517"
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 发行说明

[NuGet 3.2 RC 发行说明](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md)

发布 NuGet 3.2 2015 年 9 月 16 日作为一系列改进和修复了 3.1.1 发布并且可从这两个[dist.nuget.org](http://dist.nuget.org/index.html)并[Visual Studio 库](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)。

## <a name="new-features"></a>新增功能

* 位于相同的文件夹的项目现在可以具有不同`project.json`特定于每个项目的文件夹中的文件。  对于每个项目，命名`project.json`文件`{ProjectName}.project.json`，NuGet 会相应地提供首选项设置为每个项目的配置。  与安装的 Windows 10 工具 1.1 版才支持此[1102年](https://github.com/NuGet/Home/issues/1102)
* NuGet 客户端支持指定全局 NUGET_PACKAGES 环境变量指定的位置中使用的共享的全局包文件夹`project.json`托管使用 Windows 10 工具 1.1 版的项目。

## <a name="command-line-updates"></a>命令行的更新

这是支持 NuGet v3 服务器的 nuget.exe 客户端的第一个版本，使用还原项目包管理`project.json`文件。

没有大量的经过身份验证源的问题已解决在此版本中以提高与客户端之间的交互。

* 安装 / 还原交互只能提交到经过身份验证数据源的初始请求凭据[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)
* Push 命令不能解决从配置的凭据[1248年](https://github.com/NuGet/Home/issues/1248)
* 用户代理和标头现在提交到 NuGet 存储库，以便统计信息跟踪- [929](https://github.com/NuGet/Home/issues/929)

我们做了大量改进，可尝试使用远程 NuGet 存储库时更好地处理网络故障：

* 改进了错误消息时无法连接到远程源- [1238年](https://github.com/NuGet/Home/issues/1238)
* 更正了 NuGet 还原命令时将发生错误情况的正确返回 1 [1186年](https://github.com/NuGet/Home/issues/1186)
* 现在重试网络连接最多 5 次尝试 HTTP 5xx 故障-的情况下每隔 200 毫秒[1120年](https://github.com/NuGet/Home/issues/1120)
* 改进的服务器重定向响应的处理期间推送命令- [1051年](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 现在支持作为自变量的 Nuget.Config 中的 URL 或存储库名称[1046年](https://github.com/NuGet/Home/issues/1046)
* 在还原过程中已不在存储库位于的缺失包现在报告为错误而不是警告[1038年](https://github.com/NuGet/Home/issues/1038)
* 更正的 Unix/Linux 方案-\r\n multipartwebrequest 处理[776](https://github.com/NuGet/Home/issues/776)

有大量的各种命令的问题的修补程序：

* Push 命令不会再对包源的 PUT 前 GET [1237年](https://github.com/NuGet/Home/issues/1237)
* 列表命令不再重复版本号- [1185年](https://github.com/NuGet/Home/issues/1185)
* 包使用的生成参数现在正确地支持 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)
* 已更正的问题尝试打包 F # 项目使用 Visual Studio 2015-生成[1048年](https://github.com/NuGet/Home/issues/1048)
* 不还原现在进行任何操作时的包已经存在- [1040年](https://github.com/NuGet/Home/issues/1040)
* 改进的错误消息何时`packages.config`文件的格式不正确- [1034年](https://github.com/NuGet/Home/issues/1034)
* 更正了带-SolutionDirectory 开关还原命令，可以使用相对路径- [992](https://github.com/NuGet/Home/issues/992)
* 改进了更新命令，以支持解决方案级更新- [924](https://github.com/NuGet/Home/issues/924)

在此版本中已解决的问题的完整列表可在 NuGet GitHub[命令行里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。

## <a name="visual-studio-extension-updates"></a>Visual Studio 扩展更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 中的新增功能

* 新的上下文菜单项已添加到解决方案资源管理器允许包在还原时不用生成解决方案的解决方案节点上 ([1274年](https://github.com/NuGet/Home/issues/1274))。

![新还原包上下文菜单项](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新和修补程序在 Visual Studio 中

已验证的源的修补程序已累加起来，并且也在扩展中解决。  以下身份验证项还已扩展中得到解决:

* 现在正确，正确处理 NuGet v3 已验证的源而不是 v2 已经过身份验证源- [1216年](https://github.com/NuGet/Home/issues/1216)
* 在项目中使用的身份验证凭据的已更正的请求`project.json`以及与 v2 源-通信[1082年](https://github.com/NuGet/Home/issues/1082)

网络连接有影响 Visual Studio 中的用户界面和我们解决了此与以下修补程序：

* 改进的包版本的本地缓存维护[1096年](https://github.com/NuGet/Home/issues/1096)
* 连接到源到无法再尝试将其视为 v2 源-v3 时更改失败行为[1253年](https://github.com/NuGet/Home/issues/1253)
* 用多个包源的安装包时，现在阻止安装故障[1183年](https://github.com/NuGet/Home/issues/1183)

我们改进了与生成操作之间的交互的处理：

* 现在，继续生成项目，如果还原包，为单个项目失败- [1169年](https://github.com/NuGet/Home/issues/1169)
* 将包安装到解决方案中的另一个项目依赖的项目强制解决方案重新生成- [981](https://github.com/NuGet/Home/issues/981)
* 更正失败的包安装到项目的正确回滚更改[1265年](https://github.com/NuGet/Home/issues/1265)
* 更正了无意中的删除`developmentDependency`属性中的包`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)
* 调用`install.ps1`现在具有适当`$package.AssemblyReferences`传递的对象[1245年](https://github.com/NuGet/Home/issues/1245)
* 不再阻止卸载包在 UWP 项目中的项目时处于错误状态- [1128年](https://github.com/NuGet/Home/issues/1128)
* 其中包含的各种解决方案`packages.config`并`project.json`而无需第二个现在正确地生成项目生成操作- [1122年](https://github.com/NuGet/Home/issues/1122)
* 如果链接或位于不同的文件夹的正确查找 app.config 文件[1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)
* UWP 项目现在可以安装取消列出的包- [1109年](https://github.com/NuGet/Home/issues/1109)
* 当解决方案处于不处于已保存的状态-现在允许包还原[1081年](https://github.com/NuGet/Home/issues/1081)

处理的配置文件已更正的更新：

* 从在后续版本中的包不能再删除目标文件传送`project.json`托管的项目- [1288年](https://github.com/NuGet/Home/issues/1288)
* 在 ASP.NET 5 解决方案生成的过程不能再修改 Nuget.Config 文件[1201年](https://github.com/NuGet/Home/issues/1201)
* 允许在包更新的过程不能再更改版本约束[1130年](https://github.com/NuGet/Home/issues/1130)
* 锁定文件现在保持锁定状态期间生成的[1127年](https://github.com/NuGet/Home/issues/1127)
* 现在修改`packages.config`并不在更新的过程中重写该[585](https://github.com/NuGet/Home/issues/585)

与 TFS 源代码管理的交互得到改进：

* 不能再失败的包的绑定到 TFS 的安装[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)
* 更正了的 NuGet 用户界面，以允许 TFS 2013 集成- [1071年](https://github.com/NuGet/Home/issues/1071)
* 更正了对已还原到正确来自的 packages 文件夹中的包的引用[1004年](https://github.com/NuGet/Home/issues/1004)

最后，我们还改进了这些项：

* 日志消息的详细级别可以减少`project.json`托管项目- [1163年](https://github.com/NuGet/Home/issues/1163)
* 现在，正确的用户界面中显示安装的包版本[1061年](https://github.com/NuGet/Home/issues/1061)
* 现在指定其 nuspec 中的依赖项范围的包具有稳定的包版本-安装这些依赖项的预发布版本[1304年](https://github.com/NuGet/Home/issues/1304)

可以在 NuGet GitHub 中找到 Visual Studio 扩展的已解决的问题的完整列表[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>已知问题

我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)