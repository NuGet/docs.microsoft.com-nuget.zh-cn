---
title: "NuGet CLI 包命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Nuget.exe 包命令参考"
keywords: "nuget 包引用，包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 22643ee4c7d5f858da728ba9d9d2886d600d20f0
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="c6d49-104">包 (NuGet CLI) 命令</span><span class="sxs-lookup"><span data-stu-id="c6d49-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="c6d49-105">**适用于：** ，创建包&bullet;**受支持的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="c6d49-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="c6d49-106">创建根据指定的 NuGet 包`.nuspec`或项目文件。</span><span class="sxs-lookup"><span data-stu-id="c6d49-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="c6d49-107">`dotnet pack`命令 (请参阅[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(请参阅[MSBuild 目标](../schema/msbuild-targets.md)) 可用作备用项。</span><span class="sxs-lookup"><span data-stu-id="c6d49-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="c6d49-108">下单声道，从项目文件创建包不支持。</span><span class="sxs-lookup"><span data-stu-id="c6d49-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="c6d49-109">你还需要调整中的非本地路径`.nuspec`文件于 Unix 样式的路径，如 nuget.exe 未转换 Windows 路径名本身。</span><span class="sxs-lookup"><span data-stu-id="c6d49-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="c6d49-110">用法</span><span class="sxs-lookup"><span data-stu-id="c6d49-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="c6d49-111">其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或项目文件中，分别。</span><span class="sxs-lookup"><span data-stu-id="c6d49-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c6d49-112">选项</span><span class="sxs-lookup"><span data-stu-id="c6d49-112">Options</span></span>

| <span data-ttu-id="c6d49-113">选项</span><span class="sxs-lookup"><span data-stu-id="c6d49-113">Option</span></span> | <span data-ttu-id="c6d49-114">描述</span><span class="sxs-lookup"><span data-stu-id="c6d49-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6d49-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="c6d49-115">BasePath</span></span> | <span data-ttu-id="c6d49-116">设置中定义的文件的基路径`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c6d49-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c6d49-117">生成</span><span class="sxs-lookup"><span data-stu-id="c6d49-117">Build</span></span> | <span data-ttu-id="c6d49-118">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="c6d49-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="c6d49-119">排除</span><span class="sxs-lookup"><span data-stu-id="c6d49-119">Exclude</span></span> | <span data-ttu-id="c6d49-120">指定一个或多个要在创建包时排除的通配符模式。</span><span class="sxs-lookup"><span data-stu-id="c6d49-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="c6d49-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="c6d49-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="c6d49-122">生成包时，可以防止包含空的目录。</span><span class="sxs-lookup"><span data-stu-id="c6d49-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="c6d49-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c6d49-123">ForceEnglishOutput</span></span> | <span data-ttu-id="c6d49-124">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="c6d49-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c6d49-125">帮助</span><span class="sxs-lookup"><span data-stu-id="c6d49-125">Help</span></span> | <span data-ttu-id="c6d49-126">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c6d49-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="c6d49-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="c6d49-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="c6d49-128">该值表示依赖关系或作为包的一部分，生成的包应包含引用的项目。</span><span class="sxs-lookup"><span data-stu-id="c6d49-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="c6d49-129">如果所引用的项目都有一个相应`.nuspec`具有与项目中，相同的名称，则该引用的项目添加为依赖项的文件。</span><span class="sxs-lookup"><span data-stu-id="c6d49-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="c6d49-130">否则，引用的项目将添加作为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="c6d49-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="c6d49-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c6d49-131">MinClientVersion</span></span> | <span data-ttu-id="c6d49-132">设置*minClientVersion*创建的包的属性。</span><span class="sxs-lookup"><span data-stu-id="c6d49-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="c6d49-133">此值将重写现有值*minClientVersion*属性 （如果有） 中`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c6d49-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c6d49-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c6d49-134">MSBuildPath</span></span> | <span data-ttu-id="c6d49-135">*（4.0 +)*指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c6d49-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c6d49-136">MSBuildVersion</span></span> | <span data-ttu-id="c6d49-137">*（3.2 +)*指定要用于此命令的 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="c6d49-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c6d49-138">支持的值为 4、 12、 14、 15。</span><span class="sxs-lookup"><span data-stu-id="c6d49-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c6d49-139">默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="c6d49-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c6d49-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="c6d49-140">NoDefaultExcludes</span></span> | <span data-ttu-id="c6d49-141">阻止的 NuGet 的默认排除包文件和文件和文件夹从一个点，如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="c6d49-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c6d49-142">NoPackageAnalysis</span></span> | <span data-ttu-id="c6d49-143">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="c6d49-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="c6d49-144">输出目录</span><span class="sxs-lookup"><span data-stu-id="c6d49-144">OutputDirectory</span></span> | <span data-ttu-id="c6d49-145">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c6d49-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="c6d49-146">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="c6d49-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="c6d49-147">属性</span><span class="sxs-lookup"><span data-stu-id="c6d49-147">Properties</span></span> | <span data-ttu-id="c6d49-148">指定的重写项目文件; 中的值的属性的列表请参阅[常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)属性名称。</span><span class="sxs-lookup"><span data-stu-id="c6d49-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="c6d49-149">此处的属性自变量是令牌的列表 = 值对，由分号分隔，其中的每个匹配项`$token$`中`.nuspec`文件将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="c6d49-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="c6d49-150">值可以是用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="c6d49-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="c6d49-151">请注意，对于"配置"属性中，默认值是"Debug"。</span><span class="sxs-lookup"><span data-stu-id="c6d49-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="c6d49-152">若要将更改为发布配置，使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="c6d49-153">后缀</span><span class="sxs-lookup"><span data-stu-id="c6d49-153">Suffix</span></span> | <span data-ttu-id="c6d49-154">*(3.4.4+)*将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。</span><span class="sxs-lookup"><span data-stu-id="c6d49-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="c6d49-155">例如，使用`-suffix nightly`将创建具有版本数字类似的包`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="c6d49-156">后缀必须以字母以避免警告、 错误和使用不同版本的 NuGet 和 NuGet 包管理器不兼容的潜在问题开头。</span><span class="sxs-lookup"><span data-stu-id="c6d49-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="c6d49-157">符号</span><span class="sxs-lookup"><span data-stu-id="c6d49-157">Symbols</span></span> | <span data-ttu-id="c6d49-158">指定包中包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="c6d49-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="c6d49-159">如果用于`.nuspec`文件，这将创建常规的 NuGet 包文件和相应符号包。</span><span class="sxs-lookup"><span data-stu-id="c6d49-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="c6d49-160">工具</span><span class="sxs-lookup"><span data-stu-id="c6d49-160">Tool</span></span> | <span data-ttu-id="c6d49-161">指定应将项目的输出文件放在`tool`文件夹。</span><span class="sxs-lookup"><span data-stu-id="c6d49-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="c6d49-162">详细级别</span><span class="sxs-lookup"><span data-stu-id="c6d49-162">Verbosity</span></span> | <span data-ttu-id="c6d49-163">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="c6d49-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="c6d49-164">版本</span><span class="sxs-lookup"><span data-stu-id="c6d49-164">Version</span></span> | <span data-ttu-id="c6d49-165">重写从版本号`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="c6d49-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="c6d49-166">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c6d49-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="c6d49-167">排除开发依赖项</span><span class="sxs-lookup"><span data-stu-id="c6d49-167">Excluding development dependencies</span></span>

<span data-ttu-id="c6d49-168">一些 NuGet 程序包都可用作开发依赖关系，可帮助你创作你自己的库，但不一定需要实际包依赖关系。</span><span class="sxs-lookup"><span data-stu-id="c6d49-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="c6d49-169">`pack`命令将忽略`package`中的条目`packages.config`具有`developmentDependency`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="c6d49-170">这些项将不包括作为中创建的包的依赖关系中。</span><span class="sxs-lookup"><span data-stu-id="c6d49-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="c6d49-171">例如，考虑以下`packages.config`源项目文件中：</span><span class="sxs-lookup"><span data-stu-id="c6d49-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="c6d49-172">对于此项目，包创建的`nuget pack`将具有依赖关系`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="c6d49-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="c6d49-173">示例</span><span class="sxs-lookup"><span data-stu-id="c6d49-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
