---
title: NuGet 常见问题解答
description: 在命令行和 Visual Studio 中使用 NuGet 以及使用 NuGet 库的常见问题。
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: dbdd171321c2560adc06feccbd60fc4e84dcf0a3
ms.sourcegitcommit: a801052aa728a3a137225ca3ef3ff89f2d1c6b76
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403197"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="9e005-103">NuGet 常见问题</span><span class="sxs-lookup"><span data-stu-id="9e005-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="9e005-104">运行 NuGet 有哪些要求？</span><span class="sxs-lookup"><span data-stu-id="9e005-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="9e005-105">[安装指南](../install-nuget-client-tools.md)中提供了有关 UI 和命令行工具的所有信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="9e005-106">NuGet 是否支持 Mono？</span><span class="sxs-lookup"><span data-stu-id="9e005-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="9e005-107">命令行工具 `nuget.exe` 在 Mono 3.2+ 下生成和运行，并且可以在 Mono 中创建包。</span><span class="sxs-lookup"><span data-stu-id="9e005-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="9e005-108">尽管 `nuget.exe` 在 Windows 上可充分发挥功能，但用于 Linux 和 OS X 时则存在已知问题。请参阅 GitHub 上的 [Mono 问题](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。</span><span class="sxs-lookup"><span data-stu-id="9e005-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="9e005-109">[图形化客户端](https://github.com/mrward/monodevelop-nuget-addin)以 MonoDevelop 外接程序的形式提供。</span><span class="sxs-lookup"><span data-stu-id="9e005-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="9e005-110">如何确定包的内容及其是否适用于应用程序？</span><span class="sxs-lookup"><span data-stu-id="9e005-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="9e005-111">了解包的主要来源为 nuget.org（或其他私有源）上的包清单页。</span><span class="sxs-lookup"><span data-stu-id="9e005-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="9e005-112">nuget.org 上的每个包页面都包含包的说明、其版本历史记录和使用情况统计信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="9e005-113">包页面中的“信息”部分还包含项目网站的链接，此网站通常提供大量实例和其他文档，帮助你了解包的使用方法。</span><span class="sxs-lookup"><span data-stu-id="9e005-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="9e005-114">有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="9e005-115">Visual Studio 中的 NuGet</span><span class="sxs-lookup"><span data-stu-id="9e005-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="9e005-116">**NuGet 在不同 Visual Studio 产品中的受支持情况**</span><span class="sxs-lookup"><span data-stu-id="9e005-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="9e005-117">Windows 版 Visual Studio 支持[包管理器 UI](../tools/package-manager-ui.md) 和[包管理器控制台](../tools/package-manager-console.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="9e005-118">Visual Studio for Mac 具有内置 NuGet 功能，如[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)中所述。</span><span class="sxs-lookup"><span data-stu-id="9e005-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="9e005-119">Visual Studio Code（所有平台）与 NuGet 不存在任何直接集成。</span><span class="sxs-lookup"><span data-stu-id="9e005-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="9e005-120">请使用 [NuGet CLI](../tools/nuget-exe-cli-reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="9e005-121">Azure DevOps 提供[还原 NuGet 包的生成步骤](/vsts/build-release/tasks/package/nuget)。</span><span class="sxs-lookup"><span data-stu-id="9e005-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="9e005-122">还可以[在 Azure DevOps 上托管私有 NuGet 包源](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="9e005-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="9e005-123">**如何查看安装的 NuGet 工具的确切版本？**</span><span class="sxs-lookup"><span data-stu-id="9e005-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="9e005-124">在 Visual Studio 中，请使用“帮助”>“关于 Microsoft Visual Studio”命令，然后查看“NuGet 包管理器”旁显示的版本。</span><span class="sxs-lookup"><span data-stu-id="9e005-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="9e005-125">或者，启动“包管理器控制台”（“工具”>“NuGet 包管理器”>“包管理器控制台”），输入 `$host`，然后查看包括版本信息在内的 NuGet 的相关信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="9e005-126">NuGet 支持哪些编程语言？</span><span class="sxs-lookup"><span data-stu-id="9e005-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="9e005-127">NuGet 旨在将 .NET 库引入项目，通常适用于 .NET 语言。</span><span class="sxs-lookup"><span data-stu-id="9e005-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="9e005-128">由于 NuGet 还在某些项目类型中支持 MSBuild 和 Visual Studio 自动化，因此它也在不同程度上支持其他项目和语言。</span><span class="sxs-lookup"><span data-stu-id="9e005-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="9e005-129">最新版 NuGet 支持 C#、Visual Basic、F#、WiX 和 C++。</span><span class="sxs-lookup"><span data-stu-id="9e005-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="9e005-130">NuGet 支持哪些项目模板？</span><span class="sxs-lookup"><span data-stu-id="9e005-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="9e005-131">NuGet 对多种项目模板提供完整支持，如 Windows、Web、Cloud、SharePoint 和 Wix 等。</span><span class="sxs-lookup"><span data-stu-id="9e005-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="9e005-132">如何更新 Visual Studio 模板中的包？</span><span class="sxs-lookup"><span data-stu-id="9e005-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="9e005-133">在包管理器 UI，转到“更新”选项卡，选择“全部更新”；或者使用包管理控制台中的 [`Update-Package` 命令](../tools/ps-ref-update-package.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="9e005-134">若要更新模板本身，则需要手动更新模板存储库。</span><span class="sxs-lookup"><span data-stu-id="9e005-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="9e005-135">请参阅与该主题相关的 [Xavier Decoster 博客](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="9e005-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="9e005-136">请注意，此操作的风险由自己承担，因为如果所有依赖项的最新版本不相互兼容，手动更新可能会损坏该模板。</span><span class="sxs-lookup"><span data-stu-id="9e005-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="9e005-137">是否可以在 Visual Studio 之外使用 NuGet？</span><span class="sxs-lookup"><span data-stu-id="9e005-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="9e005-138">可以，NuGet 可直接在命令行中使用。</span><span class="sxs-lookup"><span data-stu-id="9e005-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="9e005-139">请参阅[安装指南](../install-nuget-client-tools.md)和 [CLI 参考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="9e005-140">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="9e005-140">NuGet command line</span></span>

<span data-ttu-id="9e005-141">如何获取最新版本的 NuGet 命令行工具？</span><span class="sxs-lookup"><span data-stu-id="9e005-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="9e005-142">请参阅[安装指南](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="9e005-143">**nuget.exe 的许可证是什么？**</span><span class="sxs-lookup"><span data-stu-id="9e005-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="9e005-144">可以根据 MIT 许可条款重新分发 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="9e005-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="9e005-145">你有责任更新和维护你选择重新分发的所有 nuget.exe 副本。</span><span class="sxs-lookup"><span data-stu-id="9e005-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="9e005-146">是否可以扩展 NuGet 命令行工具？</span><span class="sxs-lookup"><span data-stu-id="9e005-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="9e005-147">是的，可以向 `nuget.exe` 添加自定义命令，如 [Rob Reynold 博客](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="9e005-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="9e005-148">NuGet 包管理器控制台（Windows 版 Visual Studio）</span><span class="sxs-lookup"><span data-stu-id="9e005-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="9e005-149">如何在包管理器控制台中访问 DTE 对象？</span><span class="sxs-lookup"><span data-stu-id="9e005-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="9e005-150">Visual Studio 自动化对象模型中的顶层对象称为 DTE （开发工具环境）对象。</span><span class="sxs-lookup"><span data-stu-id="9e005-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="9e005-151">控制台通过名为 `$DTE` 的变量提供此对象。</span><span class="sxs-lookup"><span data-stu-id="9e005-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="9e005-152">有关详细信息，请参阅 Visual Studio 扩展性文档中的[自动化模型概述](/visualstudio/extensibility/internals/automation-model-overview)。</span><span class="sxs-lookup"><span data-stu-id="9e005-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="9e005-153">**尝试将 $DTE 变量强制转换为 DTE2 类型时出现错误：无法将“EnvDTE.DTEClass”类型的“EnvDTE.DTEClass”值转换为类型“EnvDTE80.DTE2”。** 为什么会这样？</span><span class="sxs-lookup"><span data-stu-id="9e005-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="9e005-154">这是 PowerShell 与 COM 对象交互的已知问题。</span><span class="sxs-lookup"><span data-stu-id="9e005-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="9e005-155">请尝试如下方法：</span><span class="sxs-lookup"><span data-stu-id="9e005-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="9e005-156">`Get-Interface` 是 NuGet PowerShell 主机添加的帮助程序函数。</span><span class="sxs-lookup"><span data-stu-id="9e005-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="9e005-157">创建和发布包</span><span class="sxs-lookup"><span data-stu-id="9e005-157">Creating and publishing packages</span></span>

<span data-ttu-id="9e005-158">如何在源中列出我的包？</span><span class="sxs-lookup"><span data-stu-id="9e005-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="9e005-159">请参阅[创建和发布包](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="9e005-160">我有面向不同版本的 .NET Framework 的多个版本的库。如何才能生成一个支持此方案的包？</span><span class="sxs-lookup"><span data-stu-id="9e005-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="9e005-161">请参阅[支持多个 .NET Framework 版本和配置文件](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="9e005-162">如何设置自己的存储库或源？</span><span class="sxs-lookup"><span data-stu-id="9e005-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="9e005-163">请参阅[托管包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9e005-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="9e005-164">如何将包批量上传到我的 NuGet 源？</span><span class="sxs-lookup"><span data-stu-id="9e005-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="9e005-165">请参阅[批量发布 NuGet 包](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。</span><span class="sxs-lookup"><span data-stu-id="9e005-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="9e005-166">使用包</span><span class="sxs-lookup"><span data-stu-id="9e005-166">Working with packages</span></span>

<span data-ttu-id="9e005-167">项目级包和解决方案级包之间有何差异？</span><span class="sxs-lookup"><span data-stu-id="9e005-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="9e005-168">解决方案级包 (NuGet 3.x+) 只需在解决方案上安装一次，随后即可用于该解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="9e005-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="9e005-169">项目级包需在使用它的每个项目中进行安装。</span><span class="sxs-lookup"><span data-stu-id="9e005-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="9e005-170">解决方案级包还可以安装可从包管理器控制台中调用的新命令。</span><span class="sxs-lookup"><span data-stu-id="9e005-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="9e005-171">是否可以在没有 Internet 连接时安装 NuGet 包？</span><span class="sxs-lookup"><span data-stu-id="9e005-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="9e005-172">可以，请参阅 Scott Hanselman 的博客文章 [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)（如何在 nuget.org 不可用（或用户在飞机上）时访问 NuGet）(hanselman.com)。</span><span class="sxs-lookup"><span data-stu-id="9e005-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="9e005-173">如何在默认包文件夹以外的其他位置安装包？</span><span class="sxs-lookup"><span data-stu-id="9e005-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="9e005-174">请使用 `nuget config -set repositoryPath=<path>` 设置 `Nuget.Config` 中的 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 设置。</span><span class="sxs-lookup"><span data-stu-id="9e005-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="9e005-175">如何避免将 NuGet 包文件夹中添加到源代码管理中？</span><span class="sxs-lookup"><span data-stu-id="9e005-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="9e005-176">请将 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="9e005-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="9e005-177">此密钥适用于解决方案级别，因此需要添加到 `$(Solutiondir)\.nuget\Nuget.Config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="9e005-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="9e005-178">从 Visual Studio 中启用包还原将自动创建此文件。</span><span class="sxs-lookup"><span data-stu-id="9e005-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="9e005-179">如何关闭包还原？</span><span class="sxs-lookup"><span data-stu-id="9e005-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="9e005-180">请参阅[启用和禁用包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="9e005-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="9e005-181">安装具有远程依赖项的本地包时，为何会出现“无法解析依赖项”错误？</span><span class="sxs-lookup"><span data-stu-id="9e005-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="9e005-182">将本地包安装到项目中时，需要选择“所有”源。</span><span class="sxs-lookup"><span data-stu-id="9e005-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="9e005-183">这样可以聚合所有源，而不只是一个源。</span><span class="sxs-lookup"><span data-stu-id="9e005-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="9e005-184">本地存储库用户通常不希望因为公司政策而意外安装远程包，因此才会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="9e005-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="9e005-185">如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 文件？</span><span class="sxs-lookup"><span data-stu-id="9e005-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="9e005-186">对于各个项目位于单独文件夹中的大多数项目，用户不必考虑此问题，因为 NuGet 会识别每个项目中的 `packages.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="9e005-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="9e005-187">如果使用 NuGet 3.3+ 并且同一文件夹中有多个项目，可将项目名称插入 `packages.config` 文件名（使用 `packages.{project-name}.config` 模式），然后 NuGet 将使用该文件。</span><span class="sxs-lookup"><span data-stu-id="9e005-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="9e005-188">使用 PackageReference 时不必考虑此问题，因为每个项目文件仅包含自己的依赖项列表。</span><span class="sxs-lookup"><span data-stu-id="9e005-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="9e005-189">存储库列表中未显示 nuget.org，应如何让其重新显示？</span><span class="sxs-lookup"><span data-stu-id="9e005-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="9e005-190">将 `https://api.nuget.org/v3/index.json` 添加到源列表；或</span><span class="sxs-lookup"><span data-stu-id="9e005-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="9e005-191">删除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 并指示 NuGet 重新创建它。</span><span class="sxs-lookup"><span data-stu-id="9e005-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="9e005-192">如果包未提供特定许可信息，有哪些默认许可条款？</span><span class="sxs-lookup"><span data-stu-id="9e005-192">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="9e005-193">每个包都需要受包中所含条款约束。</span><span class="sxs-lookup"><span data-stu-id="9e005-193">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="9e005-194">你应该在访问、下载或获取任何包前查看适用条款。</span><span class="sxs-lookup"><span data-stu-id="9e005-194">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="9e005-195">在 nuget.org 中，请使用包页面中的“许可信息”链接。</span><span class="sxs-lookup"><span data-stu-id="9e005-195">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="9e005-196">如果包未指定许可条款，请直接通过 nuget.org 包页面上的“联系所有者”链接与包所有者联系。</span><span class="sxs-lookup"><span data-stu-id="9e005-196">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="9e005-197">Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。</span><span class="sxs-lookup"><span data-stu-id="9e005-197">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="9e005-198">在 nuget.org 上管理包</span><span class="sxs-lookup"><span data-stu-id="9e005-198">Managing packages on nuget.org</span></span>

<span data-ttu-id="9e005-199">在上传包元数据后是否可以再对其进行编辑？</span><span class="sxs-lookup"><span data-stu-id="9e005-199">**Can I edit package metadata after it's been uploaded?**</span></span>

<span data-ttu-id="9e005-200">NuGet 建议对所有的包签名。</span><span class="sxs-lookup"><span data-stu-id="9e005-200">NuGet recommends all packages to be signed.</span></span> <span data-ttu-id="9e005-201">包签名的设计原则是已签名包的内容不得改变，nuspec 也包括在内。</span><span class="sxs-lookup"><span data-stu-id="9e005-201">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="9e005-202">编辑包元数据会使 nuspec 发生更改，导致现有签名无效。</span><span class="sxs-lookup"><span data-stu-id="9e005-202">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="9e005-203">我们建议在创建包后修改现有工作流，这样则无需编辑包元数据。</span><span class="sxs-lookup"><span data-stu-id="9e005-203">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="9e005-204">请注意，列出的包依赖项从包本身自动生成，并且无法进行编辑。</span><span class="sxs-lookup"><span data-stu-id="9e005-204">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="9e005-205">此外，要测试和验证包，同时不在公共库中提供此包，最好将包上传到[ int.nugettest.org](https://int.nugettest.org)。</span><span class="sxs-lookup"><span data-stu-id="9e005-205">In addition, uploading packages to [int.nugettest.org](https://int.nugettest.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="9e005-206">是否可以为以后发布的包预留名称？</span><span class="sxs-lookup"><span data-stu-id="9e005-206">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="9e005-207">可以。</span><span class="sxs-lookup"><span data-stu-id="9e005-207">Yes.</span></span> <span data-ttu-id="9e005-208">通过为帐户请求包 ID 前缀可以在 [nuget.org](https://www.nuget.org/) 中预留包 ID。</span><span class="sxs-lookup"><span data-stu-id="9e005-208">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="9e005-209">若要请求包 ID 前缀，请按照[文档](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-209">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="9e005-210">如何声明包的所有权？</span><span class="sxs-lookup"><span data-stu-id="9e005-210">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="9e005-211">请参阅[在 nuget.org 上管理包所有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="9e005-211">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="9e005-212">如何与违反我的软件许可的包所有者进行交涉？</span><span class="sxs-lookup"><span data-stu-id="9e005-212">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="9e005-213">我们鼓励 NuGet 社区合作解决包所有者和其他软件所有者之间可能出现的任何争议。</span><span class="sxs-lookup"><span data-stu-id="9e005-213">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="9e005-214">我们制定了周密的[争议解决流程](../policies/dispute-resolution.md)，要求 nuget.org 管理员调解之前应遵循此流程。</span><span class="sxs-lookup"><span data-stu-id="9e005-214">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="9e005-215">是否建议将测试包上传到 nuget.org？</span><span class="sxs-lookup"><span data-stu-id="9e005-215">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="9e005-216">对于测试目的，可以使用 [int.nugettest.org](https://int.nugettest.org)，或使用备用的公共 NuGet 服务器，如 [myget.org](https://myget.org) 或 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。</span><span class="sxs-lookup"><span data-stu-id="9e005-216">For test purposes, you can use [int.nugettest.org](https://int.nugettest.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="9e005-217">请注意，上传到 int.nugettest.org 的包可能不会保留。</span><span class="sxs-lookup"><span data-stu-id="9e005-217">Note that packages uploaded to int.nugettest.org may not be preserved.</span></span>

<span data-ttu-id="9e005-218">可上传到 nuget.org 的最大包大小是多少？</span><span class="sxs-lookup"><span data-stu-id="9e005-218">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="9e005-219">nuget.org 允许的最大包大小为 250 MB，但我们建议尽可能将包保持在 1 MB 以下，通过依赖项将包链接在一起。</span><span class="sxs-lookup"><span data-stu-id="9e005-219">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="9e005-220">依据经验，仅包含一个程序集的包可以避免冲突。</span><span class="sxs-lookup"><span data-stu-id="9e005-220">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="9e005-221">NuGet 使用 HTTP 下载包，因此较大包比较小包有更高的安装失败风险。</span><span class="sxs-lookup"><span data-stu-id="9e005-221">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="9e005-222">依赖项可以在多个包之间进行共享，这样可减小 NuGet 包使用者的总下载大小。</span><span class="sxs-lookup"><span data-stu-id="9e005-222">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="9e005-223">依赖项通常是静态的，永远不会更改。</span><span class="sxs-lookup"><span data-stu-id="9e005-223">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="9e005-224">修复代码中的 bug 时，可能无需更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="9e005-224">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="9e005-225">如果捆绑依赖项，最终将导致每一次都需要重新传输更大的包。</span><span class="sxs-lookup"><span data-stu-id="9e005-225">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="9e005-226">通过将 NuGet 包拆分成相关的依赖项，包使用者可以获得更细化的更新。</span><span class="sxs-lookup"><span data-stu-id="9e005-226">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="9e005-227">nuget.org 不可访问</span><span class="sxs-lookup"><span data-stu-id="9e005-227">nuget.org not accessible</span></span>

<span data-ttu-id="9e005-228">为何无法从 nuget.org 下载包或向其中上传包？</span><span class="sxs-lookup"><span data-stu-id="9e005-228">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="9e005-229">首先，请确保使用的是最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="9e005-229">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="9e005-230">如果该版本仍然失败，请[联系支持人员](https://www.nuget.org/policies/Contact)，并提供其他连接故障排除信息，包括：</span><span class="sxs-lookup"><span data-stu-id="9e005-230">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="9e005-231">使用的 NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="9e005-231">The version of NuGet you're using</span></span>
- <span data-ttu-id="9e005-232">使用的包源</span><span class="sxs-lookup"><span data-stu-id="9e005-232">The package sources you're using</span></span>
- <span data-ttu-id="9e005-233">详细还原日志</span><span class="sxs-lookup"><span data-stu-id="9e005-233">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="9e005-234">MTR 或 Fiddler 跟踪（见下文）</span><span class="sxs-lookup"><span data-stu-id="9e005-234">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="9e005-235">所在地理区域</span><span class="sxs-lookup"><span data-stu-id="9e005-235">Your geographical area</span></span>
- <span data-ttu-id="9e005-236">计算机是否设置了代理或防火墙？</span><span class="sxs-lookup"><span data-stu-id="9e005-236">Whether your machine is behind a proxy or firewall?</span></span>
- <span data-ttu-id="9e005-237">计算机是否位于云提供商的数据中心（Azure、AWS 等）？</span><span class="sxs-lookup"><span data-stu-id="9e005-237">Is your machine located on a cloud providers' data center (Azure, AWS etc)?</span></span> <span data-ttu-id="9e005-238">如果是，请提供此提供商名称和区域。</span><span class="sxs-lookup"><span data-stu-id="9e005-238">If yes, please provide the name of the provider and the region.</span></span>

<span data-ttu-id="9e005-239">捕获 MTR：</span><span class="sxs-lookup"><span data-stu-id="9e005-239">*To capture MTR:*</span></span>

- <span data-ttu-id="9e005-240">从 [http://winmtr.net/download/](http://winmtr.net/) 下载 WinMTR</span><span class="sxs-lookup"><span data-stu-id="9e005-240">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="9e005-241">输入 `api.nuget.org` 作为主机名，然后单击“启动”。</span><span class="sxs-lookup"><span data-stu-id="9e005-241">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="9e005-242">等待，直到“已发送”列 >= 100。</span><span class="sxs-lookup"><span data-stu-id="9e005-242">Wait until the **Sent** column is >= 100.</span></span>

    ![捕获 MTR](media/mtr.png)

- <span data-ttu-id="9e005-244">将文本复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="9e005-244">Copy text to clipboard.</span></span>

<span data-ttu-id="9e005-245">捕获 Fiddler：</span><span class="sxs-lookup"><span data-stu-id="9e005-245">*To capture Fiddler:*</span></span>

- <span data-ttu-id="9e005-246">安装最新版本的 [Fiddler](http://www.telerik.com/download/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="9e005-246">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="9e005-247">启动 Fiddler，使用“文件”>“捕获流量”菜单禁用捕获流量。</span><span class="sxs-lookup"><span data-stu-id="9e005-247">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="9e005-248">删除所有会话（选中列表中的所有项，按 Delete 键）。</span><span class="sxs-lookup"><span data-stu-id="9e005-248">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="9e005-249">配置 Fiddler 以捕获 HTTPS 流量，具体操作方式为：打开“工具”>“Fiddler 选项...”菜单，勾选“HTTPS”选项卡中的“解密 HTTPS 流量”。</span><span class="sxs-lookup"><span data-stu-id="9e005-249">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="9e005-250">关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9e005-250">Close Visual Studio.</span></span>
- <span data-ttu-id="9e005-251">启用“文件”>“捕获流量”菜单。</span><span class="sxs-lookup"><span data-stu-id="9e005-251">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="9e005-252">启动 Visual Studio 或 nuget.exe.exe，执行当前未运行的操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-252">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="9e005-253">Fiddler 中应显示出这些操作所产生的流量。</span><span class="sxs-lookup"><span data-stu-id="9e005-253">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="9e005-254">操作运行结束后，使用“文件”>“保存”>“所有会话”来存储捕获的会话。</span><span class="sxs-lookup"><span data-stu-id="9e005-254">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="9e005-255">注意：若要通过 Fiddler 路由 NuGet，可能需要将 `HTTP_PROXY` 环境变量设置为 `http://127.0.0.1:8888`。</span><span class="sxs-lookup"><span data-stu-id="9e005-255">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="9e005-256">如果该操作失败，请尝试[该 StackOverflow 文章中提到的方法](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。</span><span class="sxs-lookup"><span data-stu-id="9e005-256">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="9e005-257">有哪些适用于 nuget.org 的 API 终结点？</span><span class="sxs-lookup"><span data-stu-id="9e005-257">**What are the API endpoints for nuget.org?**</span></span>

- <span data-ttu-id="9e005-258">V3：`https://api.nuget.org/v3/index.json`</span><span class="sxs-lookup"><span data-stu-id="9e005-258">V3: `https://api.nuget.org/v3/index.json`</span></span>
- <span data-ttu-id="9e005-259">V2：`https://www.nuget.org/api/v2/`（请注意，V2 API 已弃用且不适用于 NuGet 4+。）</span><span class="sxs-lookup"><span data-stu-id="9e005-259">V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>

## <a name="nugetorg-account-management"></a><span data-ttu-id="9e005-260">nuget.org 帐户管理</span><span class="sxs-lookup"><span data-stu-id="9e005-260">nuget.org account management</span></span>

### <a name="how-to-create-a-new-nugetorg-account"></a><span data-ttu-id="9e005-261">如何新建 nuget.org 帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-261">How to create a new nuget.org account?</span></span>

<span data-ttu-id="9e005-262">要创建 nuget.org 帐户，需要具备 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-262">To create a nuget.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="9e005-263">如果没有帐户，请[创建](https://signup.live.com)帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-263">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="9e005-264">如果拥有 MSA 或 AAD 帐户，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-264">Follow the following steps if you have a MSA or AAD account.</span></span>
1. <span data-ttu-id="9e005-265">转到 [nuget.org 登录页](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="9e005-265">Go to the [nuget.org login page](https://www.nuget.org/users/account/LogOn).</span></span>
1. <span data-ttu-id="9e005-266">单击“Microsoft 登录”按钮。</span><span class="sxs-lookup"><span data-stu-id="9e005-266">Click on **Sign in with Microsoft** button.</span></span>
1. <span data-ttu-id="9e005-267">输入 MSA/AAD 帐户详细信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-267">Enter your MSA/AAD account details.</span></span>
1. <span data-ttu-id="9e005-268">请接受要授予 NuGet.org 应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="9e005-268">Please accept the permissions to be given to the *NuGet.org* application.</span></span>
1. <span data-ttu-id="9e005-269">此时系统将重定向至 nuget.org 并要求注册用户名。</span><span class="sxs-lookup"><span data-stu-id="9e005-269">You will be redirected to nuget.org, and asked to register a username.</span></span>
1. <span data-ttu-id="9e005-270">在输入框中指定用户名。</span><span class="sxs-lookup"><span data-stu-id="9e005-270">Specify the username in the input box.</span></span> <span data-ttu-id="9e005-271">请注意，用户名需区分大小写，并且以后无法更改/重命名。</span><span class="sxs-lookup"><span data-stu-id="9e005-271">Please note that the username **is** case sensitive and cannot be changed/renamed later.</span></span>
1. <span data-ttu-id="9e005-272">单击“注册”按钮。</span><span class="sxs-lookup"><span data-stu-id="9e005-272">Click on **Register** button.</span></span>

<span data-ttu-id="9e005-273">现在 nuget.org 帐户已成功创建。</span><span class="sxs-lookup"><span data-stu-id="9e005-273">You now have a nuget.org account.</span></span> <span data-ttu-id="9e005-274">可以在[帐户设置](https://www.nuget.org/account)页面执行帐户管理。</span><span class="sxs-lookup"><span data-stu-id="9e005-274">You can perfrom account management on the [account settings](https://www.nuget.org/account) page.</span></span>

### <a name="how-to-recover-nugetorg-password-login"></a><span data-ttu-id="9e005-275">如何恢复 nuget.org 密码登录？</span><span class="sxs-lookup"><span data-stu-id="9e005-275">How to recover nuget.org password login?</span></span>

<span data-ttu-id="9e005-276">请注意，[nuget.org 密码登录已经停止使用](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html)，当前登录 nuget.org 的唯一方式是使用 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-276">Please note that the [nuget.org Password login has been discontinued](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) and the only way to log in to nuget.org is with a personal Microsoft account (MSA) or Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="9e005-277">但是，在无法访问关联的 MSA/AAD 帐户的情形下，可能需要通过密码登录恢复 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-277">However, in case you are unable to access your associated MSA/AAD accounts you might need to use password login for recovering your nuget.org account.</span></span> <span data-ttu-id="9e005-278">这种情况下，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-278">In this situation follow the steps below.</span></span>
- <span data-ttu-id="9e005-279">**要求：** 需要有权访问与要恢复密码的帐户相关联的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="9e005-279">**Requirement:** You will need to have access to the email that is associated with the account for which you need to recover the password.</span></span>
- <span data-ttu-id="9e005-280">转到[“忘记密码”页面](https://www.nuget.org/account/ForgotPassword)</span><span class="sxs-lookup"><span data-stu-id="9e005-280">Go to the [Forgot password page](https://www.nuget.org/account/ForgotPassword)</span></span>
- <span data-ttu-id="9e005-281">输入与要恢复的 nuget.org 帐户相关联的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="9e005-281">Enter the **email** address that is associated with the nuget.org account you wish to recover.</span></span>
- <span data-ttu-id="9e005-282">单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="9e005-282">Click the **Send** button.</span></span>
- <span data-ttu-id="9e005-283">指定的电子邮件地址帐户会收到一封电子邮件，其中包含密码重置链接。</span><span class="sxs-lookup"><span data-stu-id="9e005-283">You will get an email to the specified email address account with a link to reset your password.</span></span> <span data-ttu-id="9e005-284">单击此链接并设置新密码。</span><span class="sxs-lookup"><span data-stu-id="9e005-284">Click on this link and set the new password.</span></span> <span data-ttu-id="9e005-285">如果未找到该邮件，请查看“垃圾邮件”文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e005-285">If you can't find the mail check your "junk" folder.</span></span>
- <span data-ttu-id="9e005-286">完成后，现在可以使用用户名/密码登录 NuGet。</span><span class="sxs-lookup"><span data-stu-id="9e005-286">Once done, you can now login with username/password on NuGet.</span></span>
- <span data-ttu-id="9e005-287">要通过用户名/密码登录，请使用 [nuget.org 帐户登录页面](https://www.nuget.org/users/account/LogOn)上的“使用 Nuget.org 帐户登录”链接。</span><span class="sxs-lookup"><span data-stu-id="9e005-287">To login with username/password, use the **Sign in using Nuget.org account** link on the  [nuget.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a><span data-ttu-id="9e005-288">哪个 Microsoft 帐户已链接到 nuget.org 帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-288">Which Microsoft account is linked to my nuget.org account?</span></span>

<span data-ttu-id="9e005-289">如果忘记了与 nuget.org 帐户关联的 Microsoft 帐户，请按照以下步骤获取帮助。</span><span class="sxs-lookup"><span data-stu-id="9e005-289">If you have forgotten which Microsoft account is associated with your nuget.org account, please follow the steps below to get assistance.</span></span>
1. <span data-ttu-id="9e005-290">转到 [nuget.org 登录页面](https://www.nuget.org/users/account/LogOn)，并单击“需要登录协助?”链接。</span><span class="sxs-lookup"><span data-stu-id="9e005-290">Go to [nuget.org login page](https://www.nuget.org/users/account/LogOn) and click on **Need assistance signing in?** link.</span></span>
1. <span data-ttu-id="9e005-291">此操作会弹出一个帮助对话框。</span><span class="sxs-lookup"><span data-stu-id="9e005-291">This will show you the pop-up dialog box for assistance.</span></span> <span data-ttu-id="9e005-292">按照该对话框中的步骤，找出与 nuget.org 帐户的关联的 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-292">Follow the steps in this dialog box to understand the associated Microsoft account(s) for your nuget.org account.</span></span>

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a><span data-ttu-id="9e005-293">如何更改用于登录 nuget.org 的 Microsoft 帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-293">How to change the Microsoft account I use for nuget.org login?</span></span>
<span data-ttu-id="9e005-294">要更改登录 nuget.org 所用的 Microsoft 帐户，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-294">If you wish to change the Microsoft account for nuget.org user, follow the steps below.</span></span> <span data-ttu-id="9e005-295">假设电子邮件为 `account1@outlook.com` 的 Microsoft 帐户已关联到用户名为 `MyNuGetAccount` 的 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-295">Lets say your Microsoft account with email `account1@outlook.com` is associated with your nuget.org account with username `MyNuGetAccount`.</span></span> <span data-ttu-id="9e005-296">现在需要将登录帐户更改为电子邮件为 `account2@outlook.com` 的另一 Microsoft 帐户</span><span class="sxs-lookup"><span data-stu-id="9e005-296">You wish to change the login to another Microsoft account with email `account2@outlook.com`</span></span>
1. <span data-ttu-id="9e005-297">转到[登录页面](https://www.nuget.org/users/account/LogOn)，单击“Microsoft 登录”，然后使用当前关联的 Microsoft 帐户（即 `account1@outlook.com`）登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-297">Please sign in using **currently associated Microsoft account** i.e. `account1@outlook.com` on the [login page](https://www.nuget.org/users/account/LogOn) after clicking **Sign in with Microsoft**.</span></span>
1. <span data-ttu-id="9e005-298">登录后，请转到[帐户设置](https://www.nuget.org/account)页面。</span><span class="sxs-lookup"><span data-stu-id="9e005-298">Once logged in, go to your [account settings](https://www.nuget.org/account) page.</span></span>
1. <span data-ttu-id="9e005-299">展开“登录帐户”部分。</span><span class="sxs-lookup"><span data-stu-id="9e005-299">Expand the section for **Login Account**.</span></span> <span data-ttu-id="9e005-300">单击“更改帐户”按钮。</span><span class="sxs-lookup"><span data-stu-id="9e005-300">Click on the **Change Account** button.</span></span>
1. <span data-ttu-id="9e005-301">系统会重定向至 Microsoft 登录页面。</span><span class="sxs-lookup"><span data-stu-id="9e005-301">You will now be redirected to the microsoft login page.</span></span> <span data-ttu-id="9e005-302">请使用要更改为关联帐户的帐户登录，即 `account2@outlook.com`。**注意**：登录过程中，可能需要单击“注销并使用另一个帐户登录”，才能使用其他 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-302">Please sign in with the account that you wish to change the association to i.e. `account2@outlook.com`. **Note**: you might need to click on **Sign out and sign in with different account** during the sign in flow to be able to login with a different Microsoft account.</span></span>
1. <span data-ttu-id="9e005-303">如果看到如下类似错误，请查看 [Microsoft 帐户已链接到另一个 nuget.org 帐户](#microsoft-account-is-linked-with-another-nugetorg-account)，了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-303">If you see an error like below, see [Microsoft account is linked with another nuget.org account](#microsoft-account-is-linked-with-another-nugetorg-account) for more details.</span></span>
    ><span data-ttu-id="9e005-304">_无法将此 Microsoft 帐户更新为“account2 <account2@outlook.com>”。原因可能是该帐户已链接到另一个 NuGet 帐户。有关详细信息，请联系支持人员。_</span><span class="sxs-lookup"><span data-stu-id="9e005-304">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information._</span></span>

1. <span data-ttu-id="9e005-305">使用第二个帐户成功登录后，系统会重定向到 nuget.org 帐户设置页面，现在应能看到新的 Microsoft 帐户关联作为登录帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-305">Once you have successfully signed in with your second account, you will be redirected back to your nuget.org account settings page and you should now see the new Microsoft account associated as the login account.</span></span> <span data-ttu-id="9e005-306">之后登录 nuget.org 时应使用此帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-306">Going forward you should use this account when signing into nuget.org.</span></span>

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a><span data-ttu-id="9e005-307">Microsoft 帐户已链接到另一个 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-307">Microsoft account is linked with another nuget.org account.</span></span>

<span data-ttu-id="9e005-308">尝试更改 Microsoft 登录时可能出现如下错误：</span><span class="sxs-lookup"><span data-stu-id="9e005-308">If you tried changing your Microsoft login and saw the error below:</span></span>
> <span data-ttu-id="9e005-309">_无法将此 Microsoft 帐户更新为“account2 <account2@outlook.com>”。原因可能是该帐户已链接到另一个 NuGet 帐户。有关详细信息，请联系支持人员。_</span><span class="sxs-lookup"><span data-stu-id="9e005-309">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information._</span></span>

<span data-ttu-id="9e005-310">假设对于用户名为 `MyNuGetAccount1` 的 nuget.org 用户，要将其 Microsoft 帐户登录从 `account1@outlook.com` 更改为电子邮件为 `account2@outlook.com` 的另一 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-310">Lets say you were trying to change Microsoft account login from `account1@outlook.com` for nuget.org user with username `MyNuGetAccount1` to another Microsoft account with email `account2@outlook.com`.</span></span> <span data-ttu-id="9e005-311">更改过程中出现上述错误。</span><span class="sxs-lookup"><span data-stu-id="9e005-311">And you see the error above.</span></span>

<span data-ttu-id="9e005-312">**上述错误表示什么意思？**</span><span class="sxs-lookup"><span data-stu-id="9e005-312">**What does the error above mean?**</span></span>

<span data-ttu-id="9e005-313">该错误表示要更改到的 Microsoft 帐户已有一个与之关联的 nuget.org 帐户，即上例中电子邮件为 `<account2@outlook.com>` 的 Microsoft 帐户与另一个 nuget.org 帐户（例如，用户名为 `MyNuGetAccount2`）相关联。</span><span class="sxs-lookup"><span data-stu-id="9e005-313">It means that there is another nuget.org account which is associated with the Microsoft account that you are trying to change it to i.e. in above example the Microsoft account with email `<account2@outlook.com>` is associated with another nuget.org account with, say, username `MyNuGetAccount2`.</span></span>

<span data-ttu-id="9e005-314">无法将关联登录更改为已连接到另一个 nuget.org 帐户的 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-314">You cannot change the associated login with a Microsoft account that is linked to a different nuget.org account.</span></span>

<span data-ttu-id="9e005-315">**如果忘记了另一个 nuget.org 帐户，如何才能将其找出？**</span><span class="sxs-lookup"><span data-stu-id="9e005-315">**I forgot I had another nuget.org account, how do I find out which nuget.org account it is?**</span></span>

<span data-ttu-id="9e005-316">在[登录页面](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "login page")上使用第二个 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-316">Login with the second Microsoft account on the [login page](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "login page").</span></span> <span data-ttu-id="9e005-317">这会登录到当前与第二个 Microsoft 帐户相关联的 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-317">This will log you into the nuget.org account that is currently associated with the second Microsoft account.</span></span> <span data-ttu-id="9e005-318">然后可以通过此帐户查看已上传的包和进行帐户管理。</span><span class="sxs-lookup"><span data-stu-id="9e005-318">You can then view the uploaded packages and perform account management on this account.</span></span>

<span data-ttu-id="9e005-319">**我不太关注第二个 nuget.org 帐户，我希望将第二个 Microsoft 帐户更改为第一个 nuget.org 帐户的登录名。我该怎么办？**</span><span class="sxs-lookup"><span data-stu-id="9e005-319">**I do not care about this second nuget.org account, I want to change my login for first nuget.org account with the second Microsoft account. What do I do?**</span></span>

<span data-ttu-id="9e005-320">如果不关注第二个 nuget.org 帐户，并仍希望重新使用已关联的 Microsoft 帐户（电子邮件为 `account2@outlook.com`），</span><span class="sxs-lookup"><span data-stu-id="9e005-320">If you wish to not care about the second nuget.org account and still want to re-use the associated Microsoft account with email `account2@outlook.com`.</span></span> 

<span data-ttu-id="9e005-321">可以通过删除该 nuget.org 帐户，解除其与此 Microsoft 帐户之间的关联。</span><span class="sxs-lookup"><span data-stu-id="9e005-321">You can release the association between the Microsoft account and nuget.org account by deleting the nuget.org account.</span></span>
1. <span data-ttu-id="9e005-322">对于第二个 nuget.org 帐户 `MyNuGetAccount2`，请执行[删除用户](#how-to-delete-my-nugetorg-account)的步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-322">Follow the steps to [delete user](#how-to-delete-my-nugetorg-account) for the second nuget.org account `MyNuGetAccount2`.</span></span> 
1. <span data-ttu-id="9e005-323">删除此帐户后，可以重试[更改 Microsoft 帐户登录](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)的步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-323">Once this account is deleted, you can retry the steps to [change Microsoft account login](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).</span></span>

<span data-ttu-id="9e005-324">**等一下，我也关注第二个帐户。我不想失去此帐户，但同时也想更改第一个帐户的关联帐户。**</span><span class="sxs-lookup"><span data-stu-id="9e005-324">**Wait, I care about this second account too. I do not want to lose this account but change my associated account logins for first account.**</span></span>

<span data-ttu-id="9e005-325">为此，需要创建/使用第三个 Microsoft 帐户，假设该帐户的电子邮件为 `account3@outlook.com`。</span><span class="sxs-lookup"><span data-stu-id="9e005-325">You will need to create/use a third Microsoft account, say, with email `account3@outlook.com`.</span></span> 
1. <span data-ttu-id="9e005-326">首先应使用第二个 Microsoft 帐户 `account2@outlook.com` 登录 nuget.org。按照以上步骤更改关联登录并将第三个 Microsoft 帐户与此 nuget.org 帐户关联。</span><span class="sxs-lookup"><span data-stu-id="9e005-326">First you should login with your second Microsoft account, `account2@outlook.com` on nuget.org. Follow the steps above to change associated logins and associate the third Microsoft account with this nuget.org account.</span></span>
1. <span data-ttu-id="9e005-327">完成后，电子邮件为 `account2@outlook.com` 的第二个 Microsoft 帐户即可关联到第一个 nuget.org 帐户 (`MyNuGetAccount1`)。</span><span class="sxs-lookup"><span data-stu-id="9e005-327">Once done, your second Microsoft account with email `account2@outlook.com` is free to be associated to your first nuget.org account, `MyNuGetAccount1`.</span></span> <span data-ttu-id="9e005-328">按照上述相同步骤将 Microsoft 帐户更改为第二个 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-328">Follow the same steps above to change microsoft logins to the second Microsoft account.</span></span>

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a><span data-ttu-id="9e005-329">使用 Microsoft 帐户登录时显示电子邮件已链接到另一个 Microsoft 帐户</span><span class="sxs-lookup"><span data-stu-id="9e005-329">Signing in with Microsoft account shows me my email is linked to another Microsoft account</span></span>
<span data-ttu-id="9e005-330">尝试使用 Microsoft 帐户（例如，电子邮件为 `account1@outlook.com` 的帐户）登录时，可能出现如下错误：</span><span class="sxs-lookup"><span data-stu-id="9e005-330">If you tried to sign in with your Microsoft account, say, with email `account1@outlook.com` and you see an error like below:</span></span>
> <span data-ttu-id="9e005-331">电子邮件为 "account1@outlook.com" 的帐户已链接到另一个 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-331">_The account with email 'account1@outlook.com' is linked with another microsoft account._</span></span>
>
> <span data-ttu-id="9e005-332">在帐户设置中可以更新已链接的 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-332">_If you would like to update the linked Microsoft account you can do so from the account settings page._</span></span>

<span data-ttu-id="9e005-333">**上述错误表示什么意思？**</span><span class="sxs-lookup"><span data-stu-id="9e005-333">**What does the error above mean?**</span></span>

<span data-ttu-id="9e005-334">在 nuget.org 上创建帐户后，该帐户具有一个关联的通信电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="9e005-334">When an account is created on nuget.org, there is a communication email address associated with that account.</span></span> <span data-ttu-id="9e005-335">此地址通常与所关联 Microsoft 帐户的电子邮件地址相同。</span><span class="sxs-lookup"><span data-stu-id="9e005-335">This is usually same as the email address that is used for associated Microsoft account.</span></span> <span data-ttu-id="9e005-336">但是，可以选择指定不同的电子邮件地址进行通信。</span><span class="sxs-lookup"><span data-stu-id="9e005-336">However, you could choose to specify a different email address for communication.</span></span> <span data-ttu-id="9e005-337">因此，从技术上讲，可以将另一个 Microsoft 帐户（例如电子邮件为 `account2@outlook.com` 的帐户）链接到通信电子邮件地址为 `account1@outlook.com` 的 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-337">So, technically, you could have a different Microsoft account, say with `account2@outlook.com` that is linked to nuget.org account with communication email address as `account1@outlook.com`.</span></span>

<span data-ttu-id="9e005-338">所以，上述错误表示已存在一个通信电子邮件地址为 `account1@outlook.com` 的 nuget.org 帐户，但该帐户已关联到电子邮件不是 `account1@outlook.com` 的另一个 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-338">So the error above means that there already exists nuget.org account with communication email address `account1@outlook.com` but is associated with another Microsoft account with email **that is not** `account1@outlook.com`.</span></span>

<span data-ttu-id="9e005-339">**如何查找哪个 Microsoft 帐户已链接到此 nuget.org 帐户？**</span><span class="sxs-lookup"><span data-stu-id="9e005-339">**How do I find which Microsoft account is linked to this nuget.org account?**</span></span>

<span data-ttu-id="9e005-340">应该按照[登录协助](#which-microsoft-account-is-linked-to-my-nugetorg-account)流程找出哪个 Microsoft 帐户已链接到电子邮件地址为 `account1@outlook.com` 的 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-340">You should use the [sign in assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) flow to figure out which Microsoft account is linked to the nuget.org account with the email address `account1@outlook.com`.</span></span>

<span data-ttu-id="9e005-341">**我想要使用我的 Microsoft 帐户替换已关联的 Microsoft 帐户**</span><span class="sxs-lookup"><span data-stu-id="9e005-341">**I want to override that account with my Microsoft account**</span></span>

<span data-ttu-id="9e005-342">按照[无法使用 Microsoft 登录，如何恢复 nuget.org 帐户](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)部分中的步骤将 Microsoft 帐户与现有 nuget.org 帐户相关联。</span><span class="sxs-lookup"><span data-stu-id="9e005-342">Follow the steps in [Unable to use microsoft login, how do I recover my nuget.org account](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) section to associate your Microsoft account with the existing nuget.org account.</span></span>

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a><span data-ttu-id="9e005-343">无法使用 Microsoft 登录，如何恢复 nuget.org 帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-343">Unable to use microsoft login, how do I recover my nuget.org account?</span></span>

<span data-ttu-id="9e005-344">如果尝试使用[登录协助](#which-microsoft-account-is-linked-to-my-nugetorg-account)但无权访问与 nuget.org 帐户关联的 Microsoft 帐户，请按照以下步骤将新的 Microsoft 帐户关联到此 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-344">If you tried using the [sign in assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) and you do not have access to the Microsoft account that is associated with your nuget.org account, please follow the steps below to link a new Microsoft account to your nuget.org account.</span></span>
1. <span data-ttu-id="9e005-345">**要求**：有权访问某 Microsoft 帐户（此帐户并未关联到任何现有 nuget.org 帐户）。</span><span class="sxs-lookup"><span data-stu-id="9e005-345">**Requirement**: You will need an access to a Microsoft account(which is not associated with any existing nuget.org accounts).</span></span> <span data-ttu-id="9e005-346">如果没有帐户，请[创建](https://signup.live.com)帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-346">If you do not have one, you can [create](https://signup.live.com) one.</span></span>
2. <span data-ttu-id="9e005-347">按照[密码登录恢复步骤](#how-to-recover-nugetorg-password-login)操作。如已具有密码登录，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-347">Follow the [steps to recover your password login](#how-to-recover-nugetorg-password-login), if you have the password login skip this step.</span></span>
3. <span data-ttu-id="9e005-348">通过用户名/密码登录方法[登录 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。</span><span class="sxs-lookup"><span data-stu-id="9e005-348">[Login to nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) using the username/password login.</span></span>
4. <span data-ttu-id="9e005-349">登录后会弹出如下所示的对话框。</span><span class="sxs-lookup"><span data-stu-id="9e005-349">Once logged in, you will see the popup dialog show up like below.</span></span> <span data-ttu-id="9e005-350">这是密码终止对话框。</span><span class="sxs-lookup"><span data-stu-id="9e005-350">This is the password discontinuation dialog box.</span></span>
5. <span data-ttu-id="9e005-351">**注意**：请忽略有关使用指定 Microsoft 帐户登录的说明。</span><span class="sxs-lookup"><span data-stu-id="9e005-351">**NOTE**: Please ignore the instruction to login with the specified Microsoft account.</span></span> <span data-ttu-id="9e005-352">现在可将 nuget.org 帐户链接到任何其他 Microsoft 登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-352">You can now link your nuget.org account to any other Microsoft login.</span></span>
6. <span data-ttu-id="9e005-353">单击“Microsoft 登录”按钮，然后按步骤 1 所述，使用具有访问权限的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-353">Click on the button **Sign in with Microsoft** and login with the Microsoft account that you have an access to, as mentioned in step 1.</span></span>
7. <span data-ttu-id="9e005-354">帐户现将链接到此新的 Microsoft 帐户，今后该帐户可用于登录 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="9e005-354">Your account will now be linked to the new Microsoft account, which you can use to log into nuget.org going forward.</span></span>

    ![MSA 链接对话框](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a><span data-ttu-id="9e005-356">如何将我的 nuget.org 帐户转换为组织帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-356">How to transform my nuget.org account to an organization?</span></span>

<span data-ttu-id="9e005-357">如要将帐户转换为组织帐户，且此帐户已与 Microsoft 帐户登录关联，请按照 [nuget org 上的组织](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org)文档中的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-357">If you want to transform your account to an organization, and this account is already associated with a Microsoft account login, please follow the steps given in the documentation for [organizations on nuget org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).</span></span>

<span data-ttu-id="9e005-358">但是，如果 nuget.org 帐户未关联/链接到 Microsoft 帐户，可按照如下步骤将此帐户转换为组织帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-358">If however, your nuget.org account is not associated/linked with a Microsoft account, you can follow the steps below to transform this account to an organization.</span></span>
1. <span data-ttu-id="9e005-359">**要求**：首选需要在 nuget.org 上创建一个用作组织帐户管理员的个人帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-359">**Requirement**: You need to have an individual account first created on nuget.org to be used as an admin on the org account.</span></span> <span data-ttu-id="9e005-360">如果没有此帐户，请[新建一个 nuget.org 帐户](#how-to-create-a-nugetorg-account)</span><span class="sxs-lookup"><span data-stu-id="9e005-360">If you do not have one, please [create a new nuget.org account](#how-to-create-a-nugetorg-account)</span></span>
2. <span data-ttu-id="9e005-361">如果 nuget.org 帐户尚无密码登录，请按照[密码登录恢复步骤](#how-to-recover-nugetorg-password-login)进行操作。如有，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="9e005-361">Follow the [steps to recover your password login](#how-to-recover-nugetorg-password-login) for your nuget.org account if you do not have password login for it, if you do, skip this step.</span></span>
3. <span data-ttu-id="9e005-362">通过用户名/密码登录方法[登录 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。</span><span class="sxs-lookup"><span data-stu-id="9e005-362">[Login to nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) using the username/password login.</span></span>
4. <span data-ttu-id="9e005-363">登录后会弹出如下所示的对话框。</span><span class="sxs-lookup"><span data-stu-id="9e005-363">Once logged in, you will see the popup dialog show up like below.</span></span> <span data-ttu-id="9e005-364">这是密码终止对话框。</span><span class="sxs-lookup"><span data-stu-id="9e005-364">This is the password discontinuation dialog box.</span></span> 
    > [!Important]
    > <span data-ttu-id="9e005-365">请忽略此对话框，切勿单击“Microsoft 登录”按钮。</span><span class="sxs-lookup"><span data-stu-id="9e005-365">Ignore this dialog box, **do not** click on the **Sign in with microsoft** button.</span></span>

5. <span data-ttu-id="9e005-366">转到 [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)。</span><span class="sxs-lookup"><span data-stu-id="9e005-366">Go to [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform).</span></span> <span data-ttu-id="9e005-367">这会将此 nuget.org 帐户转换为组织帐户，且无需链接到 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-367">This will allow you to convert the nuget.org account to an org without linking to a Microsoft account.</span></span>
6. <span data-ttu-id="9e005-368">为 nuget.org 个人帐户/步骤 1 中创建的帐户指定管理员用户名。</span><span class="sxs-lookup"><span data-stu-id="9e005-368">Specify the admin username for your personal nuget.org account/the account you created in Step 1.</span></span>
7. <span data-ttu-id="9e005-369">按照说明将此帐户转换为组织帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-369">Follow the instructions to complete transformation of this account to an organization.</span></span>

    ![MSA 链接对话框](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a><span data-ttu-id="9e005-371">出现有关具有非托管组合的 AAD 帐户的 nuget.org 登录问题？</span><span class="sxs-lookup"><span data-stu-id="9e005-371">nuget.org login issues for AAD accounts with unmanaged tenant?</span></span>

<span data-ttu-id="9e005-372">使用电子邮件帐户域 (@yourdomain.com) 登录过程中如果出现类似如下的错误，请参阅以下步骤恢复 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-372">If you see an error like below during your login flow with your email account domain(@yourdomain.com), see the steps below to recover your nuget.org account.</span></span>

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

<span data-ttu-id="9e005-373">**登录过程中出现的“非托管”状态是什么？为什么会出现这种情况？**</span><span class="sxs-lookup"><span data-stu-id="9e005-373">**What is this unmanaged state thing during login? And why is this happening now?**</span></span> 

<span data-ttu-id="9e005-374">你的帐户似乎在之前注册为 Microsoft 个人帐户，且其使用正常，但现在此帐户似乎已在 Azure Active Directory（用于对 Microsoft 帐户执行身份验证的标识符）中注册为“非托管”租户。</span><span class="sxs-lookup"><span data-stu-id="9e005-374">Your account seems to be previously registered as a personal Microsoft account and it worked fine, however, now it seems like your account has been registered as an "Unmanaged" tenant in the Azure Active Directory (the identity service which we use to authenticate Microsoft accounts).</span></span> 

<span data-ttu-id="9e005-375">出现此情况的原因可能是你或你所在组织的其他人员（电子邮件为 @yourdomain.com）注册了某个 AAD 集成服务，或者进行了 [Azure Active Directory 自助注册](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)，这会对所使用的 Microsoft 帐户域（对你而言为 @yourdomain.com）创建一个“非托管”租户。</span><span class="sxs-lookup"><span data-stu-id="9e005-375">This could have happened if you or someone from your organization(with @yourdomain.com email address) registered with one of the AAD integrated services or did a [self-service signup for Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), which creates such an "Unmanaged" tenant for the used Microsoft account domain(@yourdomain.com in your case).</span></span> 

<span data-ttu-id="9e005-376">**怎样才可以恢复帐户？**</span><span class="sxs-lookup"><span data-stu-id="9e005-376">**What can I do to recover my account?**</span></span>

<span data-ttu-id="9e005-377">当前，我们 (nuget.org) 无法使用 Azure Active Directory 中含有此类“非托管”租户帐户对帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9e005-377">At this moment there is not a way for us (nuget.org) to authenticate accounts with such "Unmanaged" tenant accounts in Azure Active directory.</span></span> <span data-ttu-id="9e005-378">我们正在寻找一种更佳的方式来对此类帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9e005-378">We are looking in to a better way to authenticate such accounts.</span></span>

<span data-ttu-id="9e005-379">如果要使用 Microsoft 帐户 (@yourdomain.com) 登录 nuget.org，你（或你所在公司的管理员）需要通过执行 DNS 验证声明 AAD 所有者，以对电子邮件地址为“@yourdomain.com”的用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9e005-379">If you want to login to nuget.org with your Microsoft account(@yourdomain.com), you(or an administrator at your company) will need to claim the ownership of the AAD by doing a DNS validation to authenticate users with email address "@yourdomain.com".</span></span> <span data-ttu-id="9e005-380">请按照 Azure Active directory 文档[域管理员接管](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)中的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-380">Please follow the steps for [domains admin takeover](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) documented by the Azure Active directory.</span></span> <span data-ttu-id="9e005-381">完成后，应能开始正常登录。</span><span class="sxs-lookup"><span data-stu-id="9e005-381">Once this is done, your normal login should start working.</span></span>

<span data-ttu-id="9e005-382">**我不想使用这种方法，还有什么其他方法可以恢复帐户？**</span><span class="sxs-lookup"><span data-stu-id="9e005-382">**I don’t want to do all that, what is the other way to recover my account?**</span></span>

<span data-ttu-id="9e005-383">可以[创建](https://www.microsoft.com/en-us/account)一个新的 Microsoft 帐户（其电子邮件未与 @yourdomain.com 关联）。</span><span class="sxs-lookup"><span data-stu-id="9e005-383">You can [create](https://www.microsoft.com/en-us/account) a new Microsoft account (with an email **not** associated with @yourdomain.com).</span></span> <span data-ttu-id="9e005-384">请按照[恢复 nuget.org 帐户](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)部分所述的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-384">Follow steps given in [recover your nuget.org account](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) section.</span></span>

### <a name="how-do-i-change-my-nugetorg-account-username"></a><span data-ttu-id="9e005-385">如何更改 nuget.org 帐户用户名？</span><span class="sxs-lookup"><span data-stu-id="9e005-385">How do I change my nuget.org account username?</span></span>

<span data-ttu-id="9e005-386">无法更改。</span><span class="sxs-lookup"><span data-stu-id="9e005-386">You cannot.</span></span> <span data-ttu-id="9e005-387">根据策略，截至目前我们不允许更改用户名。</span><span class="sxs-lookup"><span data-stu-id="9e005-387">As a matter of policy we do not allow the change of usernames as of yet.</span></span> <span data-ttu-id="9e005-388">更改用户名的唯一方式是创建采用所需用户名的新帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-388">The only way to change your username is to create a new account with the desired username.</span></span> <span data-ttu-id="9e005-389">创建新帐户之前，我们建议删除现有帐户，否则便可能无法重复使用已注册的 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-389">We recommend you delete your existing account before you create a new one, otherwise you will not be able to reuse your registered Microsoft account.</span></span>
> [!Important]
> <span data-ttu-id="9e005-390">删除用户仍会保留 `username`。</span><span class="sxs-lookup"><span data-stu-id="9e005-390">Deleting the user will still **reserve** the `username`.</span></span> <span data-ttu-id="9e005-391">你将无法重复使用相同的用户名，即使更改大小写也不例外。</span><span class="sxs-lookup"><span data-stu-id="9e005-391">You will not be able to reuse the same username again and **this includes the change of casings**.</span></span> <span data-ttu-id="9e005-392">例如，创建用户名为 `mycoolname` 的用户然后删除此用户后，要将此用户名改为 `MyCoolName`（大小写更改）是不可实现的。</span><span class="sxs-lookup"><span data-stu-id="9e005-392">As an example if you created a user with username `mycoolname` and you want to change this to `MyCoolName`(casing changes), it will not be possible after deleting the user.</span></span>

<span data-ttu-id="9e005-393">按照删除 [nuget.org 帐户](#how-to-delete-my-nugetorg-account)部分中所述的步骤使用正确用户名[注册新用户](#how-to-create-a-new-nugetorg-account)。</span><span class="sxs-lookup"><span data-stu-id="9e005-393">Follow the steps given in [delete your nuget.org account](#how-to-delete-my-nugetorg-account) section and to [register a new account](#how-to-create-a-new-nugetorg-account) with correct username.</span></span>

### <a name="how-to-delete-my-nugetorg-account"></a><span data-ttu-id="9e005-394">如何删除 nuget.org 帐户？</span><span class="sxs-lookup"><span data-stu-id="9e005-394">How to delete my nuget.org account?</span></span>

<span data-ttu-id="9e005-395">请注意，要删除帐户，我们建议将你作为其唯一所有者的包的所有权进行转让。</span><span class="sxs-lookup"><span data-stu-id="9e005-395">To delete your account, please note that we recommend that you transfer the ownership of any packages where you are the sole owner.</span></span> <span data-ttu-id="9e005-396">要了解如何执行此操作，请阅读有关[管理包所有者](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)的更多信息。</span><span class="sxs-lookup"><span data-stu-id="9e005-396">You can read more about [managing package owners](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) on how to do it.</span></span> <span data-ttu-id="9e005-397">这有助于我们加速处理请求。</span><span class="sxs-lookup"><span data-stu-id="9e005-397">This will also help us expedite your request.</span></span>

> [!Important]
> <span data-ttu-id="9e005-398">删除用户会导致以下结果：</span><span class="sxs-lookup"><span data-stu-id="9e005-398">Deleting the user will result in following:</span></span>
>  1. <span data-ttu-id="9e005-399">撤销关联的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="9e005-399">Revoke associated API key(s).</span></span> 
>  2. <span data-ttu-id="9e005-400">删除作为任何子包所有者的帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-400">Remove the account as an owner for any child packages.</span></span>
>  3. <span data-ttu-id="9e005-401">将所有之前存在的 ID 前缀预留与此帐户取消关联。</span><span class="sxs-lookup"><span data-stu-id="9e005-401">Dissociate all previously existent ID prefix reservations with this account.</span></span>
>  4. <span data-ttu-id="9e005-402">删除作为任何组织成员的帐户。</span><span class="sxs-lookup"><span data-stu-id="9e005-402">Remove the account as a member of any organizations.</span></span>
>  5. <span data-ttu-id="9e005-403">用户名会保留，未经我们允许，任何人不能再次使用该用户名。</span><span class="sxs-lookup"><span data-stu-id="9e005-403">Your username will be reserved and no one will be able to re-use it again without our permissions.</span></span>

<span data-ttu-id="9e005-404">请按照以下步骤继续进行帐户删除。</span><span class="sxs-lookup"><span data-stu-id="9e005-404">Follow the following steps to proceed with account deletion.</span></span>
1. <span data-ttu-id="9e005-405">使用要删除的帐户[登录 nuget.org](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="9e005-405">[Login to nuget.org](https://www.nuget.org/users/account/LogOn) with the account you wish to delete.</span></span>
2. <span data-ttu-id="9e005-406">单击此 URL：[https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)，然后按照步骤提交帐户删除请求。</span><span class="sxs-lookup"><span data-stu-id="9e005-406">Click on this url: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) and follow the steps to submit the request for deleting the account.</span></span>

<span data-ttu-id="9e005-407">我们的客户支持人员将处理请求并执行帐户删除操作。</span><span class="sxs-lookup"><span data-stu-id="9e005-407">Our customer support will process this request and perform the account deletion.</span></span>