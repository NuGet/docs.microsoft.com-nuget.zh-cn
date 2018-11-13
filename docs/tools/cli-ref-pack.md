---
title: NuGet CLI pack 命令
description: Nuget.exe pack 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 826316bdbce881836836f2a667cfa5297996d14f
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580306"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="544be-103">pack 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="544be-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="544be-104">**适用于：** 创建包&bullet;**支持的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="544be-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="544be-105">创建基于指定的 NuGet 包`.nuspec`或项目文件。</span><span class="sxs-lookup"><span data-stu-id="544be-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="544be-106">`dotnet pack`命令 (请参阅[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(请参阅[MSBuild 目标](../reference/msbuild-targets.md)) 可以用作备用项。</span><span class="sxs-lookup"><span data-stu-id="544be-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="544be-107">在 Mono 下从项目文件创建包不支持。</span><span class="sxs-lookup"><span data-stu-id="544be-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="544be-108">您还需要调整中的非本地路径`.nuspec`nuget.exe 不会将自身的 Windows 路径名转换为 Unix 样式的路径，到文件。</span><span class="sxs-lookup"><span data-stu-id="544be-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="544be-109">用法</span><span class="sxs-lookup"><span data-stu-id="544be-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="544be-110">其中`<nuspecPath>`并`<projectPath>`指定`.nuspec`或项目文件，分别。</span><span class="sxs-lookup"><span data-stu-id="544be-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="544be-111">选项</span><span class="sxs-lookup"><span data-stu-id="544be-111">Options</span></span>

| <span data-ttu-id="544be-112">选项</span><span class="sxs-lookup"><span data-stu-id="544be-112">Option</span></span> | <span data-ttu-id="544be-113">描述</span><span class="sxs-lookup"><span data-stu-id="544be-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="544be-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="544be-114">BasePath</span></span> | <span data-ttu-id="544be-115">设置中定义的文件的基路径`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="544be-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="544be-116">生成</span><span class="sxs-lookup"><span data-stu-id="544be-116">Build</span></span> | <span data-ttu-id="544be-117">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="544be-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="544be-118">排除</span><span class="sxs-lookup"><span data-stu-id="544be-118">Exclude</span></span> | <span data-ttu-id="544be-119">指定创建包时要排除的一个或多个通配符模式。</span><span class="sxs-lookup"><span data-stu-id="544be-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="544be-120">若要指定多个模式，请重复-排除标志。</span><span class="sxs-lookup"><span data-stu-id="544be-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="544be-121">请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="544be-121">See example below.</span></span> |
| <span data-ttu-id="544be-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="544be-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="544be-123">生成包时，会阻止包含空的目录。</span><span class="sxs-lookup"><span data-stu-id="544be-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="544be-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="544be-124">ForceEnglishOutput</span></span> | <span data-ttu-id="544be-125">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="544be-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="544be-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="544be-126">ConfigFile</span></span> | <span data-ttu-id="544be-127">指定 pack 命令的配置文件。</span><span class="sxs-lookup"><span data-stu-id="544be-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="544be-128">帮助</span><span class="sxs-lookup"><span data-stu-id="544be-128">Help</span></span> | <span data-ttu-id="544be-129">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="544be-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="544be-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="544be-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="544be-131">指示生成的包应包括引用的项目作为依赖项或作为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="544be-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="544be-132">如果引用的项目有一个相应`.nuspec`具有相同名称，为项目，则该引用的项目添加为依赖项的文件。</span><span class="sxs-lookup"><span data-stu-id="544be-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="544be-133">否则，引用的项目添加为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="544be-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="544be-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="544be-134">MinClientVersion</span></span> | <span data-ttu-id="544be-135">设置*minClientVersion*创建的包的属性。</span><span class="sxs-lookup"><span data-stu-id="544be-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="544be-136">此值将覆盖现有值*minClientVersion*中的属性 （如果有）`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="544be-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="544be-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="544be-137">MSBuildPath</span></span> | <span data-ttu-id="544be-138">*（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="544be-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="544be-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="544be-139">MSBuildVersion</span></span> | <span data-ttu-id="544be-140">*（3.2 +)* 指定要用于此命令的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="544be-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="544be-141">支持的值为 4、 12、 14、 15。</span><span class="sxs-lookup"><span data-stu-id="544be-141">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="544be-142">默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="544be-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="544be-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="544be-143">NoDefaultExcludes</span></span> | <span data-ttu-id="544be-144">可防止默认排除的 NuGet 包文件和文件和文件夹启动带有圆点，如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="544be-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="544be-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="544be-145">NoPackageAnalysis</span></span> | <span data-ttu-id="544be-146">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="544be-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="544be-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="544be-147">OutputDirectory</span></span> | <span data-ttu-id="544be-148">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="544be-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="544be-149">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="544be-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="544be-150">属性</span><span class="sxs-lookup"><span data-stu-id="544be-150">Properties</span></span> | <span data-ttu-id="544be-151">其他选项后应显示最后一个命令行上。</span><span class="sxs-lookup"><span data-stu-id="544be-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="544be-152">指定重写项目文件中; 中的值的属性的列表请参阅[常用的 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)属性名称。</span><span class="sxs-lookup"><span data-stu-id="544be-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="544be-153">此处的属性参数是一系列令牌 = 值对，用分号分隔，其中的每个匹配项`$token$`中`.nuspec`文件将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="544be-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="544be-154">值可以为在引号内的字符串。</span><span class="sxs-lookup"><span data-stu-id="544be-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="544be-155">请注意，对于"配置"属性中，默认值"Debug"。</span><span class="sxs-lookup"><span data-stu-id="544be-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="544be-156">若要将更改为发布配置，请使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="544be-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="544be-157">后缀</span><span class="sxs-lookup"><span data-stu-id="544be-157">Suffix</span></span> | <span data-ttu-id="544be-158">*(3.4.4+)* 将后缀追加到在内部生成的版本号，通常用于追加生成或其他预发布版本标识符。</span><span class="sxs-lookup"><span data-stu-id="544be-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="544be-159">例如，使用`-suffix nightly`将使用版本编号类似于创建包`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="544be-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="544be-160">后缀必须以字母以避免警告、 错误和使用不同版本的 NuGet 和 NuGet 包管理器可能不兼容问题开头。</span><span class="sxs-lookup"><span data-stu-id="544be-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="544be-161">符号</span><span class="sxs-lookup"><span data-stu-id="544be-161">Symbols</span></span> | <span data-ttu-id="544be-162">指定包包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="544be-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="544be-163">与一起使用时`.nuspec`文件，这将创建常规 NuGet 包文件和对应的符号包。</span><span class="sxs-lookup"><span data-stu-id="544be-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="544be-164">默认情况下它会创建[旧符号包](../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="544be-164">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="544be-165">符号包的新建议的格式是.snupkg。</span><span class="sxs-lookup"><span data-stu-id="544be-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="544be-166">请参阅[创建符号包 (.snupkg)](../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="544be-166">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="544be-167">工具</span><span class="sxs-lookup"><span data-stu-id="544be-167">Tool</span></span> | <span data-ttu-id="544be-168">指定应将该项目的输出文件放在`tool`文件夹。</span><span class="sxs-lookup"><span data-stu-id="544be-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="544be-169">详细级别</span><span class="sxs-lookup"><span data-stu-id="544be-169">Verbosity</span></span> | <span data-ttu-id="544be-170">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="544be-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="544be-171">版本</span><span class="sxs-lookup"><span data-stu-id="544be-171">Version</span></span> | <span data-ttu-id="544be-172">重写从版本号`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="544be-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="544be-173">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="544be-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="544be-174">不包括开发依赖项</span><span class="sxs-lookup"><span data-stu-id="544be-174">Excluding development dependencies</span></span>

<span data-ttu-id="544be-175">一些 NuGet 包可为开发依赖项，帮助你创作你自己的库，但不一定需要为实际的包依赖项。</span><span class="sxs-lookup"><span data-stu-id="544be-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="544be-176">`pack`命令将忽略`package`中的条目`packages.config`具有`developmentDependency`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="544be-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="544be-177">将作为依赖项中创建的包中包括这些项。</span><span class="sxs-lookup"><span data-stu-id="544be-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="544be-178">例如，请考虑以下`packages.config`源项目文件中：</span><span class="sxs-lookup"><span data-stu-id="544be-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="544be-179">对于此项目，包创建的`nuget pack`将具有依赖关系`jQuery`并`microsoft-web-helpers`但不是`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="544be-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="544be-180">示例</span><span class="sxs-lookup"><span data-stu-id="544be-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
