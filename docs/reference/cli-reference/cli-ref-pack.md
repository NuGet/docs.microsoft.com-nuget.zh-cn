---
title: NuGet CLI 包命令
description: 针对 nuget.exe 包命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 76829d45ea9821da3b7fdaa2f88d30dbb104fea1
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815360"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="27248-103">pack 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="27248-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="27248-104">**适用于：** 创建&bullet;包的**支持版本：** 2.7+</span><span class="sxs-lookup"><span data-stu-id="27248-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="27248-105">基于指定的[nuspec](../nuspec.md)或项目文件创建 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="27248-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="27248-106">命令（请参阅[dotnet 命令](../dotnet-Commands.md)）和`msbuild -t:pack` （请参阅[MSBuild 目标](../msbuild-targets.md)）可以用作备用项。 `dotnet pack`</span><span class="sxs-lookup"><span data-stu-id="27248-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="27248-107">在 Mono 下，不支持从项目文件创建包。</span><span class="sxs-lookup"><span data-stu-id="27248-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="27248-108">还需要将文件中的`.nuspec`非本地路径调整为 Unix 样式路径，因为 nuget.exe 不会转换 Windows 路径名本身。</span><span class="sxs-lookup"><span data-stu-id="27248-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="27248-109">用法</span><span class="sxs-lookup"><span data-stu-id="27248-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="27248-110">， `<nuspecPath>`并`<projectPath>`分别指定`.nuspec`或项目文件。</span><span class="sxs-lookup"><span data-stu-id="27248-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="27248-111">选项</span><span class="sxs-lookup"><span data-stu-id="27248-111">Options</span></span>

| <span data-ttu-id="27248-112">选项</span><span class="sxs-lookup"><span data-stu-id="27248-112">Option</span></span> | <span data-ttu-id="27248-113">描述</span><span class="sxs-lookup"><span data-stu-id="27248-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27248-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="27248-114">BasePath</span></span> | <span data-ttu-id="27248-115">设置在[nuspec](../nuspec.md)文件中定义的文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="27248-115">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="27248-116">Build</span><span class="sxs-lookup"><span data-stu-id="27248-116">Build</span></span> | <span data-ttu-id="27248-117">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="27248-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="27248-118">Deterministic</span><span class="sxs-lookup"><span data-stu-id="27248-118">Deterministic</span></span> | <span data-ttu-id="27248-119">指定该命令是否应创建确定性包。</span><span class="sxs-lookup"><span data-stu-id="27248-119">Specify if the command should create a deterministic package.</span></span> <span data-ttu-id="27248-120">多次调用 pack 命令将生成完全相同的字节到字节包。</span><span class="sxs-lookup"><span data-stu-id="27248-120">Multiple invocations of the pack command will generate the exact same byte-to-byte package.</span></span> <span data-ttu-id="27248-121">Pack 命令的输出不受计算机的环境状态影响。</span><span class="sxs-lookup"><span data-stu-id="27248-121">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="27248-122">特别是 zip 条目的时间戳为1980-01-01。</span><span class="sxs-lookup"><span data-stu-id="27248-122">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="27248-123">若要实现完全确定性，应通过相应的编译器选项（[确定性](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option)）生成程序集。</span><span class="sxs-lookup"><span data-stu-id="27248-123">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span> |
| <span data-ttu-id="27248-124">Exclude</span><span class="sxs-lookup"><span data-stu-id="27248-124">Exclude</span></span> | <span data-ttu-id="27248-125">指定创建包时要排除的一个或多个通配符模式。</span><span class="sxs-lookup"><span data-stu-id="27248-125">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="27248-126">若要指定多个模式，请重复-Exclude 标志。</span><span class="sxs-lookup"><span data-stu-id="27248-126">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="27248-127">请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="27248-127">See example below.</span></span> |
| <span data-ttu-id="27248-128">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="27248-128">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="27248-129">在生成包时阻止包含空目录。</span><span class="sxs-lookup"><span data-stu-id="27248-129">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="27248-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="27248-130">ForceEnglishOutput</span></span> | <span data-ttu-id="27248-131">*（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="27248-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="27248-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="27248-132">ConfigFile</span></span> | <span data-ttu-id="27248-133">指定 pack 命令的配置文件。</span><span class="sxs-lookup"><span data-stu-id="27248-133">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="27248-134">Help</span><span class="sxs-lookup"><span data-stu-id="27248-134">Help</span></span> | <span data-ttu-id="27248-135">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="27248-135">Displays help information for the command.</span></span> |
| <span data-ttu-id="27248-136">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="27248-136">IncludeReferencedProjects</span></span> | <span data-ttu-id="27248-137">指示生成的包应包含作为依赖项或包的一部分的引用项目。</span><span class="sxs-lookup"><span data-stu-id="27248-137">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="27248-138">如果引用的项目具有与项目`.nuspec`具有相同名称的相应文件，则会将引用的项目添加为依赖项。</span><span class="sxs-lookup"><span data-stu-id="27248-138">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="27248-139">否则，被引用项目作为包的一部分添加。</span><span class="sxs-lookup"><span data-stu-id="27248-139">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="27248-140">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="27248-140">MinClientVersion</span></span> | <span data-ttu-id="27248-141">设置所创建的包的*minClientVersion*属性。</span><span class="sxs-lookup"><span data-stu-id="27248-141">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="27248-142">此值将覆盖`.nuspec`文件中现有*minClientVersion*属性的值（如果有）。</span><span class="sxs-lookup"><span data-stu-id="27248-142">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="27248-143">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="27248-143">MSBuildPath</span></span> | <span data-ttu-id="27248-144">*（4.0 +）* 指定要与命令一起使用的 MSBuild 的路径，优先于`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="27248-144">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="27248-145">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="27248-145">MSBuildVersion</span></span> | <span data-ttu-id="27248-146">*（3.2 +）* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="27248-146">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="27248-147">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="27248-147">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="27248-148">默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="27248-148">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="27248-149">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="27248-149">NoDefaultExcludes</span></span> | <span data-ttu-id="27248-150">禁止默认排除 NuGet 包文件和以点（例如`.svn`和`.gitignore`）开头的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="27248-150">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="27248-151">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="27248-151">NoPackageAnalysis</span></span> | <span data-ttu-id="27248-152">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="27248-152">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="27248-153">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="27248-153">OutputDirectory</span></span> | <span data-ttu-id="27248-154">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="27248-154">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="27248-155">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="27248-155">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="27248-156">属性</span><span class="sxs-lookup"><span data-stu-id="27248-156">Properties</span></span> | <span data-ttu-id="27248-157">应在其他选项后出现在命令行的最后。</span><span class="sxs-lookup"><span data-stu-id="27248-157">Should appear last on the command line after other options.</span></span> <span data-ttu-id="27248-158">指定重写项目文件中的值的属性的列表;请参阅属性名称的[常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)。</span><span class="sxs-lookup"><span data-stu-id="27248-158">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="27248-159">此处的 Properties 参数是标记 = 值对列表，用分号分隔，其中每个`$token$` `.nuspec`在文件中出现的都将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="27248-159">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="27248-160">值可以是用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="27248-160">Values can be strings in quotation marks.</span></span> <span data-ttu-id="27248-161">请注意，对于 "配置" 属性，默认值为 "调试"。</span><span class="sxs-lookup"><span data-stu-id="27248-161">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="27248-162">若要更改为发布配置，请`-Properties Configuration=Release`使用。</span><span class="sxs-lookup"><span data-stu-id="27248-162">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="27248-163">Suffix</span><span class="sxs-lookup"><span data-stu-id="27248-163">Suffix</span></span> | <span data-ttu-id="27248-164">*（3.4.4 +）* 将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。</span><span class="sxs-lookup"><span data-stu-id="27248-164">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="27248-165">例如，使用`-suffix nightly`将创建一个版本号与相同`1.2.3-nightly`的包。</span><span class="sxs-lookup"><span data-stu-id="27248-165">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="27248-166">后缀必须以字母开头，以避免与不同版本的 NuGet 和 NuGet 包管理器的警告、错误和可能的不兼容性。</span><span class="sxs-lookup"><span data-stu-id="27248-166">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="27248-167">Symbols</span><span class="sxs-lookup"><span data-stu-id="27248-167">Symbols</span></span> | <span data-ttu-id="27248-168">指定包包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="27248-168">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="27248-169">与`.nuspec`文件一起使用时，将创建一个常规 NuGet 包文件和相应的符号包。</span><span class="sxs-lookup"><span data-stu-id="27248-169">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="27248-170">默认情况下，它会创建[旧的符号包](../../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="27248-170">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="27248-171">符号包的新推荐格式为 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="27248-171">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="27248-172">请参阅[创建符号包 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="27248-172">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="27248-173">Tool</span><span class="sxs-lookup"><span data-stu-id="27248-173">Tool</span></span> | <span data-ttu-id="27248-174">指定应将项目的输出文件放在`tool`文件夹中。</span><span class="sxs-lookup"><span data-stu-id="27248-174">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="27248-175">Verbosity</span><span class="sxs-lookup"><span data-stu-id="27248-175">Verbosity</span></span> | <span data-ttu-id="27248-176">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="27248-176">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="27248-177">Version</span><span class="sxs-lookup"><span data-stu-id="27248-177">Version</span></span> | <span data-ttu-id="27248-178">覆盖`.nuspec`文件中的版本号。</span><span class="sxs-lookup"><span data-stu-id="27248-178">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="27248-179">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="27248-179">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="27248-180">排除开发依赖项</span><span class="sxs-lookup"><span data-stu-id="27248-180">Excluding development dependencies</span></span>

<span data-ttu-id="27248-181">某些 NuGet 包可用作开发依赖项，它们可帮助你创作自己的库，但不一定是实际的包依赖项。</span><span class="sxs-lookup"><span data-stu-id="27248-181">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="27248-182">`package` `developmentDependency`命令将忽略中`packages.config`属性设置为`true`的项。 `pack`</span><span class="sxs-lookup"><span data-stu-id="27248-182">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="27248-183">这些项不会作为依赖项包含在所创建的包中。</span><span class="sxs-lookup"><span data-stu-id="27248-183">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="27248-184">例如，请考虑源项目`packages.config`中的以下文件：</span><span class="sxs-lookup"><span data-stu-id="27248-184">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="27248-185">对于此`nuget pack`项目，创建的包将依赖于`jQuery`和， `microsoft-web-helpers`而不`netfx-Guard`是。</span><span class="sxs-lookup"><span data-stu-id="27248-185">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="27248-186">示例</span><span class="sxs-lookup"><span data-stu-id="27248-186">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
