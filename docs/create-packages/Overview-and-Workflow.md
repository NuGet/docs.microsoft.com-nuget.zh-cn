---
title: 创建 NuGet 包的概述和工作流
description: 概述创建和发布 NuGet 包的流程，其中提供该流程其他特定部分的链接。
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488847"
---
# <a name="package-creation-workflow"></a><span data-ttu-id="dd8c7-103">包创建工作流</span><span class="sxs-lookup"><span data-stu-id="dd8c7-103">Package creation workflow</span></span>

<span data-ttu-id="dd8c7-104">通过公共 nuget.org 库或组织内部的私有库，创建你要进行打包并与他人共享的、以编译代码（通常为 .NET 程序集）开头的包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-104">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="dd8c7-105">此包还可以包含其他文件（如安装包时显示的自述文件）以及特定项目文件的转换文件。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-105">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="dd8c7-106">包还可仅用于拉入任意数量的其他依赖项，但不包含其自己的任何代码。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-106">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="dd8c7-107">利用这种包可以轻松传递由多个独立包组成的 SDK。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-107">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="dd8c7-108">在其他情况下，包可能仅包含用于协助调试的符号 (`.pdb`) 文件。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-108">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="dd8c7-109">如果要创建供其他开发人员使用的包，则务必了解他们将依赖于你的工作成果。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-109">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="dd8c7-110">因此，创建并发布包也表示你将修复 bug 和提供其他更新，或者至少应以开源形式提供包，以便他人可帮助维护包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-110">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="dd8c7-111">无论哪种情况，都要从决定其标识符、版本号、许可证、版权信息和任何其他必要内容开始创建包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-111">Whatever the case, creating a package begins with deciding its identifier, version number, license, copyright information, and any other necessary content.</span></span> <span data-ttu-id="dd8c7-112">完成后，可以使用“pack”命令将所有内容放到 `.nupkg` 文件中。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-112">Once done, you can use the "pack" command to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="dd8c7-113">可以将此文件发布到 NuGet 源，如 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-113">This file can be published to a NuGet feed, like nuget.org.</span></span>

> [!Tip]
> <span data-ttu-id="dd8c7-114">具有 `.nupkg` 扩展名的 NuGet 包只是一个 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-114">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="dd8c7-115">若要轻松查看任何包的内容，只需将扩展名更改为 `.zip` 并按常规方法展开内容。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-115">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="dd8c7-116">尝试将包上传到主机前，请务必将扩展名改回 `.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-116">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="dd8c7-117">若想了解并掌握创建流程，请首先参阅[创建包](../create-packages/creating-a-package.md)，其中针对适用于所有包的核心流程提供了完整说明。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-117">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span>

<span data-ttu-id="dd8c7-118">接下来，你可以考虑对包应用其他多种选项：</span><span class="sxs-lookup"><span data-stu-id="dd8c7-118">From there, you can consider a number of other options for your package:</span></span>

- <span data-ttu-id="dd8c7-119">[支持多目标框架](../create-packages/supporting-multiple-target-frameworks.md)，说明如何创建具有面向不同 .NET Framework 的多个变体的包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-119">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
- <span data-ttu-id="dd8c7-120">[创建本地化包](../create-packages/creating-localized-packages.md)，说明如何构建具有多个语言资源的包以及如何使用独立的本地化附属包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-120">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
- <span data-ttu-id="dd8c7-121">[预发行包](../create-packages/prerelease-packages.md)，演示如何向感兴趣的客户发布 alpha、beta 和 rc 版本的包。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-121">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
- <span data-ttu-id="dd8c7-122">[源和配置文件转换](../create-packages/source-and-config-file-transformations.md)，说明如何在已添加到项目的文件中执行两种单向令牌替换，以及如何修改 `web.config` 和 `app.config`（卸载包时还将舍弃这两者的设置）。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-122">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
- <span data-ttu-id="dd8c7-123">[符号包](../create-packages/symbol-packages-snupkg.md)，说明如何为库提供符号以允许使用者在调试期间单步执行代码。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-123">[Symbol Packages](../create-packages/symbol-packages-snupkg.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
- <span data-ttu-id="dd8c7-124">[包版本控制](../concepts/package-versioning.md)，说明如何识别依赖项（通过你的包所使用的其他包）所需的确切版本。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-124">[Package versioning](../concepts/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
- <span data-ttu-id="dd8c7-125">[本机包](../guides/native-packages.md)，说明面向 C++ 使用者创建包的流程。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-125">[Native Packages](../guides/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>
- <span data-ttu-id="dd8c7-126">[签名包](../create-packages/sign-a-package.md)，说明向包添加数字签名的流程。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-126">[Signing Packages](../create-packages/sign-a-package.md) describes the process for adding a digital signature to a package.</span></span>

<span data-ttu-id="dd8c7-127">当准备好将包发布到 nuget.org 时，请按照[发布包](../nuget-org/publish-a-package.md)中的简单流程执行操作。</span><span class="sxs-lookup"><span data-stu-id="dd8c7-127">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="dd8c7-128">如果希望使用私有源而非 nuget.org，请参阅[托管包概述](../hosting-packages/overview.md)</span><span class="sxs-lookup"><span data-stu-id="dd8c7-128">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>
