---
title: NuGet project.json 存档内容
description: 从 NuGet 文档的其他区域中删除了 project.json 内容的其他位。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 5b5a5309f5b22f08c289aa49781fa44f95646153
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818329"
---
# <a name="projectjson-archive"></a><span data-ttu-id="69500-103">project.json 存档</span><span class="sxs-lookup"><span data-stu-id="69500-103">project.json archive</span></span>

<span data-ttu-id="69500-104">NuGet 3.x 引入了 `project.json` 管理格式，并用于某些项目类型。</span><span class="sxs-lookup"><span data-stu-id="69500-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="69500-105">该格式已被弃用，引入 PackageReference 格式，其中项目文件中直接列出了依赖项。</span><span class="sxs-lookup"><span data-stu-id="69500-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="69500-106">另请参见：</span><span class="sxs-lookup"><span data-stu-id="69500-106">Also see:</span></span>

- [<span data-ttu-id="69500-107">project.json 架构</span><span class="sxs-lookup"><span data-stu-id="69500-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="69500-108">project.json 对包作者的影响</span><span class="sxs-lookup"><span data-stu-id="69500-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="69500-109">project.json 和 UWP</span><span class="sxs-lookup"><span data-stu-id="69500-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="69500-110">project.json 管理格式</span><span class="sxs-lookup"><span data-stu-id="69500-110">project.json management format</span></span>

<span data-ttu-id="69500-111">*最初在[包还原](../what-is-nuget.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="69500-112">在管理格式列表中：</span><span class="sxs-lookup"><span data-stu-id="69500-112">In the list of management formats:</span></span>

- <span data-ttu-id="69500-113">[`project.json`](project-json.md)：*（已弃用）* 一种 JSON 文件，用于维护项目依赖项的列表，同时将包的整体信息图存储在关联文件 `project.lock.json` 中。</span><span class="sxs-lookup"><span data-stu-id="69500-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="69500-114">此格式已被弃用，被 PackageReference 取代。</span><span class="sxs-lookup"><span data-stu-id="69500-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="69500-115">Mono 上的 nuget 还原</span><span class="sxs-lookup"><span data-stu-id="69500-115">nuget restore on Mono</span></span>

<span data-ttu-id="69500-116">*最初在[安装 NuGet 客户端工具](../install-nuget-client-tools.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="69500-117">适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="69500-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="69500-118">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="69500-118">Constraining package versions with restore</span></span>

<span data-ttu-id="69500-119">*最初在[包还原](../consume-packages/package-restore.md#constraining-package-versions-with-restore)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="69500-120">`project.json` 使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="69500-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="69500-121">例如:</span><span class="sxs-lookup"><span data-stu-id="69500-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="69500-122">NuGet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="69500-122">NuGet CLI commands</span></span>

- <span data-ttu-id="69500-123">`nuget install` 不适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="69500-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="69500-124">`nuget restore`：对于使用 `project.json` 的项目，生成 `project.lock.json` 文件和 `<project>.nuget.props` 文件（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="69500-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="69500-125">（这两个文件在源代码管理中都可以忽略。）`<projectPath>` 参数可以指向 `project.json` 文件，并具有与指向 `packages.config` 或项目文件相同的行为。</span><span class="sxs-lookup"><span data-stu-id="69500-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="69500-126">在包文件夹的优先顺序中，使用 `project.json` 时首先搜索 `%userprofile%\.nuget\packages`。</span><span class="sxs-lookup"><span data-stu-id="69500-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="69500-127">`nuget update`：在 Mono 中，此命令不适用于使用 `project.json` 的项目。</span><span class="sxs-lookup"><span data-stu-id="69500-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="69500-128">利用 PackageReference 解析依赖项</span><span class="sxs-lookup"><span data-stu-id="69500-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="69500-129">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="69500-130">PackageReference 的行为也适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="69500-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="69500-131">NuGet 还原将依赖项关系图写入 `project.json` 旁边名为 `project.lock.json` 的文件。</span><span class="sxs-lookup"><span data-stu-id="69500-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="69500-132">管理依赖项资产</span><span class="sxs-lookup"><span data-stu-id="69500-132">Managing dependency assets</span></span>

<span data-ttu-id="69500-133">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#managing-dependency-assets)。*</span><span class="sxs-lookup"><span data-stu-id="69500-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="69500-134">使用 `project.json` 格式时，可以控制依赖项中的哪些资产可流入顶层项目。</span><span class="sxs-lookup"><span data-stu-id="69500-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="69500-135">有关详细信息，请参阅 [project.json](project-json.md)。</span><span class="sxs-lookup"><span data-stu-id="69500-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="69500-136">排除引用</span><span class="sxs-lookup"><span data-stu-id="69500-136">Excluding references</span></span>

<span data-ttu-id="69500-137">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#excluding-references)。*</span><span class="sxs-lookup"><span data-stu-id="69500-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="69500-138">`project.json`：在 PackageC 的依赖项中添加 `"exclude" : "all"`：</span><span class="sxs-lookup"><span data-stu-id="69500-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="69500-139">解决包不兼容错误</span><span class="sxs-lookup"><span data-stu-id="69500-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="69500-140">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)。*</span><span class="sxs-lookup"><span data-stu-id="69500-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="69500-141">增加的错误解决方式：</span><span class="sxs-lookup"><span data-stu-id="69500-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="69500-142">**不推荐做法**：作为与包创建者合作的临时解决方案，面向 `netcore`、`netstandard` 和 `netcoreapp` 的项目可以表示其他兼容框架，并因此允许使用面向其他框架的包。</span><span class="sxs-lookup"><span data-stu-id="69500-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="69500-143">请参阅 [project.json imports](project-json.md#imports) 和 [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback)。</span><span class="sxs-lookup"><span data-stu-id="69500-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="69500-144">这将导致意外行为，因此再次提醒，与包创建者协作是解决更新时遇到的包不兼容问题的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="69500-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="69500-145">目标框架</span><span class="sxs-lookup"><span data-stu-id="69500-145">Target frameworks</span></span>

<span data-ttu-id="69500-146">*最初在[目标框架](../reference/target-frameworks.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="69500-147">[project.json](project-json.md)：`frameworks` 节点指定可编译项目的框架版本。</span><span class="sxs-lookup"><span data-stu-id="69500-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="69500-148">创建包</span><span class="sxs-lookup"><span data-stu-id="69500-148">Creating a package</span></span>

<span data-ttu-id="69500-149">*最初在[创建包](../create-packages/creating-a-package.md)中*</span><span class="sxs-lookup"><span data-stu-id="69500-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="69500-150">设置包类型</span><span class="sxs-lookup"><span data-stu-id="69500-150">Setting a package type</span></span>

<span data-ttu-id="69500-151">有了 .NET Core 1.x，安装 DotnetCliTool 包时，Visual Studio 将包置于 `project.json` `tools` 节点而不是 `dependencies` 节点中。</span><span class="sxs-lookup"><span data-stu-id="69500-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="69500-152">包类型在 `project.json` 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="69500-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="69500-153">`project.json`：指示 `packOptions.packageType` 属性 json 中的包类型：</span><span class="sxs-lookup"><span data-stu-id="69500-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="69500-154">添加 MSBuild 的目标和属性</span><span class="sxs-lookup"><span data-stu-id="69500-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="69500-155">*最初在[使用 Visual Studio 2015 创建 .NET Standard NuGet 包](../guides/create-net-standard-packages-vs2015.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="69500-156">使用 `project.json` 时，目标不添加到项目，而是通过 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="69500-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="69500-157">包版本控制</span><span class="sxs-lookup"><span data-stu-id="69500-157">Package versioning</span></span>

<span data-ttu-id="69500-158">*最初在[包版本控制](../reference/package-versioning.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="69500-159">使用 `project.json` 格式时，NuGet 还支持使用通配符表示法 \* 来表示版本号的主要、次要、修补程序和预发布后缀部分。</span><span class="sxs-lookup"><span data-stu-id="69500-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="69500-160">NuGet.Config 引用</span><span class="sxs-lookup"><span data-stu-id="69500-160">NuGet.Config reference</span></span>

<span data-ttu-id="69500-161">*最初在 [NuGet.Config 引用](../reference/nuget-config-file.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="69500-162">`globalPackagesFolder` 仅适用于 `project.json`</span><span class="sxs-lookup"><span data-stu-id="69500-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="69500-163">（添加的说明：也适用于 PackageReference。）</span><span class="sxs-lookup"><span data-stu-id="69500-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="69500-164">nuspec 文件引用</span><span class="sxs-lookup"><span data-stu-id="69500-164">nuspec file reference</span></span>

<span data-ttu-id="69500-165">*最初在 [nuspec 引用](../reference/nuspec.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="69500-166">`project.json` 使用 `<contentFiles>` 元素替代 `<files>`。</span><span class="sxs-lookup"><span data-stu-id="69500-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="69500-167">程序包管理器选项控件</span><span class="sxs-lookup"><span data-stu-id="69500-167">Package manager options control</span></span>

<span data-ttu-id="69500-168">*最初在[程序包管理器 UI 引用](../tools/package-manager-ui.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="69500-169">使用 `project.json` 管理格式的项目仅显示“显示预览窗口”选项。</span><span class="sxs-lookup"><span data-stu-id="69500-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="69500-170">Visual Studio 模板</span><span class="sxs-lookup"><span data-stu-id="69500-170">Visual Studio Templates</span></span>

<span data-ttu-id="69500-171">*最初在 [Visual Studio 模板中的 NuGet 包](../visual-studio-extensibility/visual-studio-templates.md)中。*</span><span class="sxs-lookup"><span data-stu-id="69500-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="69500-172">最佳做法：模板不包括 `project.json` 文件，也不包括安装 NuGet 包时将添加的任何引用或内容。</span><span class="sxs-lookup"><span data-stu-id="69500-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>