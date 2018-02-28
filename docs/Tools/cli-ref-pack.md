---
title: "NuGet CLI 包命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 包命令参考"
keywords: "nuget 包引用，包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="c1ef6-104">包 (NuGet CLI) 命令</span><span class="sxs-lookup"><span data-stu-id="c1ef6-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="c1ef6-105">**适用于：** ，创建包&bullet;**受支持的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="c1ef6-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="c1ef6-106">创建根据指定的 NuGet 包`.nuspec`或项目文件。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="c1ef6-107">`dotnet pack`命令 (请参阅[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(请参阅[MSBuild 目标](../reference/msbuild-targets.md)) 可用作备用项。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="c1ef6-108">下单声道，从项目文件创建包不支持。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="c1ef6-109">你还需要调整中的非本地路径`.nuspec`文件于 Unix 样式的路径，如 nuget.exe 未转换 Windows 路径名本身。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="c1ef6-110">用法</span><span class="sxs-lookup"><span data-stu-id="c1ef6-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="c1ef6-111">其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或项目文件中，分别。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c1ef6-112">选项</span><span class="sxs-lookup"><span data-stu-id="c1ef6-112">Options</span></span>

| <span data-ttu-id="c1ef6-113">选项</span><span class="sxs-lookup"><span data-stu-id="c1ef6-113">Option</span></span> | <span data-ttu-id="c1ef6-114">描述</span><span class="sxs-lookup"><span data-stu-id="c1ef6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1ef6-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="c1ef6-115">BasePath</span></span> | <span data-ttu-id="c1ef6-116">设置中定义的文件的基路径`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c1ef6-117">生成</span><span class="sxs-lookup"><span data-stu-id="c1ef6-117">Build</span></span> | <span data-ttu-id="c1ef6-118">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="c1ef6-119">排除</span><span class="sxs-lookup"><span data-stu-id="c1ef6-119">Exclude</span></span> | <span data-ttu-id="c1ef6-120">指定一个或多个要在创建包时排除的通配符模式。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="c1ef6-121">若要指定多个模式，请重复-排除标志。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="c1ef6-122">请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-122">See example below.</span></span> |
| <span data-ttu-id="c1ef6-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="c1ef6-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="c1ef6-124">生成包时，可以防止包含空的目录。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="c1ef6-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c1ef6-125">ForceEnglishOutput</span></span> | <span data-ttu-id="c1ef6-126">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c1ef6-127">帮助</span><span class="sxs-lookup"><span data-stu-id="c1ef6-127">Help</span></span> | <span data-ttu-id="c1ef6-128">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="c1ef6-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="c1ef6-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="c1ef6-130">该值表示依赖关系或作为包的一部分，生成的包应包含引用的项目。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="c1ef6-131">如果所引用的项目都有一个相应`.nuspec`具有与项目中，相同的名称，则该引用的项目添加为依赖项的文件。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="c1ef6-132">否则，引用的项目将添加作为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="c1ef6-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c1ef6-133">MinClientVersion</span></span> | <span data-ttu-id="c1ef6-134">设置*minClientVersion*创建的包的属性。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="c1ef6-135">此值将重写现有值*minClientVersion*属性 （如果有） 中`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c1ef6-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c1ef6-136">MSBuildPath</span></span> | <span data-ttu-id="c1ef6-137">*（4.0 +)*指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c1ef6-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c1ef6-138">MSBuildVersion</span></span> | <span data-ttu-id="c1ef6-139">*（3.2 +)*指定要用于此命令的 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c1ef6-140">支持的值为 4、 12、 14、 15。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c1ef6-141">默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c1ef6-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="c1ef6-142">NoDefaultExcludes</span></span> | <span data-ttu-id="c1ef6-143">阻止的 NuGet 的默认排除包文件和文件和文件夹从一个点，如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="c1ef6-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c1ef6-144">NoPackageAnalysis</span></span> | <span data-ttu-id="c1ef6-145">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="c1ef6-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="c1ef6-146">OutputDirectory</span></span> | <span data-ttu-id="c1ef6-147">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="c1ef6-148">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="c1ef6-149">属性</span><span class="sxs-lookup"><span data-stu-id="c1ef6-149">Properties</span></span> | <span data-ttu-id="c1ef6-150">指定的重写项目文件; 中的值的属性的列表请参阅[常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)属性名称。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="c1ef6-151">此处的属性自变量是令牌的列表 = 值对，由分号分隔，其中的每个匹配项`$token$`中`.nuspec`文件将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="c1ef6-152">值可以是用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="c1ef6-153">请注意，对于"配置"属性中，默认值是"Debug"。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="c1ef6-154">若要将更改为发布配置，使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="c1ef6-155">后缀</span><span class="sxs-lookup"><span data-stu-id="c1ef6-155">Suffix</span></span> | <span data-ttu-id="c1ef6-156">*(3.4.4+)*将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="c1ef6-157">例如，使用`-suffix nightly`将创建具有版本数字类似的包`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="c1ef6-158">后缀必须以字母以避免警告、 错误和使用不同版本的 NuGet 和 NuGet 包管理器不兼容的潜在问题开头。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="c1ef6-159">符号</span><span class="sxs-lookup"><span data-stu-id="c1ef6-159">Symbols</span></span> | <span data-ttu-id="c1ef6-160">指定包中包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="c1ef6-161">如果用于`.nuspec`文件，这将创建常规的 NuGet 包文件和相应符号包。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="c1ef6-162">工具</span><span class="sxs-lookup"><span data-stu-id="c1ef6-162">Tool</span></span> | <span data-ttu-id="c1ef6-163">指定应将项目的输出文件放在`tool`文件夹。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="c1ef6-164">详细级别</span><span class="sxs-lookup"><span data-stu-id="c1ef6-164">Verbosity</span></span> | <span data-ttu-id="c1ef6-165">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="c1ef6-166">版本</span><span class="sxs-lookup"><span data-stu-id="c1ef6-166">Version</span></span> | <span data-ttu-id="c1ef6-167">重写从版本号`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="c1ef6-168">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c1ef6-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="c1ef6-169">排除开发依赖项</span><span class="sxs-lookup"><span data-stu-id="c1ef6-169">Excluding development dependencies</span></span>

<span data-ttu-id="c1ef6-170">一些 NuGet 程序包都可用作开发依赖关系，可帮助你创作你自己的库，但不一定需要实际包依赖关系。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="c1ef6-171">`pack`命令将忽略`package`中的条目`packages.config`具有`developmentDependency`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="c1ef6-172">这些项将不包括作为中创建的包的依赖关系中。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="c1ef6-173">例如，考虑以下`packages.config`源项目文件中：</span><span class="sxs-lookup"><span data-stu-id="c1ef6-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="c1ef6-174">对于此项目，包创建的`nuget pack`将具有依赖关系`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="c1ef6-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="c1ef6-175">示例</span><span class="sxs-lookup"><span data-stu-id="c1ef6-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
