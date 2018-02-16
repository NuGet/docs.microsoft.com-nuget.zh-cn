---
title: "NuGet 2.7 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.7 的发行说明。"
keywords: "NuGet 2.7 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 43638626661ae034bb0a1cc28958a2e2929f047f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 发行说明

[NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)

NuGet 2.7 已于 2013 年 8 月 22 日发布。

## <a name="acknowledgements"></a>致谢

我们真诚地感谢以下外部参与者的 NuGet 2.7 进行重大贡献：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 显示许可证 url 时详细列出包和详细级别。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [# 1956年](http://nuget.codeplex.com/workitem/1956)-developmentDependency 将特性添加到`packages.config`和命令中使用它包以仅包括运行时包
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - 避免 nuget.exe 包命令中的重复属性键。
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [# 2610年](http://nuget.codeplex.com/workitem/2610)-机缓存大小增加到 200。
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修复 NuGet 对话框的错误选项卡中显示更新
    - 修复 Project.TargetFramework 可以为 null ProjectManager 中
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修复 SharedPackageRepository FindPackage/FindPackagesById 上不存在 packageId 将失败
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -启用对 Nomad 项目的支持
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -修复推送命令将会失败，退出代码 0，当文件不存在。
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -使用项目引用数据库项目时添加 BindingRedirect 命令修复 bug。
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 2891年](http://nuget.codeplex.com/workitem/2891)-修复 bug 的 nuget.pack 错误地解析排除属性中的通配符。
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -修复 bug`NuGet.targets`未通过 $(Platform) 到 nuget.exe 还原包时。
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -这将允许将具有相同名称但不同大小写，最终导致"项已存在"异常的文件添加 nuget.exe 包命令中的修复 bug。
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [# 2990年](http://nuget.codeplex.com/workitem/2990)-NetPortableProfile 类添加版本属性。
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -如果修复 bug NullReferenceException requireApiKey = true，但标头 X NUGET APIKEY 不存在
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -修复 NuGet.Build 目标文件到，以便它新平台上正常工作 MonoDevelop
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - 通过增加并行化提高还原命令性能

## <a name="notable-features-in-the-release"></a>发行版中的值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>默认情况下，（具有隐式同意） 的程序包还原

NuGet 2.7 引入了一种新方法来打包还原，并且还克服了主要障碍： 现在，包还原同意默认情况下处于启用 ！ 新的方法和隐式同意的组合将极大地简化包还原方案。

#### <a name="implicit-consent"></a>隐式同意

使用 NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6，用户需要显式允许 NuGet 下载缺少的程序包期间生成。 如果此许可实际上并没有显式授予，则必须启用程序包还原的解决方案将无法生成，直至用户具有向授予许可。

从 NuGet 2.7 开始，包还原同意的情况下为 ON 默认情况下同时显式允许用户*选择退出*的程序包还原，如果需要，使用 Visual Studio 中的 NuGet 的设置中的复选框。 隐式同意此更改影响 NuGet 在以下环境：

* Visual Studio 2013 预览版
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 命令行实用工具

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的包自动还原

从 NuGet 2.7 开始，NuGet 将自动下载缺少的程序包在 Visual Studio 中，在生成期间即使程序包还原尚未显式启用解决方案。 此自动包还原发生在 Visual Studio 中，在生成项目或解决方案，但之前调用 MSBuild。 这将生成几个明显的好处：

1. 不再需要对解决方案中使用"启用 NuGet 包还原"笔势
1. 项目无需进行修改，NuGet 不会对你的项目以确保启用程序包还原进行更改
1. 将还原所有 NuGet 包，包括那些包含 MSBuild 属性中的目标文件的导入*之前*调用 MSBuild 时，确保这些属性/目标正确识别生成过程

若要在 Visual Studio 中使用自动程序包还原，只需执行一个操作 （中）：

1. 未签入你`packages`文件夹

有几种方法忽略你`packages`从源代码管理文件夹。 有关详细信息，请参阅[包和源控件](../consume-packages/packages-and-source-control.md)主题。

当所有用户隐式选择了参加自动包还原同意的情况下，你可以轻松地选择退出计划通过 Visual Studio 中的包管理器设置。

![程序包管理器设置](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>从命令行的简化的程序包还原

NuGet 2.7 引入 nuget.exe 的新功能： `nuget.exe restore`

此新的 Restore 命令允许你轻松地通过接受的解决方案文件或文件夹作为自变量来还原使用单个命令，解决方案的所有包。 此外，在当前文件夹中没有单个解决方案时，会进行隐式该自变量。 这意味着所有以下各项工作从包含单个解决方案文件 (MySolution.sln) 的文件夹：

1. nuget.exe restore MySolution.sln
1. nuget.exe 还原。
1. nuget.exe 还原

Restore 命令将打开的解决方案文件并找到解决方案中的所有项目。 在这里，它将查找`packages.config`为每个项目和还原的所有包找到的文件。 它还将还原的解决方案级包中找到`.nuget\packages.config`文件。 有关新的 Restore 命令的详细信息可在[命令行参考](../tools/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的包还原工作流

很高兴有关这些更改对包还原，因为它引入了新的工作流。 如果你想要忽略从源代码管理包你只需不要分配出`packages`文件夹。 打开并生成解决方案的 visual Studio 用户会自动还原的包。 对于命令行生成，只需调用`nuget.exe restore`之前调用`msbuild`。 不再需要请记得对解决方案，使用"启用 NuGet 包还原"笔势，并且我们将不再需要修改你的项目以 alter 生成。 这还会生成包含 MSBuild 的导入，尤其是通过 NuGet 的最新功能添加导入的包提供大大提高的体验和[自动导入属性/目标文件](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 文件夹中。

除了我们已完成自己工作，我们还致力于与某些重要的合作伙伴，为了使这种新方法。我们不是具体的时间线为其中的任何未知的但每个伙伴是因为我们有关新的方法非常高兴。

* Team Foundation Service-它们正在努力将集成到调用`nuget.exe restore`到默认值生成方案。
* Windows Azure 网站-它们正在努力，可以将你的项目推送到 Azure，并且具有`nuget.exe restore`调用之前生成您的网站。
* TeamCity-它们正在更新以其 NuGet 安装程序插件获得 TeamCity 8.x
* 他们正在处理 AppHarbor-若要允许您将你的存储库推送到 AppHarbor 并使`nuget.exe restore`生成你的解决方案之前调用。

与每个上述伙伴，它们将使用其自己的 nuget.exe 的副本并不需要执行 nuget.exe 解决方案中。

#### <a name="known-issues"></a>已知问题

出现了两个已知的问题 nuget.exe 还原初始 2.7 版本中，但它们已固定到更新的 9/6/2013年上[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)。  此更新，还可以在[NuGet 2.7 下载页](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。  运行`nuget.exe update -self`将更新到最新版本。

固定了：

1. [使用 SLN 文件时，新的程序包还原不能在 Mono](https://nuget.codeplex.com/workitem/3596)
1. [新的程序包还原不能使用 Wix 项目](https://nuget.codeplex.com/workitem/3598)

此外，还有新的包还原工作流的已知的问题，由此[自动包还原并不适用于解决方案文件夹下的项目](https://nuget.codeplex.com/workitem/3625)。 在 NuGet 2.7.1 中进行了修复此问题。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>项目重定目标和升级生成错误/警告

多次重定目标或升级你的项目之后, 你找到一些 NuGet 程序包不正常。 遗憾的是，没有这不会指示，然后不提供的指导上没有解决方法。 使用 NuGet 2.7，我们现在使用某些 Visual Studio 事件识别已重定目标或升级而影响你已安装的 NuGet 包中的项目时。

如果我们检测到的任何你的包已受重定目标或升级，我们将生成立即生成错误，告知你。 除了立即生成错误，我们还保留`requireReinstallation="true"`中标记出来。 你`packages.config`文件适用于 Visual Studio 中的所有程序包都是受影响的重定目标，并且每个后续都生成将会引发这些包的都生成警告。

尽管 NuGet 无法执行自动操作以重新安装受影响的包，我们希望这种指示和警告将指导帮助您发现何时需要重新安装包。 我们还致力于[包重新安装指南文档](../consume-packages/reinstalling-and-updating-packages.md)这些错误消息将定向到你。

### <a name="nuget-configuration-defaults"></a>NuGet 配置默认值

许多公司内部，使用 NuGet，但有引导其开发人员可以使用内部包源，而不是 nuget.org 硬时间。NuGet 2.7 引入了一种允许计算机范围的默认值为指定的配置默认值功能：

1. 已启用的程序包源
1. 已注册，但已禁用的包源
1. 默认 nuget.exe 推送源

其中每个现在可以配置在一个文件位于内`%ProgramData%\NuGet\NuGetDefaults.Config`。 如果此配置文件指定包源，则将不会自动注册的默认 nuget.org 包源中与的`NuGetDefaults.Config`将改为注册。

虽然不需要使用此功能，我们预期公司部署`NuGetDefaults.Config`使用组策略文件。

*请注意，此功能将永远不会导致包源以为从开发人员 NuGet 设置中删除。这意味着如果开发人员已使用 NuGet，并因此具有 nuget.org 包源注册，它也不会删除创建后`NuGetDefaults.Config`文件。*

请参阅[NuGet 配置的默认值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)有关此功能的详细信息。

### <a name="renaming-the-default-package-source"></a>重命名默认的程序包源

NuGet 始终注册了名为"NuGet 正式程序包源"，指向 nuget.org 一个默认包源。该名称详细，且它还未指定实际上指向。 若要解决这些两个问题，我们已重命名只需"nuget.org"在 UI 中为此包源。 包源的 URL 也进行了更改以包括"www"。 前缀。 使用 NuGet 2.7 之后, 你现有的"NuGet 正式程序包源"将自动更新到"nuget.org"作为其名称和"https://www.nuget.org/api/v2/"作为其 URL。

### <a name="performance-improvements"></a>性能改进

我们在 2.7 其会生成较小的内存需求量、 更少的磁盘使用情况和更快的包安装进行了一些性能改进。 我们还对基于 OData 的源，这将减少总体负载进行了更智能的查询。

### <a name="new-extensibility-apis"></a>新扩展性 Api

我们将一些新 Api 添加到我们的扩展性服务以填充的缺少的功能在早期版本的差距。

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>仅限开发的依赖关系

此功能由提供[Adam Ralph](https://twitter.com/adamralph)并且它允许程序包作者以声明依赖项仅在开发使用时间，而不需要包的依赖项。 通过添加`developmentDependency="true"`到中的包属性`packages.config`，`nuget.exe pack`不再包括作为依赖项包。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>删除 Visual Studio 2010 Express 适用于 Windows Phone 支持

2.7 中的新包还原模型由新 VSPackage 不同于主要的 NuGet VSPackage 的实现。 由于技术问题，此新 VSPackage 不正确在适用*Visual Studio 2010 Express 为 Windows Phone* SKU 为我们共享相同的基本代码与其他支持 Visual Studio Sku。 因此，从 NuGet 2.7 开始，我们删除支持*Visual Studio 2010 Express 为 Windows Phone*来自已发布的扩展插件。 支持*Visual Studio 2010 Express for Web*仍包含在主扩展发布到 Visual Studio 扩展库中。

因为我们不确定如何许多开发人员仍在使用该版本/版本的 Visual Studio 中 NuGet，我们发布专门为这些用户单独的 Visual Studio 扩展和发布上 CodePlex （而不是 Visual Studio 扩展库）. 我们不打算继续保持该扩展，但如果这会影响你通过在 CodePlex 上填写问题来请让我们知道。

若要下载 NuGet 包管理器 （Visual Studio 2010 Express 为 Windows Phone)，请访问[NuGet 2.7 下载](https://nuget.codeplex.com/releases/view/107605)页。

### <a name="bug-fixes"></a>Bug 修复

除了这些功能，此版本的 NuGet 还包括许多其他 bug 修复。 出现了 97 总问题在版本中解决。 有关工作的完整列表项固定在 NuGet 2.7，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
