---
title: NuGet 常见问题解答
description: 在命令行和 Visual Studio 中使用 NuGet 的常见问题和解答。
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 27a925c8748cb2085e8c9fe71ef23281cf9fd553
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860539"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="c845a-103">NuGet 常见问题</span><span class="sxs-lookup"><span data-stu-id="c845a-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="c845a-104">运行 NuGet 有哪些要求？ </span><span class="sxs-lookup"><span data-stu-id="c845a-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="c845a-105">[安装指南](../install-nuget-client-tools.md)中提供了有关 UI 和命令行工具的所有信息。</span><span class="sxs-lookup"><span data-stu-id="c845a-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="c845a-106">NuGet 是否支持 Mono？ </span><span class="sxs-lookup"><span data-stu-id="c845a-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="c845a-107">命令行工具 `nuget.exe` 在 Mono 3.2+ 下生成和运行，并且可以在 Mono 中创建包。</span><span class="sxs-lookup"><span data-stu-id="c845a-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="c845a-108">尽管 `nuget.exe` 在 Windows 上可充分发挥功能，但用于 Linux 和 OS X 时则存在已知问题。请参阅 GitHub 上的 [Mono 问题](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。</span><span class="sxs-lookup"><span data-stu-id="c845a-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="c845a-109">[图形化客户端](https://github.com/mrward/monodevelop-nuget-addin)以 MonoDevelop 外接程序的形式提供。</span><span class="sxs-lookup"><span data-stu-id="c845a-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="c845a-110">如何确定包的内容及其是否适用于应用程序？ </span><span class="sxs-lookup"><span data-stu-id="c845a-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="c845a-111">了解包的主要来源为 nuget.org（或其他私有源）上的包清单页。</span><span class="sxs-lookup"><span data-stu-id="c845a-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="c845a-112">nuget.org 上的每个包页面都包含包的说明、其版本历史记录和使用情况统计信息。</span><span class="sxs-lookup"><span data-stu-id="c845a-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="c845a-113">包页面中的“信息”部分还包含项目网站的链接，此网站通常提供大量实例和其他文档，帮助你了解包的使用方法  。</span><span class="sxs-lookup"><span data-stu-id="c845a-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="c845a-114">有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="c845a-115">Visual Studio 中的 NuGet</span><span class="sxs-lookup"><span data-stu-id="c845a-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="c845a-116">**NuGet 在不同 Visual Studio 产品中的受支持情况**</span><span class="sxs-lookup"><span data-stu-id="c845a-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="c845a-117">Windows 版 Visual Studio 支持[包管理器 UI](../consume-packages/install-use-packages-visual-studio.md) 和[包管理器控制台](../consume-packages/install-use-packages-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="c845a-118">Visual Studio for Mac 具有内置 NuGet 功能，如[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)中所述。</span><span class="sxs-lookup"><span data-stu-id="c845a-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="c845a-119">Visual Studio Code（所有平台）与 NuGet 不存在任何直接集成。</span><span class="sxs-lookup"><span data-stu-id="c845a-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="c845a-120">请使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 或 [dotnet CLI](../reference/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="c845a-121">Azure DevOps 提供[还原 NuGet 包的生成步骤](/vsts/build-release/tasks/package/nuget)。</span><span class="sxs-lookup"><span data-stu-id="c845a-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="c845a-122">还可以[在 Azure DevOps 上托管私有 NuGet 包源](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="c845a-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="c845a-123">**如何查看安装的 NuGet 工具的确切版本？**</span><span class="sxs-lookup"><span data-stu-id="c845a-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="c845a-124">在 Visual Studio 中，请使用“帮助”>“关于 Microsoft Visual Studio”命令，然后查看“NuGet 包管理器”旁显示的版本   。</span><span class="sxs-lookup"><span data-stu-id="c845a-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="c845a-125">或者，启动“包管理器控制台”（“工具”>“NuGet 包管理器”>“包管理器控制台”），输入 `$host`，然后查看包括版本信息在内的 NuGet 的相关信息  。</span><span class="sxs-lookup"><span data-stu-id="c845a-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="c845a-126">NuGet 支持哪些编程语言？ </span><span class="sxs-lookup"><span data-stu-id="c845a-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="c845a-127">NuGet 旨在将 .NET 库引入项目，通常适用于 .NET 语言。</span><span class="sxs-lookup"><span data-stu-id="c845a-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="c845a-128">由于 NuGet 还在某些项目类型中支持 MSBuild 和 Visual Studio 自动化，因此它也在不同程度上支持其他项目和语言。</span><span class="sxs-lookup"><span data-stu-id="c845a-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="c845a-129">最新版 NuGet 支持 C#、Visual Basic、F#、WiX 和 C++。</span><span class="sxs-lookup"><span data-stu-id="c845a-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="c845a-130">NuGet 支持哪些项目模板？ </span><span class="sxs-lookup"><span data-stu-id="c845a-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="c845a-131">NuGet 对多种项目模板提供完整支持，如 Windows、Web、Cloud、SharePoint 和 Wix 等。</span><span class="sxs-lookup"><span data-stu-id="c845a-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="c845a-132">如何更新 Visual Studio 模板中的包？ </span><span class="sxs-lookup"><span data-stu-id="c845a-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="c845a-133">在包管理器 UI，转到“更新”选项卡，选择“全部更新”；或者使用包管理控制台中的 [`Update-Package` 命令](../reference/ps-reference/ps-ref-update-package.md)   。</span><span class="sxs-lookup"><span data-stu-id="c845a-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="c845a-134">若要更新模板本身，则需要手动更新模板存储库。</span><span class="sxs-lookup"><span data-stu-id="c845a-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="c845a-135">请参阅与该主题相关的 [Xavier Decoster 博客](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="c845a-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="c845a-136">请注意，此操作的风险由自己承担，因为如果所有依赖项的最新版本不相互兼容，手动更新可能会损坏该模板。</span><span class="sxs-lookup"><span data-stu-id="c845a-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="c845a-137">是否可以在 Visual Studio 之外使用 NuGet？ </span><span class="sxs-lookup"><span data-stu-id="c845a-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="c845a-138">可以，NuGet 可直接在命令行中使用。</span><span class="sxs-lookup"><span data-stu-id="c845a-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="c845a-139">请参阅[安装指南](../install-nuget-client-tools.md)和 [CLI 参考](../reference/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="c845a-140">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="c845a-140">NuGet command line</span></span>

<span data-ttu-id="c845a-141">如何获取最新版本的 NuGet 命令行工具？ </span><span class="sxs-lookup"><span data-stu-id="c845a-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="c845a-142">请参阅[安装指南](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="c845a-143">**nuget.exe 的许可证是什么？**</span><span class="sxs-lookup"><span data-stu-id="c845a-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="c845a-144">可以根据 MIT 许可条款重新分发 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="c845a-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="c845a-145">你有责任更新和维护你选择重新分发的所有 nuget.exe 副本。</span><span class="sxs-lookup"><span data-stu-id="c845a-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="c845a-146">是否可以扩展 NuGet 命令行工具？ </span><span class="sxs-lookup"><span data-stu-id="c845a-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="c845a-147">是的，可以向 `nuget.exe` 添加自定义命令，如 [Rob Reynold 博客](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="c845a-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="c845a-148">NuGet 包管理器控制台（Windows 版 Visual Studio）</span><span class="sxs-lookup"><span data-stu-id="c845a-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="c845a-149">如何在包管理器控制台中访问 DTE 对象？ </span><span class="sxs-lookup"><span data-stu-id="c845a-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="c845a-150">Visual Studio 自动化对象模型中的顶层对象称为 DTE （开发工具环境）对象。</span><span class="sxs-lookup"><span data-stu-id="c845a-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="c845a-151">控制台通过名为 `$DTE` 的变量提供此对象。</span><span class="sxs-lookup"><span data-stu-id="c845a-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="c845a-152">有关详细信息，请参阅 Visual Studio 扩展性文档中的[自动化模型概述](/visualstudio/extensibility/internals/automation-model-overview)。</span><span class="sxs-lookup"><span data-stu-id="c845a-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="c845a-153">**尝试将 $DTE 变量强制转换为 DTE2 类型时出现错误：无法将“EnvDTE.DTEClass”类型的“EnvDTE.DTEClass”值转换为类型“EnvDTE80.DTE2”。** 为什么会这样？</span><span class="sxs-lookup"><span data-stu-id="c845a-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="c845a-154">这是 PowerShell 与 COM 对象交互的已知问题。</span><span class="sxs-lookup"><span data-stu-id="c845a-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="c845a-155">请尝试如下方法：</span><span class="sxs-lookup"><span data-stu-id="c845a-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="c845a-156">`Get-Interface` 是 NuGet PowerShell 主机添加的帮助程序函数。</span><span class="sxs-lookup"><span data-stu-id="c845a-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="c845a-157">创建和发布包</span><span class="sxs-lookup"><span data-stu-id="c845a-157">Creating and publishing packages</span></span>

<span data-ttu-id="c845a-158">如何在源中列出我的包？ </span><span class="sxs-lookup"><span data-stu-id="c845a-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="c845a-159">请参阅[创建和发布包](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="c845a-160">我有面向不同版本的 .NET Framework 的多个版本的库。  如何才能生成一个支持此方案的包？</span><span class="sxs-lookup"><span data-stu-id="c845a-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="c845a-161">请参阅[支持多个 .NET Framework 版本和配置文件](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="c845a-162">如何设置自己的存储库或源？ </span><span class="sxs-lookup"><span data-stu-id="c845a-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="c845a-163">请参阅[托管包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c845a-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="c845a-164">如何将包批量上传到我的 NuGet 源？ </span><span class="sxs-lookup"><span data-stu-id="c845a-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="c845a-165">请参阅[批量发布 NuGet 包](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。</span><span class="sxs-lookup"><span data-stu-id="c845a-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="c845a-166">使用包</span><span class="sxs-lookup"><span data-stu-id="c845a-166">Working with packages</span></span>

<span data-ttu-id="c845a-167">项目级包和解决方案级包之间有何差异？ </span><span class="sxs-lookup"><span data-stu-id="c845a-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="c845a-168">解决方案级包 (NuGet 3.x+) 只需在解决方案上安装一次，随后即可用于该解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="c845a-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="c845a-169">项目级包需在使用它的每个项目中进行安装。</span><span class="sxs-lookup"><span data-stu-id="c845a-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="c845a-170">解决方案级包还可以安装可从包管理器控制台中调用的新命令。</span><span class="sxs-lookup"><span data-stu-id="c845a-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="c845a-171">是否可以在没有 Internet 连接时安装 NuGet 包？ </span><span class="sxs-lookup"><span data-stu-id="c845a-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="c845a-172">可以，请参阅 Scott Hanselman 的博客文章 [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)（如何在 nuget.org 不可用（或用户在飞机上）时访问 NuGet）(hanselman.com)。</span><span class="sxs-lookup"><span data-stu-id="c845a-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="c845a-173">如何在默认包文件夹以外的其他位置安装包？ </span><span class="sxs-lookup"><span data-stu-id="c845a-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="c845a-174">请使用 `nuget config -set repositoryPath=<path>` 设置 `Nuget.Config` 中的 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 设置。</span><span class="sxs-lookup"><span data-stu-id="c845a-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="c845a-175">如何避免将 NuGet 包文件夹中添加到源代码管理中？ </span><span class="sxs-lookup"><span data-stu-id="c845a-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="c845a-176">请将 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="c845a-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="c845a-177">此密钥适用于解决方案级别，因此需要添加到 `$(Solutiondir)\.nuget\Nuget.Config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="c845a-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="c845a-178">从 Visual Studio 中启用包还原将自动创建此文件。</span><span class="sxs-lookup"><span data-stu-id="c845a-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="c845a-179">如何关闭包还原？ </span><span class="sxs-lookup"><span data-stu-id="c845a-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="c845a-180">请参阅[启用和禁用包还原](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="c845a-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="c845a-181">安装具有远程依赖项的本地包时，为何会出现“无法解析依赖项”错误？ </span><span class="sxs-lookup"><span data-stu-id="c845a-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="c845a-182">将本地包安装到项目中时，需要选择“所有”源  。</span><span class="sxs-lookup"><span data-stu-id="c845a-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="c845a-183">这样可以聚合所有源，而不只是一个源。</span><span class="sxs-lookup"><span data-stu-id="c845a-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="c845a-184">本地存储库用户通常不希望因为公司政策而意外安装远程包，因此才会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="c845a-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="c845a-185">如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 文件？ </span><span class="sxs-lookup"><span data-stu-id="c845a-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="c845a-186">对于各个项目位于单独文件夹中的大多数项目，用户不必考虑此问题，因为 NuGet 会识别每个项目中的 `packages.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="c845a-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="c845a-187">如果使用 NuGet 3.3+ 并且同一文件夹中有多个项目，可将项目名称插入 `packages.config` 文件名（使用 `packages.{project-name}.config` 模式），然后 NuGet 将使用该文件。</span><span class="sxs-lookup"><span data-stu-id="c845a-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="c845a-188">使用 PackageReference 时不必考虑此问题，因为每个项目文件仅包含自己的依赖项列表。</span><span class="sxs-lookup"><span data-stu-id="c845a-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="c845a-189">存储库列表中未显示 nuget.org，应如何让其重新显示？ </span><span class="sxs-lookup"><span data-stu-id="c845a-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="c845a-190">将 `https://api.nuget.org/v3/index.json` 添加到源列表；或</span><span class="sxs-lookup"><span data-stu-id="c845a-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="c845a-191">删除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 并指示 NuGet 重新创建它。</span><span class="sxs-lookup"><span data-stu-id="c845a-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
