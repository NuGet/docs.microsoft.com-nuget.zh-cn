---
title: NuGet 常见问题解答
description: 在命令行和 Visual Studio 中使用 NuGet 的常见问题和解答。
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999944"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 常见问题

有关 NuGet.org 相关常见问题（如 NuGet.org 帐户问题），请参阅[NuGet.org 常见问题解答](../nuget-org/nuget-org-faq.md)。

运行 NuGet 有哪些要求？ 

[安装指南](../install-nuget-client-tools.md)中提供了有关 UI 和命令行工具的所有信息。

NuGet 是否支持 Mono？ 

命令行工具 `nuget.exe` 在 Mono 3.2+ 下生成和运行，并且可以在 Mono 中创建包。

尽管 `nuget.exe` 在 Windows 上可充分发挥功能，但用于 Linux 和 OS X 时则存在已知问题。请参阅 GitHub 上的 [Mono 问题](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。

[图形化客户端](https://github.com/mrward/monodevelop-nuget-addin)以 MonoDevelop 外接程序的形式提供。

如何确定包的内容及其是否适用于应用程序？ 

了解包的主要来源为 nuget.org（或其他私有源）上的包清单页。 nuget.org 上的每个包页面都包含包的说明、其版本历史记录和使用情况统计信息。 包页面中的“信息”部分还包含项目网站的链接，此网站通常提供大量实例和其他文档，帮助你了解包的使用方法  。

有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)。

## <a name="nuget-in-visual-studio"></a>Visual Studio 中的 NuGet

**NuGet 在不同 Visual Studio 产品中的受支持情况**

- Windows 版 Visual Studio 支持[包管理器 UI](../consume-packages/install-use-packages-visual-studio.md) 和[包管理器控制台](../consume-packages/install-use-packages-powershell.md)。
- Visual Studio for Mac 具有内置 NuGet 功能，如[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)中所述。
- Visual Studio Code（所有平台）与 NuGet 不存在任何直接集成。 请使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 或 [dotnet CLI](../reference/dotnet-commands.md)。
- Azure DevOps 提供[还原 NuGet 包的生成步骤](/vsts/build-release/tasks/package/nuget)。 还可以[在 Azure DevOps 上托管私有 NuGet 包源](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。

**如何查看安装的 NuGet 工具的确切版本？**

在 Visual Studio 中，请使用“帮助”>“关于 Microsoft Visual Studio”命令，然后查看“NuGet 包管理器”旁显示的版本   。

或者，启动“包管理器控制台”（“工具”>“NuGet 包管理器”>“包管理器控制台”），输入 `$host`，然后查看包括版本信息在内的 NuGet 的相关信息  。

NuGet 支持哪些编程语言？ 

NuGet 旨在将 .NET 库引入项目，通常适用于 .NET 语言。 由于 NuGet 还在某些项目类型中支持 MSBuild 和 Visual Studio 自动化，因此它也在不同程度上支持其他项目和语言。

最新版 NuGet 支持 C#、Visual Basic、F#、WiX 和 C++。

NuGet 支持哪些项目模板？ 

NuGet 对多种项目模板提供完整支持，如 Windows、Web、Cloud、SharePoint 和 Wix 等。

如何更新 Visual Studio 模板中的包？ 

在包管理器 UI，转到“更新”选项卡，选择“全部更新”；或者使用包管理控制台中的 [`Update-Package` 命令](../reference/ps-reference/ps-ref-update-package.md)   。

若要更新模板本身，则需要手动更新模板存储库。 请参阅与该主题相关的 [Xavier Decoster 博客](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。 请注意，此操作的风险由自己承担，因为如果所有依赖项的最新版本不相互兼容，手动更新可能会损坏该模板。

是否可以在 Visual Studio 之外使用 NuGet？ 

可以，NuGet 可直接在命令行中使用。 请参阅[安装指南](../install-nuget-client-tools.md)和 [CLI 参考](../reference/nuget-exe-cli-reference.md)。

## <a name="nuget-command-line"></a>NuGet 命令行

如何获取最新版本的 NuGet 命令行工具？ 

请参阅[安装指南](../install-nuget-client-tools.md)。 若要检查当前安装的工具版本，请使用 `nuget help`。

**nuget.exe 的许可证是什么？**

可以根据 MIT 许可条款重新分发 nuget.exe。 你有责任更新和维护你选择重新分发的所有 nuget.exe 副本。

是否可以扩展 NuGet 命令行工具？ 

是的，可以向 `nuget.exe` 添加自定义命令，如 [Rob Reynold 博客](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet 包管理器控制台（Windows 版 Visual Studio）

如何在包管理器控制台中访问 DTE 对象？ 

Visual Studio 自动化对象模型中的顶层对象称为 DTE （开发工具环境）对象。 控制台通过名为 `$DTE` 的变量提供此对象。 有关详细信息，请参阅 Visual Studio 扩展性文档中的[自动化模型概述](/visualstudio/extensibility/internals/automation-model-overview)。

**尝试将 $DTE 变量强制转换为 DTE2 类型时出现错误：无法将“EnvDTE.DTEClass”类型的“EnvDTE.DTEClass”值转换为类型“EnvDTE80.DTE2”。** 为什么会这样？

这是 PowerShell 与 COM 对象交互的已知问题。 请尝试如下方法：

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` 是 NuGet PowerShell 主机添加的帮助程序函数。

## <a name="creating-and-publishing-packages"></a>创建和发布包

如何在源中列出我的包？ 

请参阅[创建和发布包](../quickstart/create-and-publish-a-package.md)。

我有面向不同版本的 .NET Framework 的多个版本的库。  如何才能生成一个支持此方案的包？

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

请参阅[启用和禁用包还原](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)。

安装具有远程依赖项的本地包时，为何会出现“无法解析依赖项”错误？ 

将本地包安装到项目中时，需要选择“所有”源  。 这样可以聚合所有源，而不只是一个源。 本地存储库用户通常不希望因为公司政策而意外安装远程包，因此才会出现此错误。

如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 文件？ 

对于各个项目位于单独文件夹中的大多数项目，用户不必考虑此问题，因为 NuGet 会识别每个项目中的 `packages.config` 文件。 如果使用 NuGet 3.3+ 并且同一文件夹中有多个项目，可将项目名称插入 `packages.config` 文件名（使用 `packages.{project-name}.config` 模式），然后 NuGet 将使用该文件。

使用 PackageReference 时不必考虑此问题，因为每个项目文件仅包含自己的依赖项列表。

存储库列表中未显示 nuget.org，应如何让其重新显示？ 

- 将 `https://api.nuget.org/v3/index.json` 添加到源列表；或
- 删除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 并指示 NuGet 重新创建它。
