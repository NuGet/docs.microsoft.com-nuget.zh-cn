---
title: 创建本机 NuGet 包
description: 详细介绍如何创建用于 C++ 项目中的包含 C++ 代码（而不是托管代码）的本机 NuGet 包。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774214"
---
# <a name="creating-native-packages"></a><span data-ttu-id="fb82e-103">创建本机包</span><span class="sxs-lookup"><span data-stu-id="fb82e-103">Creating native packages</span></span>

<span data-ttu-id="fb82e-104">本机包包含本机二进制文件（而不是托管程序集），因此可用于 C++（或类似）项目中。</span><span class="sxs-lookup"><span data-stu-id="fb82e-104">A native package contains native binaries instead of managed assemblies, allowing it to be used within C++ (or similar) projects.</span></span> <span data-ttu-id="fb82e-105">（请参阅“使用”部分中的[本机 C++ 包](../consume-packages/finding-and-choosing-packages.md#native-c-packages)。）</span><span class="sxs-lookup"><span data-stu-id="fb82e-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="fb82e-106">若要用于 C++ 项目中，包必须面向 `native` 框架。</span><span class="sxs-lookup"><span data-stu-id="fb82e-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="fb82e-107">目前不存在与此框架关联的任何版本号，因为 NuGet 对所有 C++ 项目的处理方式相同。</span><span class="sxs-lookup"><span data-stu-id="fb82e-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="fb82e-108">请确保在 `.nuspec` 的 `<tags>` 部分中包括本机，以便其他开发人员通过搜索该标记查找包。</span><span class="sxs-lookup"><span data-stu-id="fb82e-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="fb82e-109">然后，面向 `native` 的本机 NuGet 包在 `\build`、`\content` 和 `\tools` 文件夹中提供文件；此事例中没有使用 `\lib`（NuGet 不能直接向 C++ 项目添加引用）。</span><span class="sxs-lookup"><span data-stu-id="fb82e-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="fb82e-110">包还可能包括 `\build` 中的目标和属性文件，NuGet 会将这些内容自动导入到使用该包的项目中。</span><span class="sxs-lookup"><span data-stu-id="fb82e-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="fb82e-111">这些文件的名称必须与包 ID 的名称相同，包含 `.targets` 和/或 `.props` 扩展名。</span><span class="sxs-lookup"><span data-stu-id="fb82e-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="fb82e-112">例如，[cpprestsdk](https://nuget.org/packages/cpprestsdk/) 包在 `\build` 文件夹中包括 `cpprestsdk.targets` 文件。</span><span class="sxs-lookup"><span data-stu-id="fb82e-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="fb82e-113">`\build` 文件夹可用于所有 NuGet 包，并非仅用于本机包。</span><span class="sxs-lookup"><span data-stu-id="fb82e-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="fb82e-114">与 `\content`、`\lib` 和 `\tools` 文件夹相同，`\build` 文件夹也遵照目标框架。</span><span class="sxs-lookup"><span data-stu-id="fb82e-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="fb82e-115">这意味着可创建 `\build\net40` 文件夹和 `\build\net45` 文件夹，且 NuGet 会向项目中导入相应的属性和目标文件。</span><span class="sxs-lookup"><span data-stu-id="fb82e-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="fb82e-116">（无需使用 PowerShell 脚本导入 MSBuild 目标。）</span><span class="sxs-lookup"><span data-stu-id="fb82e-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
