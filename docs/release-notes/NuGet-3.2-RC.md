---
title: NuGet 3.2 RC 发行说明
description: NuGet 3.2 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780294"
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC 发行说明

[NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)  | [NuGet 3.2 发行说明](../release-notes/nuget-3.2.md)

NuGet 3.2 候选发布版发布于9月2日2015，作为3.1.1 版本的改进和修复的集合。  此外，这些是第一次发布到新的 dist.nuget.org 存储库的版本。

## <a name="new-features"></a>新功能

* 位于同一文件夹中的项目现在可以 `project.json` 在该文件夹中具有特定于每个项目的不同文件。  对于每个项目，将文件命名为， `project.json` `{ProjectName}.project.json` NuGet 将正确引用并对每个项目正确使用该内容。  这支持新功能  [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` 现在支持 globalPackagesFolder 作为相对路径- [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>命令行更新

这是 nuget.exe 客户端的第一个版本，它支持 NuGet v3 服务器，并为使用文件管理的项目还原包 `project.json` 。

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>在此版本中解决了许多经过身份验证的源问题，以改善与客户端的交互。

* 安装/还原交互仅向经过身份验证的源的初始请求提交凭据- [1300](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)
* Push 命令不能解析配置中的凭据- [1248](https://github.com/NuGet/Home/issues/1248)
* 用户代理和标头现在已提交到 NuGet 存储库以帮助进行统计跟踪- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>我们进行了大量改进，以便在尝试使用远程 NuGet 存储库时更好地处理网络故障：

* 改善了无法连接到远程源时的错误消息- [1238](https://github.com/NuGet/Home/issues/1238)
* 更正了 NuGet restore 命令，以便在出现错误情况时正确返回 1- [1186](https://github.com/NuGet/Home/issues/1186)
* 现在，重试每个200毫秒的网络连接，在出现 HTTP 5xx 失败时最多执行5次尝试- [1120](https://github.com/NuGet/Home/issues/1120)
* 改进了推送命令期间服务器重定向响应的处理- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 现在支持作为参数的 Nuget.Config 中的 URL 或存储库名称- [1046](https://github.com/NuGet/Home/issues/1046)
* 还原期间缺少存储库中的程序包现在会报告为错误，而不是警告 [1038](https://github.com/NuGet/Home/issues/1038)
* 更正了针对 Unix/Linux 方案的 \r\n multipartwebrequest 处理- [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>有多个针对各种命令的问题的修补程序：

* 在针对包源进行 PUT 之前，推送命令不再执行 GET- [1237](https://github.com/NuGet/Home/issues/1237)
* List 命令不再重复版本号- [1185](https://github.com/NuGet/Home/issues/1185)
* 带有-build 参数的 Pack 现在正确支持 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107)
* 更正了尝试打包使用 Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)生成的 F # 项目的问题
* 如果包已存在，则立即还原为非 ops- [1040](https://github.com/NuGet/Home/issues/1040)
* 文件格式错误时改进的错误消息 `packages.config` - [1034](https://github.com/NuGet/Home/issues/1034)
* 使用开关更正了还原命令， `-SolutionDirectory` 以便使用相对路径- [992](https://github.com/NuGet/Home/issues/992)
* 改进了更新的命令来支持解决方案范围的更新- [924](https://github.com/NuGet/Home/issues/924)

此版本中解决的问题的完整列表可在 NuGet GitHub [命令行里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)中找到。

## <a name="visual-studio-extension-updates"></a>Visual Studio 扩展更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 中的新功能

* 已将新的上下文菜单项添加到 "解决方案" 节点上的解决方案资源管理器，这允许在不生成解决方案 ([1274](https://github.com/NuGet/Home/issues/1274)) 的情况下还原包。

![新的 "还原包" 上下文菜单项](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Visual Studio 中的更新和修补程序

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>经过身份验证的源的修补程序也会在扩展中汇总和寻址。  以下身份验证项目也在扩展中进行了说明：

* 现在正确地正确对待 NuGet v3 身份验证源，而不是作为 v2 身份验证源- [1216](https://github.com/NuGet/Home/issues/1216)
* 更正 `project.json` 了使用和与 v2 源通信的项目中身份验证凭据的请求- [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>网络连接已影响 Visual Studio 中的用户界面，我们通过以下修补程序解决了这一问题：

* 提高了包版本（ [1096](https://github.com/NuGet/Home/issues/1096) ）的本地缓存的维护
* 在连接到 v3 源时更改了失败行为，不再尝试将其视为 v2 源- [1253](https://github.com/NuGet/Home/issues/1253)
* 现在，在安装包含多个包源的包时阻止安装失败- [1183](https://github.com/NuGet/Home/issues/1183)

改进了对生成操作的交互处理：

* 如果为单个项目还原包失败，现在继续生成项目- [1169](https://github.com/NuGet/Home/issues/1169)
* 将包安装到由解决方案中其他项目依赖的项目中会强制解决方案重新生成- [981](https://github.com/NuGet/Home/issues/981)
* 更正了已失败的包安装以正确回滚对项目的更改- [1265](https://github.com/NuGet/Home/issues/1265)
* 更正了 `developmentDependency` `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)中对包的属性的意外删除
* 对的调用 `install.ps1` 现在传递了正确的 `$package.AssemblyReferences` 对象- [1245](https://github.com/NuGet/Home/issues/1245)
* 当项目处于错误状态时，不再阻止卸载 UWP 项目中的包- [1128](https://github.com/NuGet/Home/issues/1128)
* `packages.config`现在可正确生成包含和项目组合的解决方案， `project.json` 而无需进行第二次生成操作- [1122](https://github.com/NuGet/Home/issues/1122)
* 如果文件已链接或位于其他文件夹中，则正确查找 app.config 文件- [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)
* UWP 项目现在可以安装未列出的包- [1109](https://github.com/NuGet/Home/issues/1109)
* 当解决方案未处于保存状态时，现在允许使用包还原- [1081](https://github.com/NuGet/Home/issues/1081)


已更正处理配置文件的更新：

* 不再从托管项目的后续版本中删除包中提供的目标文件 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 解决方案版本期间不再修改 Nuget.Config 文件- [1201](https://github.com/NuGet/Home/issues/1201)
* 在包更新期间不再更改允许的版本约束- [1130](https://github.com/NuGet/Home/issues/1130)
* 锁定文件现在在生成期间保持锁定状态- [1127](https://github.com/NuGet/Home/issues/1127)
* 现在 `packages.config` ，在更新过程中修改和不重写此项- [585](https://github.com/NuGet/Home/issues/585)


与 TFS 源代码管理的交互经过改进：

* 对于绑定到 TFS- [1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)的包，不会再安装失败。
* 更正了 NuGet 用户界面以允许 TFS 2013 集成- [1071](https://github.com/NuGet/Home/issues/1071)
* 更正了对从包文件夹中正确还原的包的引用- [1004](https://github.com/NuGet/Home/issues/1004)

最后，我们还改进了以下各项：

* 针对托管项目减少的日志消息详细级别 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)
* 现在正确地在用户界面中显示包的安装版本- [1061](https://github.com/NuGet/Home/issues/1061)


有关 Visual Studio 扩展的问题的完整列表，请参阅 NuGet GitHub [3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>已知问题

我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)