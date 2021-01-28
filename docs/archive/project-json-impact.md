---
title: project.json 对 NuGet 包作者的影响
description: 详细介绍 NuGet 3.x 中的 project.json 实现如何影响包作者，如不支持的功能、内容和包格式。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 82b7ce7962ecccc9559ae25a8fe35a3820238049
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775383"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="74873-103">创建包时 project.json 产生的影响</span><span class="sxs-lookup"><span data-stu-id="74873-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="74873-104">此内容已弃用。</span><span class="sxs-lookup"><span data-stu-id="74873-104">This content is deprecated.</span></span> <span data-ttu-id="74873-105">项目应使用 `packages.config` 或 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="74873-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="74873-106">NuGet 3+ 中使用的 `project.json` 系统通过多种方式影响包作者，这些内容将在后续部分介绍。</span><span class="sxs-lookup"><span data-stu-id="74873-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="74873-107">影响现有包使用的更改</span><span class="sxs-lookup"><span data-stu-id="74873-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="74873-108">传统的 NuGet 包支持一系列不会传送到可传递体系的功能。</span><span class="sxs-lookup"><span data-stu-id="74873-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="74873-109">忽略了安装和卸载脚本</span><span class="sxs-lookup"><span data-stu-id="74873-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="74873-110">[依赖项解析](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)中介绍的可传递还原模型不具有“包安装时间”概念。</span><span class="sxs-lookup"><span data-stu-id="74873-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="74873-111">包的状态为存在或不存在，但安装包后不会出现一致的进程。</span><span class="sxs-lookup"><span data-stu-id="74873-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="74873-112">此外，仅 Visual Studio 支持安装脚本。</span><span class="sxs-lookup"><span data-stu-id="74873-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="74873-113">其他 IDE 必须模拟 Visual Studio 扩展性 API 以尝试支持此类脚本，且在常见编辑器和命令行工具中不提供支持。</span><span class="sxs-lookup"><span data-stu-id="74873-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="74873-114">不支持转换内容。</span><span class="sxs-lookup"><span data-stu-id="74873-114">Content transforms are not supported</span></span>

<span data-ttu-id="74873-115">与安装脚本相似，转换在包安装上运行，且通常不是幂等的。</span><span class="sxs-lookup"><span data-stu-id="74873-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="74873-116">由于不再存在安装时间，XDT 转换和类似功能不受支持，并且如果在可传递方案中使用了此类包，则会忽略前述转换和功能。</span><span class="sxs-lookup"><span data-stu-id="74873-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="74873-117">内容</span><span class="sxs-lookup"><span data-stu-id="74873-117">Content</span></span>

<span data-ttu-id="74873-118">传统的 NuGet 包传送源代码和配置文件之类的内容文件。</span><span class="sxs-lookup"><span data-stu-id="74873-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="74873-119">通常用于以下两个方案：</span><span class="sxs-lookup"><span data-stu-id="74873-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="74873-120">将初始文件放置到项目中，以便用户稍后进行编辑。</span><span class="sxs-lookup"><span data-stu-id="74873-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="74873-121">常见示例是默认配置文件。</span><span class="sxs-lookup"><span data-stu-id="74873-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="74873-122">将内容文件用作项目中所安装程序集的辅助文件。</span><span class="sxs-lookup"><span data-stu-id="74873-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="74873-123">示例是程序集使用的徽标图像。</span><span class="sxs-lookup"><span data-stu-id="74873-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="74873-124">目前禁用了对内容的支持，其原因与不支持脚本和转换的原因相似，但我们正在设计对内容的支持。</span><span class="sxs-lookup"><span data-stu-id="74873-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="74873-125">内容文件仍可以在包中进行传送，且此类文件目前被忽略，但是最终用户仍可以将其复制到适当的位置。</span><span class="sxs-lookup"><span data-stu-id="74873-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="74873-126">可在此处查看恢复内容文件的其中一项建议并跟踪其进度：[https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)。</span><span class="sxs-lookup"><span data-stu-id="74873-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="74873-127">对包作者的影响</span><span class="sxs-lookup"><span data-stu-id="74873-127">Impact for package authors</span></span>

<span data-ttu-id="74873-128">使用上述功能的包必须使用不同的机制。</span><span class="sxs-lookup"><span data-stu-id="74873-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="74873-129">对此最常用的有用机制是继续受到完全支持的 MSBuild 目标/属性。</span><span class="sxs-lookup"><span data-stu-id="74873-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="74873-130">生成系统可以选择在包中选取其他约定。</span><span class="sxs-lookup"><span data-stu-id="74873-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="74873-131">这样便可实现 MSBuild 目标和 Roslyn 分析器支持。</span><span class="sxs-lookup"><span data-stu-id="74873-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="74873-132">可以生成支持适用于 `packages.config` 和 `project.json` 方案的目标和分析器的包。</span><span class="sxs-lookup"><span data-stu-id="74873-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="74873-133">尝试修改项目以简化启动的包通常用于一组非常有限的方案，且应改为提供自述文件或包的使用方法指南。</span><span class="sxs-lookup"><span data-stu-id="74873-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="74873-134">大多数现有包都无需使用下文介绍的包格式。</span><span class="sxs-lookup"><span data-stu-id="74873-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="74873-135">格式使得本机内容作为优先方案。</span><span class="sxs-lookup"><span data-stu-id="74873-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="74873-136">这意味着，托管程序集依赖近硬件实现基于目标平台随托管程序集提供二进制实现。</span><span class="sxs-lookup"><span data-stu-id="74873-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="74873-137">例如，System.IO.Compression 包便是利用此技术。</span><span class="sxs-lookup"><span data-stu-id="74873-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="74873-138">总之，如果上述功能不是绝对必要，我们建议继续使用现有的包格式，因为仅 NuGet 3.x+ 支持此处介绍的格式。</span><span class="sxs-lookup"><span data-stu-id="74873-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="74873-139">可通过填充生成适用于 `packages.config` 和 `project.json` 方案的包，但以传统方式组织包的结构通常会更简单，无需上述弃用的功能。</span><span class="sxs-lookup"><span data-stu-id="74873-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="74873-140">3.x 包格式</span><span class="sxs-lookup"><span data-stu-id="74873-140">3.x package format</span></span>

<span data-ttu-id="74873-141">3\.x 包格式允许使用 NuGet 2.x 之外的其他几项功能：</span><span class="sxs-lookup"><span data-stu-id="74873-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="74873-142">定义一个引用程序集和一组实现程序集，前者用于编译，后者用于不同平台/设备上的运行时。</span><span class="sxs-lookup"><span data-stu-id="74873-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="74873-143">这样，你就可以利用平台特定的 API，同时为使用者提供常见的外围应用。</span><span class="sxs-lookup"><span data-stu-id="74873-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="74873-144">具体而言，这有助于更轻松地编写中间可移植库。</span><span class="sxs-lookup"><span data-stu-id="74873-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="74873-145">允许包在操作系统或 CPU 体系结构等平台上透视。</span><span class="sxs-lookup"><span data-stu-id="74873-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="74873-146">允许将平台特定的实现分离到辅助包中。</span><span class="sxs-lookup"><span data-stu-id="74873-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="74873-147">支持本机依赖项作为优先选项。</span><span class="sxs-lookup"><span data-stu-id="74873-147">Support Native dependencies as a first class citizen.</span></span>
