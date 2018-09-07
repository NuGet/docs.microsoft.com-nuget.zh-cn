---
title: NuGet 常见问题解答
description: 在命令行和 Visual Studio 中使用 NuGet 以及使用 NuGet 库的常见问题。
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 8c63abc9971623e0732ae8d973fafcd04c5d9f48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548799"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="23d5f-103">NuGet 常见问题</span><span class="sxs-lookup"><span data-stu-id="23d5f-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="23d5f-104">运行 NuGet 有哪些要求？</span><span class="sxs-lookup"><span data-stu-id="23d5f-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="23d5f-105">[安装指南](../install-nuget-client-tools.md)中提供了有关 UI 和命令行工具的所有信息。</span><span class="sxs-lookup"><span data-stu-id="23d5f-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="23d5f-106">NuGet 是否支持 Mono？</span><span class="sxs-lookup"><span data-stu-id="23d5f-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="23d5f-107">命令行工具 `nuget.exe` 在 Mono 3.2+ 下生成和运行，并且可以在 Mono 中创建包。</span><span class="sxs-lookup"><span data-stu-id="23d5f-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="23d5f-108">尽管 `nuget.exe` 在 Windows 上可充分发挥功能，但用于 Linux 和 OS X 时则存在已知问题。请参阅 GitHub 上的 [Mono 问题](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="23d5f-109">[图形化客户端](https://github.com/mrward/monodevelop-nuget-addin)以 MonoDevelop 外接程序的形式提供。</span><span class="sxs-lookup"><span data-stu-id="23d5f-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="23d5f-110">如何确定包的内容及其是否适用于应用程序？</span><span class="sxs-lookup"><span data-stu-id="23d5f-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="23d5f-111">了解包的主要来源为 nuget.org（或其他私有源）上的包清单页。</span><span class="sxs-lookup"><span data-stu-id="23d5f-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="23d5f-112">nuget.org 上的每个包页面都包含包的说明、其版本历史记录和使用情况统计信息。</span><span class="sxs-lookup"><span data-stu-id="23d5f-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="23d5f-113">包页面中的“信息”部分还包含项目网站的链接，此网站通常提供大量实例和其他文档，帮助你了解包的使用方法。</span><span class="sxs-lookup"><span data-stu-id="23d5f-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="23d5f-114">有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="23d5f-115">Visual Studio 中的 NuGet</span><span class="sxs-lookup"><span data-stu-id="23d5f-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="23d5f-116">**NuGet 在不同 Visual Studio 产品中的受支持情况**</span><span class="sxs-lookup"><span data-stu-id="23d5f-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="23d5f-117">Windows 版 Visual Studio 支持[包管理器 UI](../tools/package-manager-ui.md) 和[包管理器控制台](../tools/package-manager-console.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="23d5f-118">Visual Studio for Mac 具有内置 NuGet 功能，如[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)中所述。</span><span class="sxs-lookup"><span data-stu-id="23d5f-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="23d5f-119">Visual Studio Code（所有平台）与 NuGet 不存在任何直接集成。</span><span class="sxs-lookup"><span data-stu-id="23d5f-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="23d5f-120">请使用 [NuGet CLI](../tools/nuget-exe-cli-reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="23d5f-121">Visual Studio Team Services 提供[还原 NuGet 包的生成步骤](/vsts/build-release/tasks/package/nuget)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-121">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="23d5f-122">还可以[在 Team Services 上托管私有 NuGet 包源](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-122">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="23d5f-123">**如何查看安装的 NuGet 工具的确切版本？**</span><span class="sxs-lookup"><span data-stu-id="23d5f-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="23d5f-124">在 Visual Studio 中，请使用“帮助”>“关于 Microsoft Visual Studio”命令，然后查看“NuGet 包管理器”旁显示的版本。</span><span class="sxs-lookup"><span data-stu-id="23d5f-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="23d5f-125">或者，启动“包管理器控制台”（“工具”>“NuGet 包管理器”>“包管理器控制台”），输入 `$host`，然后查看包括版本信息在内的 NuGet 的相关信息。</span><span class="sxs-lookup"><span data-stu-id="23d5f-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="23d5f-126">NuGet 支持哪些编程语言？</span><span class="sxs-lookup"><span data-stu-id="23d5f-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="23d5f-127">NuGet 旨在将 .NET 库引入项目，通常适用于 .NET 语言。</span><span class="sxs-lookup"><span data-stu-id="23d5f-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="23d5f-128">由于 NuGet 还在某些项目类型中支持 MSBuild 和 Visual Studio 自动化，因此它也在不同程度上支持其他项目和语言。</span><span class="sxs-lookup"><span data-stu-id="23d5f-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="23d5f-129">最新版 NuGet 支持 C#、Visual Basic、F#、WiX 和 C++。</span><span class="sxs-lookup"><span data-stu-id="23d5f-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="23d5f-130">NuGet 支持哪些项目模板？</span><span class="sxs-lookup"><span data-stu-id="23d5f-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="23d5f-131">NuGet 对多种项目模板提供完整支持，如 Windows、Web、Cloud、SharePoint 和 Wix 等。</span><span class="sxs-lookup"><span data-stu-id="23d5f-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="23d5f-132">如何更新 Visual Studio 模板中的包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="23d5f-133">在包管理器 UI，转到“更新”选项卡，选择“全部更新”；或者使用包管理控制台中的 [`Update-Package` 命令](../tools/ps-ref-update-package.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="23d5f-134">若要更新模板本身，则需要手动更新模板存储库。</span><span class="sxs-lookup"><span data-stu-id="23d5f-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="23d5f-135">请参阅与该主题相关的 [Xavier Decoster 博客](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="23d5f-136">请注意，此操作的风险由自己承担，因为如果所有依赖项的最新版本不相互兼容，手动更新可能会损坏该模板。</span><span class="sxs-lookup"><span data-stu-id="23d5f-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="23d5f-137">是否可以在 Visual Studio 之外使用 NuGet？</span><span class="sxs-lookup"><span data-stu-id="23d5f-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="23d5f-138">可以，NuGet 可直接在命令行中使用。</span><span class="sxs-lookup"><span data-stu-id="23d5f-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="23d5f-139">请参阅[安装指南](../install-nuget-client-tools.md)和 [CLI 参考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="23d5f-140">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="23d5f-140">NuGet command line</span></span>

<span data-ttu-id="23d5f-141">如何获取最新版本的 NuGet 命令行工具？</span><span class="sxs-lookup"><span data-stu-id="23d5f-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="23d5f-142">请参阅[安装指南](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="23d5f-143">**nuget.exe 的许可证是什么？**</span><span class="sxs-lookup"><span data-stu-id="23d5f-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="23d5f-144">可以根据 MIT 许可条款重新分发 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="23d5f-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="23d5f-145">你有责任更新和维护你选择重新分发的所有 nuget.exe 副本。</span><span class="sxs-lookup"><span data-stu-id="23d5f-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="23d5f-146">是否可以扩展 NuGet 命令行工具？</span><span class="sxs-lookup"><span data-stu-id="23d5f-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="23d5f-147">是的，可以向 `nuget.exe` 添加自定义命令，如 [Rob Reynold 博客](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="23d5f-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="23d5f-148">NuGet 包管理器控制台（Windows 版 Visual Studio）</span><span class="sxs-lookup"><span data-stu-id="23d5f-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="23d5f-149">如何在包管理器控制台中访问 DTE 对象？</span><span class="sxs-lookup"><span data-stu-id="23d5f-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="23d5f-150">Visual Studio 自动化对象模型中的顶层对象称为 DTE （开发工具环境）对象。</span><span class="sxs-lookup"><span data-stu-id="23d5f-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="23d5f-151">控制台通过名为 `$DTE` 的变量提供此对象。</span><span class="sxs-lookup"><span data-stu-id="23d5f-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="23d5f-152">有关详细信息，请参阅 Visual Studio 扩展性文档中的[自动化模型概述](/visualstudio/extensibility/internals/automation-model-overview)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="23d5f-153">我尝试将 $DTE 变量强制转换为类型 DTE2，但出现错误：无法将类型“EnvDTE.DTEClass”的“EnvDTE.DTEClass”值转换为类型“EnvDTE80.DTE2”。为什么会这样？</span><span class="sxs-lookup"><span data-stu-id="23d5f-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="23d5f-154">这是 PowerShell 与 COM 对象交互的已知问题。</span><span class="sxs-lookup"><span data-stu-id="23d5f-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="23d5f-155">请尝试如下方法：</span><span class="sxs-lookup"><span data-stu-id="23d5f-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="23d5f-156">`Get-Interface` 是 NuGet PowerShell 主机添加的帮助程序函数。</span><span class="sxs-lookup"><span data-stu-id="23d5f-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="23d5f-157">创建和发布包</span><span class="sxs-lookup"><span data-stu-id="23d5f-157">Creating and publishing packages</span></span>

<span data-ttu-id="23d5f-158">如何在源中列出我的包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="23d5f-159">请参阅[创建和发布包](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="23d5f-160">我有面向不同版本的 .NET Framework 的多个版本的库。如何才能生成一个支持此方案的包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="23d5f-161">请参阅[支持多个 .NET Framework 版本和配置文件](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="23d5f-162">如何设置自己的存储库或源？</span><span class="sxs-lookup"><span data-stu-id="23d5f-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="23d5f-163">请参阅[托管包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="23d5f-164">如何将包批量上传到我的 NuGet 源？</span><span class="sxs-lookup"><span data-stu-id="23d5f-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="23d5f-165">请参阅[批量发布 NuGet 包](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="23d5f-166">使用包</span><span class="sxs-lookup"><span data-stu-id="23d5f-166">Working with packages</span></span>

<span data-ttu-id="23d5f-167">项目级包和解决方案级包之间有何差异？</span><span class="sxs-lookup"><span data-stu-id="23d5f-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="23d5f-168">解决方案级包 (NuGet 3.x+) 只需在解决方案上安装一次，随后即可用于该解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="23d5f-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="23d5f-169">项目级包需在使用它的每个项目中进行安装。</span><span class="sxs-lookup"><span data-stu-id="23d5f-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="23d5f-170">解决方案级包还可以安装可从包管理器控制台中调用的新命令。</span><span class="sxs-lookup"><span data-stu-id="23d5f-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="23d5f-171">是否可以在没有 Internet 连接时安装 NuGet 包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="23d5f-172">可以，请参阅 Scott Hanselman 的博客文章 [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)（如何在 nuget.org 不可用（或用户在飞机上）时访问 NuGet）(hanselman.com)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="23d5f-173">如何在默认包文件夹以外的其他位置安装包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="23d5f-174">请使用 `nuget config -set repositoryPath=<path>` 设置 `Nuget.Config` 中的 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 设置。</span><span class="sxs-lookup"><span data-stu-id="23d5f-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="23d5f-175">如何避免将 NuGet 包文件夹中添加到源代码管理中？</span><span class="sxs-lookup"><span data-stu-id="23d5f-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="23d5f-176">请将 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="23d5f-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="23d5f-177">此密钥适用于解决方案级别，因此需要添加到 `$(Solutiondir)\.nuget\Nuget.Config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="23d5f-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="23d5f-178">从 Visual Studio 中启用包还原将自动创建此文件。</span><span class="sxs-lookup"><span data-stu-id="23d5f-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="23d5f-179">如何关闭包还原？</span><span class="sxs-lookup"><span data-stu-id="23d5f-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="23d5f-180">请参阅[启用和禁用包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="23d5f-181">安装具有远程依赖项的本地包时，为何会出现“无法解析依赖项”错误？</span><span class="sxs-lookup"><span data-stu-id="23d5f-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="23d5f-182">将本地包安装到项目中时，需要选择“所有”源。</span><span class="sxs-lookup"><span data-stu-id="23d5f-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="23d5f-183">这样可以聚合所有源，而不只是一个源。</span><span class="sxs-lookup"><span data-stu-id="23d5f-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="23d5f-184">本地存储库用户通常不希望因为公司政策而意外安装远程包，因此才会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="23d5f-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="23d5f-185">如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 文件？</span><span class="sxs-lookup"><span data-stu-id="23d5f-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="23d5f-186">对于各个项目位于单独文件夹中的大多数项目，用户不必考虑此问题，因为 NuGet 会识别每个项目中的 `packages.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="23d5f-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="23d5f-187">如果使用 NuGet 3.3+ 并且同一文件夹中有多个项目，可将项目名称插入 `packages.config` 文件名（使用 `packages.{project-name}.config` 模式），然后 NuGet 将使用该文件。</span><span class="sxs-lookup"><span data-stu-id="23d5f-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="23d5f-188">使用 PackageReference 时不必考虑此问题，因为每个项目文件仅包含自己的依赖项列表。</span><span class="sxs-lookup"><span data-stu-id="23d5f-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="23d5f-189">存储库列表中未显示 nuget.org，应如何让其重新显示？</span><span class="sxs-lookup"><span data-stu-id="23d5f-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="23d5f-190">将 `https://api.nuget.org/v3/index.json` 添加到源列表；或</span><span class="sxs-lookup"><span data-stu-id="23d5f-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="23d5f-191">删除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 并指示 NuGet 重新创建它。</span><span class="sxs-lookup"><span data-stu-id="23d5f-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="23d5f-192">如果包未提供特定许可信息，有哪些默认许可条款？</span><span class="sxs-lookup"><span data-stu-id="23d5f-192">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="23d5f-193">每个包都需要受包中所含条款约束。</span><span class="sxs-lookup"><span data-stu-id="23d5f-193">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="23d5f-194">你应该在访问、下载或获取任何包前查看适用条款。</span><span class="sxs-lookup"><span data-stu-id="23d5f-194">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="23d5f-195">在 nuget.org 中，请使用包页面中的“许可信息”链接。</span><span class="sxs-lookup"><span data-stu-id="23d5f-195">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="23d5f-196">如果包未指定许可条款，请直接通过 nuget.org 包页面上的“联系所有者”链接与包所有者联系。</span><span class="sxs-lookup"><span data-stu-id="23d5f-196">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="23d5f-197">Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。</span><span class="sxs-lookup"><span data-stu-id="23d5f-197">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="23d5f-198">在 nuget.org 上管理包</span><span class="sxs-lookup"><span data-stu-id="23d5f-198">Managing packages on nuget.org</span></span>

<span data-ttu-id="23d5f-199">在上传包元数据后是否可以再对其进行编辑？</span><span class="sxs-lookup"><span data-stu-id="23d5f-199">**Can I edit package metadata after it's been uploaded?**</span></span>

<span data-ttu-id="23d5f-200">NuGet 建议对所有的包签名。</span><span class="sxs-lookup"><span data-stu-id="23d5f-200">NuGet recommends all packages to be signed.</span></span> <span data-ttu-id="23d5f-201">包签名的设计原则是已签名包的内容不得改变，nuspec 也包括在内。</span><span class="sxs-lookup"><span data-stu-id="23d5f-201">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="23d5f-202">编辑包元数据会使 nuspec 发生更改，导致现有签名无效。</span><span class="sxs-lookup"><span data-stu-id="23d5f-202">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="23d5f-203">我们建议在创建包后修改现有工作流，这样则无需编辑包元数据。</span><span class="sxs-lookup"><span data-stu-id="23d5f-203">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="23d5f-204">请注意，列出的包依赖项从包本身自动生成，并且无法进行编辑。</span><span class="sxs-lookup"><span data-stu-id="23d5f-204">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="23d5f-205">此外，要测试和验证包，同时不在公共库中提供此包，最好将包上传到 [staging.nuget.org](http://staging.nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-205">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="23d5f-206">是否可以为以后发布的包预留名称？</span><span class="sxs-lookup"><span data-stu-id="23d5f-206">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="23d5f-207">可以。</span><span class="sxs-lookup"><span data-stu-id="23d5f-207">Yes.</span></span> <span data-ttu-id="23d5f-208">通过为帐户请求包 ID 前缀可以在 [nuget.org](https://www.nuget.org/) 中预留包 ID。</span><span class="sxs-lookup"><span data-stu-id="23d5f-208">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="23d5f-209">若要请求包 ID 前缀，请按照[文档](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="23d5f-209">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="23d5f-210">如何声明包的所有权？</span><span class="sxs-lookup"><span data-stu-id="23d5f-210">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="23d5f-211">请参阅[在 nuget.org 上管理包所有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-211">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="23d5f-212">如何与违反我的软件许可的包所有者进行交涉？</span><span class="sxs-lookup"><span data-stu-id="23d5f-212">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="23d5f-213">我们鼓励 NuGet 社区合作解决包所有者和其他软件所有者之间可能出现的任何争议。</span><span class="sxs-lookup"><span data-stu-id="23d5f-213">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="23d5f-214">我们制定了周密的[争议解决流程](../policies/dispute-resolution.md)，要求 nuget.org 管理员调解之前应遵循此流程。</span><span class="sxs-lookup"><span data-stu-id="23d5f-214">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="23d5f-215">是否建议将测试包上传到 nuget.org？</span><span class="sxs-lookup"><span data-stu-id="23d5f-215">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="23d5f-216">对于测试目的，可以使用 [staging.nuget.org](http://staging.nuget.org)，或使用备用的公共 NuGet 服务器，如 [myget.org](https://myget.org) 或 [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-216">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="23d5f-217">请注意，上传到 staging.nuget.org 的包可能不会保留。</span><span class="sxs-lookup"><span data-stu-id="23d5f-217">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="23d5f-218">请参阅[告别预览版](http://blog.nuget.org/20130419/goodbye-preview.html)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-218">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="23d5f-219">可上传到 nuget.org 的最大包大小是多少？</span><span class="sxs-lookup"><span data-stu-id="23d5f-219">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="23d5f-220">nuget.org 允许的最大包大小为 250 MB，但我们建议尽可能将包保持在 1 MB 以下，通过依赖项将包链接在一起。</span><span class="sxs-lookup"><span data-stu-id="23d5f-220">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="23d5f-221">依据经验，仅包含一个程序集的包可以避免冲突。</span><span class="sxs-lookup"><span data-stu-id="23d5f-221">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="23d5f-222">NuGet 使用 HTTP 下载包，因此较大包比较小包有更高的安装失败风险。</span><span class="sxs-lookup"><span data-stu-id="23d5f-222">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="23d5f-223">依赖项可以在多个包之间进行共享，这样可减小 NuGet 包使用者的总下载大小。</span><span class="sxs-lookup"><span data-stu-id="23d5f-223">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="23d5f-224">依赖项通常是静态的，永远不会更改。</span><span class="sxs-lookup"><span data-stu-id="23d5f-224">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="23d5f-225">修复代码中的 bug 时，可能无需更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="23d5f-225">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="23d5f-226">如果捆绑依赖项，最终将导致每一次都需要重新传输更大的包。</span><span class="sxs-lookup"><span data-stu-id="23d5f-226">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="23d5f-227">通过将 NuGet 包拆分成相关的依赖项，包使用者可以获得更细化的更新。</span><span class="sxs-lookup"><span data-stu-id="23d5f-227">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="23d5f-228">nuget.org 不可访问</span><span class="sxs-lookup"><span data-stu-id="23d5f-228">nuget.org not accessible</span></span>

<span data-ttu-id="23d5f-229">为何无法从 nuget.org 下载包或向其中上传包？</span><span class="sxs-lookup"><span data-stu-id="23d5f-229">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="23d5f-230">首先，请确保使用的是最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="23d5f-230">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="23d5f-231">如果该版本仍然失败，请[联系支持人员](https://www.nuget.org/policies/Contact)，并提供其他连接故障排除信息，包括：</span><span class="sxs-lookup"><span data-stu-id="23d5f-231">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="23d5f-232">使用的 NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="23d5f-232">The version of NuGet you're using</span></span>
- <span data-ttu-id="23d5f-233">使用的包源</span><span class="sxs-lookup"><span data-stu-id="23d5f-233">The package sources you're using</span></span>
- <span data-ttu-id="23d5f-234">详细还原日志</span><span class="sxs-lookup"><span data-stu-id="23d5f-234">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="23d5f-235">MTR 或 Fiddler 跟踪（见下文）</span><span class="sxs-lookup"><span data-stu-id="23d5f-235">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="23d5f-236">所在地理区域</span><span class="sxs-lookup"><span data-stu-id="23d5f-236">Your geographical area</span></span>
- <span data-ttu-id="23d5f-237">操作系统版本</span><span class="sxs-lookup"><span data-stu-id="23d5f-237">Your operating system version</span></span>
- <span data-ttu-id="23d5f-238">计算机配置（CPU、网络、硬盘驱动器）</span><span class="sxs-lookup"><span data-stu-id="23d5f-238">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="23d5f-239">计算机是否设置了代理或防火墙</span><span class="sxs-lookup"><span data-stu-id="23d5f-239">Whether your machine is behind a proxy or firewall</span></span>
- <span data-ttu-id="23d5f-240">计算机上安装的 .NET 版本</span><span class="sxs-lookup"><span data-stu-id="23d5f-240">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="23d5f-241">使用的跨平台工具（如 .NET CLI 或 DNU）的版本</span><span class="sxs-lookup"><span data-stu-id="23d5f-241">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="23d5f-242">捕获 MTR：</span><span class="sxs-lookup"><span data-stu-id="23d5f-242">*To capture MTR:*</span></span>

- <span data-ttu-id="23d5f-243">从 [http://winmtr.net/download/](http://winmtr.net/) 下载 WinMTR</span><span class="sxs-lookup"><span data-stu-id="23d5f-243">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="23d5f-244">输入 `api.nuget.org` 作为主机名，然后单击“启动”。</span><span class="sxs-lookup"><span data-stu-id="23d5f-244">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="23d5f-245">等待，直到“已发送”列 >= 100。</span><span class="sxs-lookup"><span data-stu-id="23d5f-245">Wait until the **Sent** column is >= 100.</span></span>

    ![捕获 MTR](media/mtr.png)

- <span data-ttu-id="23d5f-247">将文本复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="23d5f-247">Copy text to clipboard.</span></span>

<span data-ttu-id="23d5f-248">捕获 Fiddler：</span><span class="sxs-lookup"><span data-stu-id="23d5f-248">*To capture Fiddler:*</span></span>

- <span data-ttu-id="23d5f-249">安装最新版本的 [Fiddler](http://www.telerik.com/download/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-249">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="23d5f-250">启动 Fiddler，使用“文件”>“捕获流量”菜单禁用捕获流量。</span><span class="sxs-lookup"><span data-stu-id="23d5f-250">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="23d5f-251">删除所有会话（选中列表中的所有项，按 Delete 键）。</span><span class="sxs-lookup"><span data-stu-id="23d5f-251">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="23d5f-252">配置 Fiddler 以捕获 HTTPS 流量，具体操作方式为：打开“工具”>“Fiddler 选项...”菜单，勾选“HTTPS”选项卡中的“解密 HTTPS 流量”。</span><span class="sxs-lookup"><span data-stu-id="23d5f-252">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="23d5f-253">关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="23d5f-253">Close Visual Studio.</span></span>
- <span data-ttu-id="23d5f-254">启用“文件”>“捕获流量”菜单。</span><span class="sxs-lookup"><span data-stu-id="23d5f-254">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="23d5f-255">启动 Visual Studio 或 nuget.exe.exe，执行当前未运行的操作。</span><span class="sxs-lookup"><span data-stu-id="23d5f-255">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="23d5f-256">Fiddler 中应显示出这些操作所产生的流量。</span><span class="sxs-lookup"><span data-stu-id="23d5f-256">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="23d5f-257">操作运行结束后，使用“文件”>“保存”>“所有会话”来存储捕获的会话。</span><span class="sxs-lookup"><span data-stu-id="23d5f-257">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="23d5f-258">注意：若要通过 Fiddler 路由 NuGet，可能需要将 `HTTP_PROXY` 环境变量设置为 `http://127.0.0.1:8888`。</span><span class="sxs-lookup"><span data-stu-id="23d5f-258">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="23d5f-259">如果该操作失败，请尝试[该 StackOverflow 文章中提到的方法](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。</span><span class="sxs-lookup"><span data-stu-id="23d5f-259">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="23d5f-260">有哪些适用于 nuget.org 的 API 终结点？</span><span class="sxs-lookup"><span data-stu-id="23d5f-260">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="23d5f-261">V3：`https://api.nuget.org/v3/index.json` V2：`https://www.nuget.org/api/v2/`（请注意，V2 API 已弃用并且不适用于 NuGet 4+。）</span><span class="sxs-lookup"><span data-stu-id="23d5f-261">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
