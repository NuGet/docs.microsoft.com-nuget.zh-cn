---
title: NuGet project.json 存档内容 | Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 从 NuGet 文档的其他区域中删除了 project.json 内容的其他位。
keywords: NuGet project.json 文件
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="eed65-104">project.json 存档</span><span class="sxs-lookup"><span data-stu-id="eed65-104">project.json archive</span></span>

<span data-ttu-id="eed65-105">NuGet 3.x 引入了 `project.json` 管理格式，并用于某些项目类型。</span><span class="sxs-lookup"><span data-stu-id="eed65-105">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="eed65-106">该格式已被弃用，引入 PackageReference 格式，其中项目文件中直接列出了依赖项。</span><span class="sxs-lookup"><span data-stu-id="eed65-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="eed65-107">另请参见：</span><span class="sxs-lookup"><span data-stu-id="eed65-107">Also see:</span></span>

- [<span data-ttu-id="eed65-108">project.json 架构</span><span class="sxs-lookup"><span data-stu-id="eed65-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="eed65-109">project.json 对包作者的影响</span><span class="sxs-lookup"><span data-stu-id="eed65-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="eed65-110">project.json 和 UWP</span><span class="sxs-lookup"><span data-stu-id="eed65-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="eed65-111">project.json 管理格式</span><span class="sxs-lookup"><span data-stu-id="eed65-111">project.json management format</span></span>

<span data-ttu-id="eed65-112">*最初在[包还原](../what-is-nuget.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="eed65-113">在管理格式列表中：</span><span class="sxs-lookup"><span data-stu-id="eed65-113">In the list of management formats:</span></span>

- <span data-ttu-id="eed65-114">[`project.json`](project-json.md)：*（已弃用）*一种 JSON 文件，用于维护项目依赖项的列表，同时将包的整体信息图存储在关联文件 `project.lock.json` 中。</span><span class="sxs-lookup"><span data-stu-id="eed65-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="eed65-115">此格式已被弃用，被 PackageReference 取代。</span><span class="sxs-lookup"><span data-stu-id="eed65-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="eed65-116">Mono 上的 nuget 还原</span><span class="sxs-lookup"><span data-stu-id="eed65-116">nuget restore on Mono</span></span>

<span data-ttu-id="eed65-117">*最初在[安装 NuGet 客户端工具](../install-nuget-client-tools.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="eed65-118">适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="eed65-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="eed65-119">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="eed65-119">Constraining package versions with restore</span></span>

<span data-ttu-id="eed65-120">*最初在[包还原](../consume-packages/package-restore.md#constraining-package-versions-with-restore)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="eed65-121">`project.json` 使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="eed65-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="eed65-122">例如:</span><span class="sxs-lookup"><span data-stu-id="eed65-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="eed65-123">NuGet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="eed65-123">NuGet CLI commands</span></span>

- <span data-ttu-id="eed65-124">`nuget install` 不适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="eed65-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="eed65-125">`nuget restore`：对于使用 `project.json` 的项目，生成 `project.lock.json` 文件和 `<project>.nuget.props` 文件（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="eed65-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="eed65-126">（这两个文件在源代码管理中都可以忽略。）`<projectPath>` 参数可以指向 `project.json` 文件，并具有与指向 `packages.config` 或项目文件相同的行为。</span><span class="sxs-lookup"><span data-stu-id="eed65-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="eed65-127">在包文件夹的优先顺序中，使用 `project.json` 时首先搜索 `%userprofile%\.nuget\packages`。</span><span class="sxs-lookup"><span data-stu-id="eed65-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="eed65-128">`nuget update`：在 Mono 中，此命令不适用于使用 `project.json` 的项目。</span><span class="sxs-lookup"><span data-stu-id="eed65-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="eed65-129">利用 PackageReference 解析依赖项</span><span class="sxs-lookup"><span data-stu-id="eed65-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="eed65-130">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="eed65-131">PackageReference 的行为也适用于 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="eed65-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="eed65-132">NuGet 还原将依赖项关系图写入 `project.json` 旁边名为 `project.lock.json` 的文件。</span><span class="sxs-lookup"><span data-stu-id="eed65-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="eed65-133">管理依赖项资产</span><span class="sxs-lookup"><span data-stu-id="eed65-133">Managing dependency assets</span></span>

<span data-ttu-id="eed65-134">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#managing-dependency-assets)。*</span><span class="sxs-lookup"><span data-stu-id="eed65-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="eed65-135">使用 `project.json` 格式时，可以控制依赖项中的哪些资产可流入顶层项目。</span><span class="sxs-lookup"><span data-stu-id="eed65-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="eed65-136">有关详细信息，请参阅 [project.json](project-json.md)。</span><span class="sxs-lookup"><span data-stu-id="eed65-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="eed65-137">排除引用</span><span class="sxs-lookup"><span data-stu-id="eed65-137">Excluding references</span></span>

<span data-ttu-id="eed65-138">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#excluding-references)。*</span><span class="sxs-lookup"><span data-stu-id="eed65-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="eed65-139">`project.json`：在 PackageC 的依赖项中添加 `"exclude" : "all"`：</span><span class="sxs-lookup"><span data-stu-id="eed65-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="eed65-140">解决包不兼容错误</span><span class="sxs-lookup"><span data-stu-id="eed65-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="eed65-141">*最初在[依赖项解析](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)。*</span><span class="sxs-lookup"><span data-stu-id="eed65-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="eed65-142">增加的错误解决方式：</span><span class="sxs-lookup"><span data-stu-id="eed65-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="eed65-143">**不推荐做法**：作为与包创建者合作的临时解决方案，面向 `netcore`、`netstandard` 和 `netcoreapp` 的项目可以表示其他兼容框架，并因此允许使用面向其他框架的包。</span><span class="sxs-lookup"><span data-stu-id="eed65-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="eed65-144">请参阅 [project.json imports](project-json.md#imports) 和 [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback)。</span><span class="sxs-lookup"><span data-stu-id="eed65-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="eed65-145">这将导致意外行为，因此再次提醒，与包创建者协作是解决更新时遇到的包不兼容问题的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="eed65-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="eed65-146">目标框架</span><span class="sxs-lookup"><span data-stu-id="eed65-146">Target frameworks</span></span>

<span data-ttu-id="eed65-147">*最初在[目标框架](../reference/target-frameworks.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="eed65-148">[project.json](project-json.md)：`frameworks` 节点指定可编译项目的框架版本。</span><span class="sxs-lookup"><span data-stu-id="eed65-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="eed65-149">创建包</span><span class="sxs-lookup"><span data-stu-id="eed65-149">Creating a package</span></span>

<span data-ttu-id="eed65-150">*最初在[创建包](../create-packages/creating-a-package.md)中*</span><span class="sxs-lookup"><span data-stu-id="eed65-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="eed65-151">设置包类型</span><span class="sxs-lookup"><span data-stu-id="eed65-151">Setting a package type</span></span>

<span data-ttu-id="eed65-152">有了 .NET Core 1.x，安装 DotnetCliTool 包时，Visual Studio 将包置于 `project.json` `tools` 节点而不是 `dependencies` 节点中。</span><span class="sxs-lookup"><span data-stu-id="eed65-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="eed65-153">包类型在 `project.json` 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="eed65-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="eed65-154">`project.json`：指示 `packOptions.packageType` 属性 json 中的包类型：</span><span class="sxs-lookup"><span data-stu-id="eed65-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="eed65-155">添加 MSBuild 的目标和属性</span><span class="sxs-lookup"><span data-stu-id="eed65-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="eed65-156">*最初在[使用 Visual Studio 2015 创建 .NET Standard NuGet 包](../guides/create-net-standard-packages-vs2015.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="eed65-157">使用 `project.json` 时，目标不添加到项目，而是通过 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="eed65-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="eed65-158">包版本控制</span><span class="sxs-lookup"><span data-stu-id="eed65-158">Package versioning</span></span>

<span data-ttu-id="eed65-159">*最初在[包版本控制](../reference/package-versioning.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="eed65-160">使用 `project.json` 格式时，NuGet 还支持使用通配符表示法 \* 来表示版本号的主要、次要、修补程序和预发布后缀部分。</span><span class="sxs-lookup"><span data-stu-id="eed65-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="eed65-161">NuGet.Config 引用</span><span class="sxs-lookup"><span data-stu-id="eed65-161">NuGet.Config reference</span></span>

<span data-ttu-id="eed65-162">*最初在 [NuGet.Config 引用](../reference/nuget-config-file.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="eed65-163">`globalPackagesFolder` 仅适用于 `project.json`</span><span class="sxs-lookup"><span data-stu-id="eed65-163">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="eed65-164">（添加的说明：也适用于 PackageReference。）</span><span class="sxs-lookup"><span data-stu-id="eed65-164">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="eed65-165">nuspec 文件引用</span><span class="sxs-lookup"><span data-stu-id="eed65-165">nuspec file reference</span></span>

<span data-ttu-id="eed65-166">*最初在 [nuspec 引用](../reference/nuspec.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-166">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="eed65-167">`project.json` 使用 `<contentFiles>` 元素替代 `<files>`。</span><span class="sxs-lookup"><span data-stu-id="eed65-167">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="eed65-168">程序包管理器选项控件</span><span class="sxs-lookup"><span data-stu-id="eed65-168">Package manager options control</span></span>

<span data-ttu-id="eed65-169">*最初在[程序包管理器 UI 引用](../tools/package-manager-ui.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-169">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="eed65-170">使用 `project.json` 管理格式的项目仅显示“显示预览窗口”选项。</span><span class="sxs-lookup"><span data-stu-id="eed65-170">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="eed65-171">Visual Studio 模板</span><span class="sxs-lookup"><span data-stu-id="eed65-171">Visual Studio Templates</span></span>

<span data-ttu-id="eed65-172">*最初在 [Visual Studio 模板中的 NuGet 包](../visual-studio-extensibility/visual-studio-templates.md)中。*</span><span class="sxs-lookup"><span data-stu-id="eed65-172">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="eed65-173">最佳做法：模板不包括 `project.json` 文件，也不包括安装 NuGet 包时将添加的任何引用或内容。</span><span class="sxs-lookup"><span data-stu-id="eed65-173">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>