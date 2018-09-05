---
title: NuGet 2.7 发行说明
description: 发行说明适用于 NuGet 2.7 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550960"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 发行说明

[NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)

NuGet 2.7 已于 2013 年 8 月 22 日发布。

## <a name="acknowledgements"></a>致谢

我们要特别感谢的重要贡献到 NuGet 2.7 以下外部参与者：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 显示许可证 url 时详细列出的包和详细级别。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [# 1956年](http://nuget.codeplex.com/workitem/1956)-添加到 developmentDependency 属性`packages.config`和 pack 命令中使用仅包含运行时包
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - 避免在 nuget.exe pack 命令中的重复属性键。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [# 2610年](http://nuget.codeplex.com/workitem/2610)-机缓存大小增加到 200。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修复 NuGet 对话框中错误选项卡显示更新
    - 修复 Project.TargetFramework 可以为 null ProjectManager 中
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修复 SharedPackageRepository FindPackage/FindPackagesById 上不存在包 Id 将会失败
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -启用对 Nomad 项目的支持
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -修复推送命令失败，并退出代码 0，当文件不存在。
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -使用项目引用数据库项目时添加 BindingRedirect 命令修复 bug。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 2891年](http://nuget.codeplex.com/workitem/2891)-修复 bug 的 nuget.pack 错误地分析 exclude 属性中的通配符。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -修复 bug`NuGet.targets`未通过 $ （platform） 到 nuget.exe 还原包时。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe package 命令，以允许添加具有相同名称但大小写不同，最终导致出现"已存在项"异常的文件中的修复 bug。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [# 2990年](http://nuget.codeplex.com/workitem/2990)-NetPortableProfile 类添加版本属性。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -如果修复 bug NullReferenceException requireApiKey = true，但标头 X NUGET APIKEY 不存在
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -修复了 NuGet.Build 目标文件到，以便其正常运行 monodevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - 通过增加并行化提高还原命令性能

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>默认情况下 （与隐式同意） 的包还原

NuGet 2.7 引入了一种新方法以包还原，并且还克服了主要障碍： 现在，包还原同意的情况下默认情况下为打开 ！ 新的方法和隐式许可的组合将极大地简化了包还原方案。

#### <a name="implicit-consent"></a>隐式同意

使用 NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6 中，用户需要显式允许 NuGet 下载缺失的包期间构建。 如果此许可不具有显式授予，则必须启用包还原的解决方案将无法生成，直至已向用户授予许可。

从 NuGet 2.7 开始，包还原同意的情况下为 ON 默认情况下同时允许用户显式*选择退出*的包还原，如果需要，使用 Visual Studio 中的 NuGet 的设置中的复选框。 隐式同意此更改影响在以下环境中的 NuGet:

* Visual Studio 2013 预览版
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 命令行实用程序

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的自动包还原

从 NuGet 2.7 开始，NuGet 将自动下载缺少的包在 Visual Studio 中，在生成期间即使包还原未显式启用的解决方案。 此进行自动包还原在 Visual Studio 中生成项目或解决方案，但之前调用 MSBuild。 这会生成几个重要优点：

1. 不再需要在解决方案上使用"启用 NuGet 包还原"手势
1. 项目无需进行修改，NuGet 不会对你的项目以确保启用包还原进行更改
1. 将还原所有 NuGet 包，包括那些包含 MSBuild 属性/目标文件的导入*之前*MSBuild 调用，确保在生成过程正确识别这些属性/目标

若要在 Visual Studio 中使用自动包还原，只需选择一个操作 （中）：

1. 不签入你`packages`文件夹

有几种方法，以忽略此参数在`packages`从源代码管理文件夹。 有关详细信息，请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)主题。

虽然所有用户都是隐式选择加入自动包还原同意的情况下，您可以轻松地选择退出通过 Visual Studio 中的包管理器设置。

![包管理器设置](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>从命令行中的简化的包还原

NuGet 2.7 引入了 nuget.exe 的新功能： `nuget.exe restore`

此新的还原命令，可轻松通过接受的解决方案文件或文件夹作为参数来还原所有包使用单个命令的解决方案。 此外，当在当前文件夹中只有一个单一的解决方案时，则暗指该参数。 这意味着所有以下各项都工作从包含单个解决方案文件 (MySolution.sln) 的文件夹：

1. nuget.exe 还原 MySolution.sln
1. nuget.exe 还原。
1. nuget.exe 还原

Restore 命令将打开解决方案文件并查找解决方案中的所有项目。 在这里，它将查找`packages.config`的每个项目和找到的所有包还原的文件。 它还将还原解决方案级别包中找到`.nuget\packages.config`文件。 有关新的还原命令的详细信息可在[命令行参考](../tools/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的包还原工作流

我们很高兴有关包还原，这些更改，因为它引入了新的工作流。 如果你想要忽略从源代码管理包，只需不提交`packages`文件夹。 打开并生成解决方案的 visual Studio 用户将看到自动还原包。 对于命令行生成，只需调用`nuget.exe restore`然后再调用`msbuild`。 不再需要记得在解决方案上使用"启用 NuGet 包还原"笔势和我们不再需要修改您要更改生成的项目。 这还会生成包含 MSBuild 的导入，尤其是通过 NuGet 的最新功能添加的导入的包的大大改进的体验并[自动导入属性/目标文件](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 文件夹中。

除了我们已完成自己的工作，我们还正在使用一些重要合作伙伴以完善您的这种新方法。我们尚无具体的时间线有这些，但每个伙伴是我们有关的新方法一样兴奋不已。

* Team Foundation Service-他们正在努力将集成到调用`nuget.exe restore`到默认生成方案。
* Windows Azure 网站-他们正在努力，可以将你的项目推送到 Azure 和具有`nuget.exe restore`构建您的网站之前调用。
* TeamCity-它们为 TeamCity 更新其 NuGet 安装程序插件 8.x
* AppHarbor-他们正在努力，可以将你的存储库推送到 AppHarbor 和具有`nuget.exe restore`生成你的解决方案之前调用。

与每个上述合作伙伴，它们将使用其自己的 nuget.exe 的副本并不需要在解决方案中执行 nuget.exe。

#### <a name="known-issues"></a>已知问题

使用 nuget.exe 还原初始 2.7 版本中，两个已知问题，但它们已修复 9/6/2013 到的更新[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)。  此更新，还可以在[NuGet 2.7 下载页](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。  运行`nuget.exe update -self`将更新到最新版本。

固定了：

1. [新的包还原时使用 SLN 文件不能在 Mono 上](https://nuget.codeplex.com/workitem/3596)
1. [新的包还原不使用 Wix 项目](https://nuget.codeplex.com/workitem/3598)

此外，还有新的包还原工作流的已知的问题，由此[自动包还原并不适用于解决方案文件夹下的项目](https://nuget.codeplex.com/workitem/3625)。 NuGet 2.7.1 中修复此问题。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>项目重定向和升级生成错误/警告

很多时候后重定向或升级你的项目，您发现一些 NuGet 包不运行正常。 遗憾的是，不会指示此并且然后没有不提供的指导如何解决它。 NuGet 2.7，我们现在使用 Visual Studio 的某些事件时已重定向或升级你的项目会影响已安装的 NuGet 包的方式识别。

如果检测到您的包的任何受影响的重定向或升级，我们将生成即时生成错误，告知你。 除了即时生成错误，我们还保留`requireReinstallation="true"`标记中你`packages.config`文件适用于所有受影响的重定目标，且每个后续的包生成 Visual Studio 中将会引发这些包的生成警告。

尽管 NuGet 不能执行自动操作以重新安装受影响的包，我们希望此指示和警告将指导帮助您发现需要重新安装包。 我们还在努力[包重新安装指导文档](../consume-packages/reinstalling-and-updating-packages.md)这些错误消息定向到。

### <a name="nuget-configuration-defaults"></a>NuGet 配置默认值

许多公司都使用 NuGet 在内部，但很难将指导其开发人员而不是 nuget.org 使用内部包源。NuGet 2.7 引入了一种允许计算机范围默认设置，以便为指定的配置默认值功能：

1. 启用了的包源
1. 已注册，但禁用的包源
1. 默认 nuget.exe 推送源

其中每项功能现在可以配置在一个文件位于`%ProgramData%\NuGet\NuGetDefaults.Config`。 如果此配置文件指定包源，则默认 nuget.org 包源将不会自动注册和与中的`NuGetDefaults.Config`将改为注册。

虽然不需要使用此功能，但我们希望公司部署`NuGetDefaults.Config`使用组策略文件。

*请注意，此功能将永远不会导致要从开发人员的 NuGet 设置中删除的包源。这意味着如果开发人员已使用 NuGet，因此具有 nuget.org 包源注册，将不会删除在创建后`NuGetDefaults.Config`文件。*

请参阅[NuGet 配置默认](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)有关此功能的详细信息。

### <a name="renaming-the-default-package-source"></a>重命名默认包源

NuGet 始终注册了名为"NuGet 正式程序包来源"指向 nuget.org 一个默认包源。该名称为详细，它还没有指定实际上指向。 若要解决这些两个问题，我们已重命名为只需"nuget.org"UI 中此包源。 包源的 URL 也已更改为包括"www"。 前缀。 使用 NuGet 2.7 之后, 你现有的"NuGet 正式程序包来源"将自动更新为"nuget.org"作为其名称和"<https://www.nuget.org/api/v2/>"作为其 URL。

### <a name="performance-improvements"></a>性能改进

我们在其会生成较小的内存占用量、 更少的磁盘使用情况和更快的包安装 2.7 中所做改进性能。 我们还对基于 OData 的源，这将减少总体负载更智能的查询。

### <a name="new-extensibility-apis"></a>新扩展性 Api

我们添加一些新的 Api 到我们的可扩展性服务来弥补缺少的功能在以前的版本。

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

### <a name="development-only-dependencies"></a>仅开发依赖项

此功能已由提供[Adam Ralph](https://twitter.com/adamralph) ，并允许程序包作者以声明中仅用于开发的依赖项的时间，并且不需要包依赖项。 通过添加`developmentDependency="true"`属性中的包`packages.config`，`nuget.exe pack`将不再包含此包作为依赖项。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>删除对 Visual Studio 2010 Express for Windows Phone 支持

2.7 中新的包还原模型由新 VSPackage 不同于主要的 NuGet VSPackage 实现。 由于技术问题，此新 VSPackage 不会正常工作*Visual Studio 2010 Express 的 Windows Phone* SKU，因为我们共享相同的基本代码与其他受支持 Visual Studio Sku。 因此，从 NuGet 2.7 开始，我们将要删除的支持*Visual Studio 2010 Express 的 Windows Phone*从已发布的扩展。 为支持*Visual Studio 2010 Express for Web*仍包含在发布到 Visual Studio 扩展库的主扩展。

因为我们不确定有多少开发人员仍在使用该版本的 Visual Studio 在 NuGet，我们是发布单独的 Visual Studio 扩展专门为这些用户，并将其发布在 CodePlex （而不是 Visual Studio 扩展库）. 我们不打算继续保持该扩展，但如果这会影响你请让我们知道在 CodePlex 上提交问题。

若要下载 NuGet 包管理器 （适用于 Visual Studio 2010 Express 的 Windows Phone)，请访问[NuGet 2.7 下载](https://nuget.codeplex.com/releases/view/107605)页。

### <a name="bug-fixes"></a>Bug 修复

除了这些功能，此版本的 NuGet 还包括许多其他 bug 修复。 出现的版本中解决的 97 总问题。 有关工作的完整列表项中已修复 NuGet 2.7，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
