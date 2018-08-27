---
title: NuGet 常见问题解答
description: 在命令行和 Visual Studio 中使用 NuGet 以及使用 NuGet 库的常见问题。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 3fe59ef03632053182b034052e93a5f2e6f444bd
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792936"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 常见问题

运行 NuGet 有哪些要求？

[安装指南](../install-nuget-client-tools.md)中提供了有关 UI 和命令行工具的所有信息。

NuGet 是否支持 Mono？

命令行工具 `nuget.exe` 在 Mono 3.2+ 下生成和运行，并且可以在 Mono 中创建包。

尽管 `nuget.exe` 在 Windows 上可充分发挥功能，但用于 Linux 和 OS X 时则存在已知问题。请参阅 GitHub 上的 [Mono 问题](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。

[图形化客户端](https://github.com/mrward/monodevelop-nuget-addin)以 MonoDevelop 外接程序的形式提供。

如何确定包的内容及其是否适用于应用程序？

了解包的主要来源为 nuget.org（或其他私有源）上的包清单页。 nuget.org 上的每个包页面都包含包的说明、其版本历史记录和使用情况统计信息。 包页面中的“信息”部分还包含项目网站的链接，此网站通常提供大量实例和其他文档，帮助你了解包的使用方法。

有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)。

## <a name="nuget-in-visual-studio"></a>Visual Studio 中的 NuGet

**NuGet 在不同 Visual Studio 产品中的受支持情况**

- Windows 版 Visual Studio 支持[包管理器 UI](../tools/package-manager-ui.md) 和[包管理器控制台](../tools/package-manager-console.md)。
- Visual Studio for Mac 具有内置 NuGet 功能，如[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)中所述。
- Visual Studio Code（所有平台）与 NuGet 不存在任何直接集成。 请使用 [NuGet CLI](../tools/nuget-exe-cli-reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。
- Visual Studio Team Services 提供[还原 NuGet 包的生成步骤](/vsts/build-release/tasks/package/nuget)。 还可以[在 Team Services 上托管私有 NuGet 包源](https://www.visualstudio.com/docs/package/nuget/publish)。

**如何查看安装的 NuGet 工具的确切版本？**

在 Visual Studio 中，请使用“帮助”>“关于 Microsoft Visual Studio”命令，然后查看“NuGet 包管理器”旁显示的版本。

或者，启动“包管理器控制台”（“工具”>“NuGet 包管理器”>“包管理器控制台”），输入 `$host`，然后查看包括版本信息在内的 NuGet 的相关信息。

NuGet 支持哪些编程语言？

NuGet 旨在将 .NET 库引入项目，通常适用于 .NET 语言。 由于 NuGet 还在某些项目类型中支持 MSBuild 和 Visual Studio 自动化，因此它也在不同程度上支持其他项目和语言。

最新版 NuGet 支持 C#、Visual Basic、F#、WiX 和 C++。

NuGet 支持哪些项目模板？

NuGet 对多种项目模板提供完整支持，如 Windows、Web、Cloud、SharePoint 和 Wix 等。

如何更新 Visual Studio 模板中的包？

在包管理器 UI，转到“更新”选项卡，选择“全部更新”；或者使用包管理控制台中的 [`Update-Package` 命令](../tools/ps-ref-update-package.md)。

若要更新模板本身，则需要手动更新模板存储库。 请参阅与该主题相关的 [Xavier Decoster 博客](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。 请注意，此操作的风险由自己承担，因为如果所有依赖项的最新版本不相互兼容，手动更新可能会损坏该模板。

是否可以在 Visual Studio 之外使用 NuGet？

可以，NuGet 可直接在命令行中使用。 请参阅[安装指南](../install-nuget-client-tools.md)和 [CLI 参考](../tools/nuget-exe-cli-reference.md)。

## <a name="nuget-command-line"></a>NuGet 命令行

如何获取最新版本的 NuGet 命令行工具？

请参阅[安装指南](../install-nuget-client-tools.md)。

**nuget.exe 的许可证是什么？**

可以根据 MIT 许可条款重新分发 nuget.exe。 你有责任更新和维护你选择重新分发的所有 nuget.exe 副本。

是否可以扩展 NuGet 命令行工具？

是的，可以向 `nuget.exe` 添加自定义命令，如 [Rob Reynold 博客](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet 包管理器控制台（Windows 版 Visual Studio）

如何在包管理器控制台中访问 DTE 对象？

Visual Studio 自动化对象模型中的顶层对象称为 DTE （开发工具环境）对象。 控制台通过名为 `$DTE` 的变量提供此对象。 有关详细信息，请参阅 Visual Studio 扩展性文档中的[自动化模型概述](/visualstudio/extensibility/internals/automation-model-overview)。

我尝试将 $DTE 变量强制转换为类型 DTE2，但出现错误：无法将类型“EnvDTE.DTEClass”的“EnvDTE.DTEClass”值转换为类型“EnvDTE80.DTE2”。为什么会这样？

这是 PowerShell 与 COM 对象交互的已知问题。 请尝试如下方法：

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` 是 NuGet PowerShell 主机添加的帮助程序函数。

## <a name="creating-and-publishing-packages"></a>创建和发布包

如何在源中列出我的包？

请参阅[创建和发布包](../quickstart/create-and-publish-a-package.md)。

我有面向不同版本的 .NET Framework 的多个版本的库。如何才能生成一个支持此方案的包？

请参阅[支持多个 .NET Framework 版本和配置文件](../create-packages/supporting-multiple-target-frameworks.md)。

如何设置自己的存储库或源？

请参阅[托管包概述](../hosting-packages/overview.md)。

如何将包批量上传到我的 NuGet 源？

请参阅[批量发布 NuGet 包](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。

## <a name="working-with-packages"></a>使用包

项目级包和解决方案级包之间有何差异？

解决方案级包 (NuGet 3.x+) 只需在解决方案上安装一次，随后即可用于该解决方案中的所有项目。 项目级包需在使用它的每个项目中进行安装。 解决方案级包还可以安装可从包管理器控制台中调用的新命令。

是否可以在没有 Internet 连接时安装 NuGet 包？

可以，请参阅 Scott Hanselman 的博客文章 [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)（如何在 nuget.org 不可用（或用户在飞机上）时访问 NuGet）(hanselman.com)。

如何在默认包文件夹以外的其他位置安装包？

请使用 `nuget config -set repositoryPath=<path>` 设置 `Nuget.Config` 中的 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 设置。

如何避免将 NuGet 包文件夹中添加到源代码管理中？

请将 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 设置为 `true`。 此密钥适用于解决方案级别，因此需要添加到 `$(Solutiondir)\.nuget\Nuget.Config` 文件中。 从 Visual Studio 中启用包还原将自动创建此文件。

如何关闭包还原？

请参阅[启用和禁用包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。

安装具有远程依赖项的本地包时，为何会出现“无法解析依赖项”错误？

将本地包安装到项目中时，需要选择“所有”源。 这样可以聚合所有源，而不只是一个源。 本地存储库用户通常不希望因为公司政策而意外安装远程包，因此才会出现此错误。

如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 文件？

对于各个项目位于单独文件夹中的大多数项目，用户不必考虑此问题，因为 NuGet 会识别每个项目中的 `packages.config` 文件。 如果使用 NuGet 3.3+ 并且同一文件夹中有多个项目，可将项目名称插入 `packages.config` 文件名（使用 `packages.{project-name}.config` 模式），然后 NuGet 将使用该文件。

使用 PackageReference 时不必考虑此问题，因为每个项目文件仅包含自己的依赖项列表。

存储库列表中未显示 nuget.org，应如何让其重新显示？

- 将 `https://api.nuget.org/v3/index.json` 添加到源列表；或
- 删除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 并指示 NuGet 重新创建它。

如果包未提供特定许可信息，有哪些默认许可条款？

每个包都需要受包中所含条款约束。 你应该在访问、下载或获取任何包前查看适用条款。 在 nuget.org 中，请使用包页面中的“许可信息”链接。

如果包未指定许可条款，请直接通过 nuget.org 包页面上的“联系所有者”链接与包所有者联系。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

## <a name="managing-packages-on-nugetorg"></a>在 nuget.org 上管理包

在上传包元数据后是否可以再对其进行编辑？

NuGet 建议对所有的包签名。 包签名的设计原则是已签名包的内容不得改变，nuspec 也包括在内。 编辑包元数据会使 nuspec 发生更改，导致现有签名无效。 我们建议在创建包后修改现有工作流，这样则无需编辑包元数据。

请注意，列出的包依赖项从包本身自动生成，并且无法进行编辑。

此外，要测试和验证包，同时不在公共库中提供此包，最好将包上传到 [staging.nuget.org](http://staging.nuget.org)。

是否可以为以后发布的包预留名称？

可以。 通过为帐户请求包 ID 前缀可以在 [nuget.org](https://www.nuget.org/) 中预留包 ID。 若要请求包 ID 前缀，请按照[文档](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)中的说明操作。

如何声明包的所有权？

请参阅[在 nuget.org 上管理包所有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。

如何与违反我的软件许可的包所有者进行交涉？

我们鼓励 NuGet 社区合作解决包所有者和其他软件所有者之间可能出现的任何争议。 我们制定了周密的[争议解决流程](../policies/dispute-resolution.md)，要求 nuget.org 管理员调解之前应遵循此流程。

是否建议将测试包上传到 nuget.org？

对于测试目的，可以使用 [staging.nuget.org](http://staging.nuget.org)，或使用备用的公共 NuGet 服务器，如 [myget.org](https://myget.org) 或 [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。

请注意，上传到 staging.nuget.org 的包可能不会保留。 请参阅[告别预览版](http://blog.nuget.org/20130419/goodbye-preview.html)。

可上传到 nuget.org 的最大包大小是多少？

nuget.org 允许的最大包大小为 250 MB，但我们建议尽可能将包保持在 1 MB 以下，通过依赖项将包链接在一起。 依据经验，仅包含一个程序集的包可以避免冲突。

NuGet 使用 HTTP 下载包，因此较大包比较小包有更高的安装失败风险。

依赖项可以在多个包之间进行共享，这样可减小 NuGet 包使用者的总下载大小。

依赖项通常是静态的，永远不会更改。 修复代码中的 bug 时，可能无需更新依赖项。 如果捆绑依赖项，最终将导致每一次都需要重新传输更大的包。 通过将 NuGet 包拆分成相关的依赖项，包使用者可以获得更细化的更新。

## <a name="nugetorg-not-accessible"></a>nuget.org 不可访问

为何无法从 nuget.org 下载包或向其中上传包？

首先，请确保使用的是最新版本的 NuGet。 如果该版本仍然失败，请[联系支持人员](https://www.nuget.org/policies/Contact)，并提供其他连接故障排除信息，包括：

- 使用的 NuGet 版本
- 使用的包源
- 详细还原日志
- MTR 或 Fiddler 跟踪（见下文）
- 所在地理区域
- 操作系统版本
- 计算机配置（CPU、网络、硬盘驱动器）
- 计算机是否设置了代理或防火墙
- 计算机上安装的 .NET 版本
- 使用的跨平台工具（如 .NET CLI 或 DNU）的版本

捕获 MTR：

- 从 [http://winmtr.net/download/](http://winmtr.net/) 下载 WinMTR
- 输入 `api.nuget.org` 作为主机名，然后单击“启动”。
- 等待，直到“已发送”列 >= 100。

    ![捕获 MTR](media/mtr.png)

- 将文本复制到剪贴板。

捕获 Fiddler：

- 安装最新版本的 [Fiddler](http://www.telerik.com/download/fiddler)。
- 启动 Fiddler，使用“文件”>“捕获流量”菜单禁用捕获流量。
- 删除所有会话（选中列表中的所有项，按 Delete 键）。
- 配置 Fiddler 以捕获 HTTPS 流量，具体操作方式为：打开“工具”>“Fiddler 选项...”菜单，勾选“HTTPS”选项卡中的“解密 HTTPS 流量”。
- 关闭 Visual Studio。
- 启用“文件”>“捕获流量”菜单。
- 启动 Visual Studio 或 nuget.exe.exe，执行当前未运行的操作。 Fiddler 中应显示出这些操作所产生的流量。
- 操作运行结束后，使用“文件”>“保存”>“所有会话”来存储捕获的会话。

注意：若要通过 Fiddler 路由 NuGet，可能需要将 `HTTP_PROXY` 环境变量设置为 `http://127.0.0.1:8888`。

如果该操作失败，请尝试[该 StackOverflow 文章中提到的方法](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。

有哪些适用于 nuget.org 的 API 终结点？

V3：`https://api.nuget.org/v3/index.json` V2：`https://www.nuget.org/api/v2/`（请注意，V2 API 已弃用并且不适用于 NuGet 4+。）
