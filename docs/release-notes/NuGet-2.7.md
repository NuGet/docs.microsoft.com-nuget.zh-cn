---
title: NuGet 2.7 发行说明
description: NuGet 2.7 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780389"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 发行说明

[NuGet 2.6.1 For WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)  | [NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)

NuGet 2.7 于8月 22 2013 日发布。

## <a name="acknowledgements"></a>致谢

我们想感谢以下外部参与者对 NuGet 2.7 的重大贡献：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss)) 
    - 列出包时显示许可证 url，详细信息详细说明。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - [#1956](http://nuget.codeplex.com/workitem/1956) -将 developmentDependency 属性添加到 `packages.config` 中，并将其用于 pack 命令中，以仅包含运行时包
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael)) 
    - 避免 nuget.exe pack 命令中出现重复的属性键。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan)) 
    - [#2610](http://nuget.codeplex.com/workitem/2610) -将计算机缓存大小增加到200。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel)) 
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修复在错误的选项卡中显示更新的 NuGet 对话框
    - 修复项目。在 ProjectManager 中，TargetFramework 可以为 null
    - [#3248](http://nuget.codeplex.com/workitem/3248) 修复了不存在的 packageId 上的 SharedPackageRepository FindPackage/FindPackagesById 将失败
6. [古柯 Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland)) 
    - [#3234](http://nuget.codeplex.com/workitem/3234) -启用对 Nomad 项目的支持
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie)) 
    - 在文件不存在时， [#3252](http://nuget.codeplex.com/workitem/3252)修复推送命令失败，退出代码为0。
8. [圣马丁 Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -在项目引用数据库项目时使用 Add-BindingRedirect 命令修复 bug。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos)) 
    - [#2891](http://nuget.codeplex.com/workitem/2891) -修复 nuget 的 bug。不正确地对 "exclude" 特性中的通配符进行分析。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981)) 
     - [#3307](http://nuget.codeplex.com/workitem/3307) 修复 bug `NuGet.targets` 在还原包时，不会将 $ (平台) 传递到 nuget.exe。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) 修复 nuget.exe 包命令中的 bug，该命令允许添加名称相同但大小写不同的文件，最终导致 "项已存在" 异常。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu)) 
     - [#2990](http://nuget.codeplex.com/workitem/2990) -将版本属性添加到 NetPortableProfile 类。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -修复 bug NullReferenceException if requireApiKey = true，但标头 X-APIKEY 不存在
14. [迈克尔 Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism)) 
     - [#3278](https://nuget.codeplex.com/workitem/3278) -将 NuGet 版本文件修复为，以使其在 MonoDevelop 上正常工作
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km)) 
     - 通过提高并行度提高还原命令性能

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>默认情况下，包还原 (具有隐式同意) 

NuGet 2.7 引入了一种新的包还原方法，还克服了重大障碍：默认情况下，包还原许可已启用！ 新方法和隐式许可的组合可大大简化包还原方案。

#### <a name="implicit-consent"></a>隐式同意

对于 NuGet 版本2.0、2.1、2.2、2.5 和2.6，用户需要在生成过程中显式允许 NuGet 下载缺少的包。 如果未显式指定此许可，则已启用包还原的解决方案在用户授予同意之前无法生成。

从 NuGet 2.7 开始，默认启用包还原许可，同时允许用户在需要时使用 NuGet 的 "设置" 中的复选框明确 *选择退出* 包还原。 此隐式同意更改会影响以下环境中的 NuGet：

* Visual Studio 2013 预览版
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line 实用工具

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的自动包还原

从 NuGet 2.7 开始，NuGet 将在 Visual Studio 中生成期间自动下载缺少的包，即使未对该解决方案显式启用包还原也是如此。 在生成项目或解决方案时，但在调用 MSBuild 之前，将在 Visual Studio 中执行此自动包还原。 这产生了几个重要的好处：

1. 不再需要在解决方案中使用 "启用 NuGet 包还原" 手势
1. 不需要修改项目，并且 NuGet 不会对项目进行更改，以确保启用包还原
1. 所有 NuGet 包（包括包含属性/目标文件的 MSBuild 导入的文件）将在调用 MSBuild *之前* 还原，并确保在生成过程中正确识别这些属性/目标

若要在 Visual Studio 中使用自动包还原，只需在) 操作中执行一个 (：

1. 不签入您的 `packages` 文件夹

有多种方法可以 `packages` 从源代码管理中省略文件夹。 有关详细信息，请参阅 [包和源代码管理](../consume-packages/packages-and-source-control.md) 主题。

虽然所有用户都隐式选择自动包还原许可，但你可以轻松地通过 Visual Studio 中的包管理器设置进行选择。

![程序包管理器设置](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>从 Command-Line 简化包还原

NuGet 2.7 为 nuget.exe 引入了一项新功能： `nuget.exe restore`

这一新的 "还原" 命令可让你使用单个命令轻松还原解决方案的所有包，方法是接受解决方案文件或文件夹作为参数。 此外，当当前文件夹中只有一个解决方案时，该参数是隐含的。 这意味着，以下所有工作都包含单个解决方案文件 (MySolution) ：

1. nuget.exe restore MySolution
1. nuget.exe 还原。
1. nuget.exe 还原

Restore 命令将打开解决方案文件并查找解决方案中的所有项目。 然后，它将查找 `packages.config` 每个项目的文件，并还原找到的所有包。 它还将还原在文件中找到的解决方案级别包 `.nuget\packages.config` 。 有关新还原命令的详细信息，请参阅 [命令行参考](../reference/cli-reference/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的包还原工作流

我们对包还原进行了这些更改，因为它引入了一个新的工作流。 如果要从源代码管理中省略包，只需提交 `packages` 文件夹。 打开并生成解决方案的 Visual Studio 用户将看到包自动还原。 对于命令行生成，只需 `nuget.exe restore` 在调用之前调用 `msbuild` 。 不再需要记得在解决方案上使用 "启用 NuGet 包还原" 手势，而不再需要修改项目来更改生成。 这还为包含 MSBuild 导入的包带来了更好的体验，特别是通过 NuGet 的最新功能添加的导入，可自动导入 \build 文件夹中的 [属性/目标文件](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) 。

除了我们亲自完成的工作外，我们还与一些重要合作伙伴合作，将此新方法舍入。对于其中的任何一种情况，我们都没有具体的时间表，但每个合作伙伴都非常兴奋。

* Team Foundation Service-他们正在努力将对的调用集成到 `nuget.exe restore` 默认生成方案。
* Microsoft Azure 网站-他们正在努力，使你能够将项目推送到 Azure，并在 `nuget.exe restore` 构建你的网站之前调用它。
* TeamCity-他们正在为 TeamCity 3.x 更新 NuGet 安装程序插件
* AppHarbor-它们的作用是使你能够将存储库推送到 AppHarbor，并在 `nuget.exe restore` 构建解决方案之前调用它。

对于上述每个合作伙伴，他们将使用自己 nuget.exe 的副本，而无需在解决方案中携带 nuget.exe。

#### <a name="known-issues"></a>已知问题

在初始2.7 版本中，nuget.exe 还原有两个已知问题，但在9/6/2013 上已修复了该问题，并更新了 [NuGet 命令行包](http://www.nuget.org/packages/NuGet.CommandLine/)。  CodePlex 上的 [NuGet 2.7 下载页面](https://nuget.codeplex.com/releases/view/107605) 上也提供了此更新。  运行 `nuget.exe update -self` 将更新到最新版本。

固定的是：

1. [使用 SLN 文件时，新包还原不适用于 Mono](https://nuget.codeplex.com/workitem/3596)
1. [新包还原不适用于 Wix 项目](https://nuget.codeplex.com/workitem/3598)

新的包还原工作流也存在一个已知问题，即 [对于解决方案文件夹下的项目，自动包还原不起作用](https://nuget.codeplex.com/workitem/3625)。 此问题已在 NuGet 2.7.1 中修复。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>项目重定目标和升级生成错误/警告

在重定目标或升级项目后多次，你会发现某些 NuGet 包不能正常工作。 遗憾的是，没有任何迹象，就如何解决此情况没有任何帮助。 使用 NuGet 2.7，我们现在使用一些 Visual Studio 事件来识别你的项目重定向或升级的方式，这种方式会影响你安装的 NuGet 包。

如果检测到你的任何包受重定目标或升级的影响，我们将生成即时生成错误以通知你。 除了立即生成错误外，还 `requireReinstallation="true"` `packages.config` 会在文件中为受重定目标影响的所有包保留一个标志，并且 Visual Studio 中的每个后续生成将引发这些包的生成警告。

尽管 NuGet 不能执行自动操作来重新安装受影响的包，但我们希望这一指示和警告将引导你在需要重新安装包时了解相关信息。 我们还致力于在 [包重新安装指南文档](../consume-packages/reinstalling-and-updating-packages.md) 中，将这些错误消息定向到。

### <a name="nuget-configuration-defaults"></a>NuGet 配置默认值

许多公司都在内部使用 NuGet，但我们已在很大时间向开发人员提供了使用内部包源（而不是 nuget.org）的指导。NuGet 2.7 引入了 "配置默认值" 功能，该功能允许为以下项指定计算机范围的默认值：

1. 启用的包源
1. 已注册，但已禁用包源
1. 默认 nuget.exe 推送源

现在，其中的每个可在位于的文件中进行配置 `%ProgramData%\NuGet\NuGetDefaults.Config` 。 如果此配置文件指定了包源，则将不会自动注册默认的 nuget.org 包源，而是改为注册中的包源 `NuGetDefaults.Config` 。

尽管不需要使用此功能，但我们希望公司 `NuGetDefaults.Config` 使用组策略部署文件。

*请注意，此功能永远不会导致包源从开发人员的 NuGet 设置中删除。这意味着，如果开发人员已使用 NuGet，并因此注册了 nuget.org 包源，则不会在创建文件后将其删除 `NuGetDefaults.Config` 。*

有关此功能的详细信息，请参阅 [NuGet 配置默认值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) 。

### <a name="renaming-the-default-package-source"></a>重命名默认包源

NuGet 始终注册一个指向 nuget.org 的默认包源，名为 "NuGet 官方包源"。该名称是详细的，它也不指定实际指向的位置。 若要解决这两个问题，我们已将此包源重命名为 UI 中的 "nuget.org"。 包源的 URL 也已更改为包含 "www"。 前缀开头。 使用 NuGet 2.7 后，现有的 "NuGet 官方包源" 将自动更新为 "nuget.org" 作为其名称，将 " <https://www.nuget.org/api/v2/> " 作为其 URL。

### <a name="performance-improvements"></a>性能改进

我们在2.7 中进行了一些性能改进，从而降低了内存占用，减少了磁盘使用量，并加快了包安装。 我们还为基于 OData 的源进行了更智能化的查询，这将减少总体负载。

### <a name="new-extensibility-apis"></a>新的扩展性 Api

我们向扩展性服务添加了一些新的 Api，以弥补以前版本中缺少的功能的差距。

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

### <a name="development-only-dependencies"></a>Development-Only 依赖关系

此功能由 [Adam Ralph](https://twitter.com/adamralph) 提供，它允许包作者声明仅在开发时使用的依赖项，而无需包依赖项。 通过将 `developmentDependency="true"` 属性添加到中的包 `packages.config` ， `nuget.exe pack` 将不再包含该包作为依赖项。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>删除了对 Visual Studio 2010 Express for Windows Phone 的支持

2.7 中的新包还原模型是通过与主 NuGet VSPackage 不同的新 VSPackage 实现的。 由于技术问题，在 *Visual studio 2010 Express for Windows Phone* SKU 中，此新的 VSPackage 无法正常工作，因为我们与其他受支持的 Visual studio sku 共享相同的代码库。 因此，从 NuGet 2.7 开始，我们将从已发布的扩展中删除对 *Visual Studio 2010 Express for Windows Phone* 的支持。 支持 *Visual studio 2010 Express For Web* 仍包含在发布到 Visual Studio 扩展库的主扩展中。

由于我们不确定开发人员在该版本的 Visual Studio 中仍使用 NuGet 的多少开发人员，我们将专门为这些用户发布单独的 Visual Studio 扩展，并将其发布到 CodePlex (而不是) 的 Visual Studio 扩展库。 我们不打算继续维护该扩展，但如果这样会影响你，请在 CodePlex 上存档问题，告诉我们。

若要下载适用于 Visual Studio 2010 Express 的 NuGet 包管理器 (Windows Phone) ，请访问 [nuget 2.7 下载](https://nuget.codeplex.com/releases/view/107605) 页。

### <a name="bug-fixes"></a>Bug 修复

除了这些功能以外，此版本的 NuGet 还包括许多其他 bug 修复。 此版本中解决了97的总问题。 有关 NuGet 2.7 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
