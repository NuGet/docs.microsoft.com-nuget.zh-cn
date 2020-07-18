---
title: NuGet CLI 包命令
description: nuget.exe pack 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 649c440d868c89068a069a396919b58b999369e5
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451133"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="f471d-103">pack 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="f471d-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="f471d-104">**适用于：** 创建包的 &bullet; **支持版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="f471d-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="f471d-105">基于指定的[nuspec](../nuspec.md)或项目文件创建 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f471d-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="f471d-106">`dotnet pack`命令（请参阅[dotnet 命令](../dotnet-Commands.md)）和 `msbuild -t:pack` （请参阅[MSBuild 目标](../msbuild-targets.md)）可以用作备用项。</span><span class="sxs-lookup"><span data-stu-id="f471d-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="f471d-107">[`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) 为基于[PackageReference](../../consume-packages/package-references-in-project-files.md)的项目使用或。</span><span class="sxs-lookup"><span data-stu-id="f471d-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="f471d-108">在 Mono 下，不支持从项目文件创建包。</span><span class="sxs-lookup"><span data-stu-id="f471d-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="f471d-109">还需要将文件中的非本地路径调整 `.nuspec` 为 Unix 样式路径，因为 nuget.exe 不会转换 Windows 路径名本身。</span><span class="sxs-lookup"><span data-stu-id="f471d-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="f471d-110">使用情况</span><span class="sxs-lookup"><span data-stu-id="f471d-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="f471d-111">， `<nuspecPath>` 并 `<projectPath>` 分别指定 `.nuspec` 或项目文件。</span><span class="sxs-lookup"><span data-stu-id="f471d-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="f471d-112">选项</span><span class="sxs-lookup"><span data-stu-id="f471d-112">Options</span></span>

| <span data-ttu-id="f471d-113">选项</span><span class="sxs-lookup"><span data-stu-id="f471d-113">Option</span></span> | <span data-ttu-id="f471d-114">说明</span><span class="sxs-lookup"><span data-stu-id="f471d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471d-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="f471d-115">BasePath</span></span> | <span data-ttu-id="f471d-116">设置在[nuspec](../nuspec.md)文件中定义的文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="f471d-116">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="f471d-117">生成</span><span class="sxs-lookup"><span data-stu-id="f471d-117">Build</span></span> | <span data-ttu-id="f471d-118">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="f471d-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="f471d-119">Exclude</span><span class="sxs-lookup"><span data-stu-id="f471d-119">Exclude</span></span> | <span data-ttu-id="f471d-120">指定创建包时要排除的一个或多个通配符模式。</span><span class="sxs-lookup"><span data-stu-id="f471d-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="f471d-121">若要指定多个模式，请重复-Exclude 标志。</span><span class="sxs-lookup"><span data-stu-id="f471d-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="f471d-122">请参阅以下示例。</span><span class="sxs-lookup"><span data-stu-id="f471d-122">See example below.</span></span> |
| <span data-ttu-id="f471d-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="f471d-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="f471d-124">在生成包时阻止包含空目录。</span><span class="sxs-lookup"><span data-stu-id="f471d-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="f471d-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f471d-125">ForceEnglishOutput</span></span> | <span data-ttu-id="f471d-126">*（3.5 +）* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f471d-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f471d-127">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f471d-127">ConfigFile</span></span> | <span data-ttu-id="f471d-128">指定 pack 命令的配置文件。</span><span class="sxs-lookup"><span data-stu-id="f471d-128">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="f471d-129">帮助</span><span class="sxs-lookup"><span data-stu-id="f471d-129">Help</span></span> | <span data-ttu-id="f471d-130">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="f471d-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="f471d-131">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="f471d-131">IncludeReferencedProjects</span></span> | <span data-ttu-id="f471d-132">指示生成的包应包含作为依赖项或包的一部分的引用项目。</span><span class="sxs-lookup"><span data-stu-id="f471d-132">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="f471d-133">如果引用的项目具有与 `.nuspec` 项目具有相同名称的相应文件，则会将引用的项目添加为依赖项。</span><span class="sxs-lookup"><span data-stu-id="f471d-133">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="f471d-134">否则，被引用项目作为包的一部分添加。</span><span class="sxs-lookup"><span data-stu-id="f471d-134">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="f471d-135">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f471d-135">MinClientVersion</span></span> | <span data-ttu-id="f471d-136">设置所创建的包的*minClientVersion*属性。</span><span class="sxs-lookup"><span data-stu-id="f471d-136">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="f471d-137">此值将覆盖文件中现有*minClientVersion*属性的值（如果有） `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-137">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="f471d-138">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="f471d-138">MSBuildPath</span></span> | <span data-ttu-id="f471d-139">*（4.0 +）* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-139">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="f471d-140">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="f471d-140">MSBuildVersion</span></span> | <span data-ttu-id="f471d-141">*（3.2 +）* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="f471d-141">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="f471d-142">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="f471d-142">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="f471d-143">默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="f471d-143">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="f471d-144">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="f471d-144">NoDefaultExcludes</span></span> | <span data-ttu-id="f471d-145">禁止默认排除 NuGet 包文件和以点（例如和）开头的文件和文件夹 `.svn` `.gitignore` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-145">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="f471d-146">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f471d-146">NoPackageAnalysis</span></span> | <span data-ttu-id="f471d-147">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="f471d-147">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="f471d-148">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f471d-148">OutputDirectory</span></span> | <span data-ttu-id="f471d-149">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="f471d-149">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="f471d-150">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="f471d-150">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f471d-151">属性</span><span class="sxs-lookup"><span data-stu-id="f471d-151">Properties</span></span> | <span data-ttu-id="f471d-152">应在其他选项后出现在命令行的最后。</span><span class="sxs-lookup"><span data-stu-id="f471d-152">Should appear last on the command line after other options.</span></span> <span data-ttu-id="f471d-153">指定重写项目文件中的值的属性的列表;请参阅属性名称的[常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)。</span><span class="sxs-lookup"><span data-stu-id="f471d-153">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="f471d-154">此处的 Properties 参数是标记 = 值对列表，用分号分隔，其中每个 `$token$` 在文件中出现的 `.nuspec` 都将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="f471d-154">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="f471d-155">值可以是用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="f471d-155">Values can be strings in quotation marks.</span></span> <span data-ttu-id="f471d-156">请注意，对于 "配置" 属性，默认值为 "调试"。</span><span class="sxs-lookup"><span data-stu-id="f471d-156">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="f471d-157">若要更改为发布配置，请使用 `-Properties Configuration=Release` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-157">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="f471d-158">**一般情况**下，属性应该与在相应的项目生成过程中使用的属性相同，以避免潜在的异常行为。</span><span class="sxs-lookup"><span data-stu-id="f471d-158">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span> |
| <span data-ttu-id="f471d-159">Suffix</span><span class="sxs-lookup"><span data-stu-id="f471d-159">Suffix</span></span> | <span data-ttu-id="f471d-160">*（3.4.4 +）* 将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。</span><span class="sxs-lookup"><span data-stu-id="f471d-160">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="f471d-161">例如，使用 `-suffix nightly` 将创建一个版本号与相同的包 `1.2.3-nightly` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-161">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="f471d-162">后缀必须以字母开头，以避免与不同版本的 NuGet 和 NuGet 包管理器的警告、错误和可能的不兼容性。</span><span class="sxs-lookup"><span data-stu-id="f471d-162">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="f471d-163">符号</span><span class="sxs-lookup"><span data-stu-id="f471d-163">Symbols</span></span> | <span data-ttu-id="f471d-164">指定包包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="f471d-164">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="f471d-165">与文件一起使用时 `.nuspec` ，将创建一个常规 NuGet 包文件和相应的符号包。</span><span class="sxs-lookup"><span data-stu-id="f471d-165">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="f471d-166">默认情况下，它会创建[旧的符号包](../../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="f471d-166">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="f471d-167">符号包的新推荐格式为 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="f471d-167">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="f471d-168">请参阅[创建符号包 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="f471d-168">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="f471d-169">工具</span><span class="sxs-lookup"><span data-stu-id="f471d-169">Tool</span></span> | <span data-ttu-id="f471d-170">指定应将项目的输出文件放在 `tool` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f471d-170">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="f471d-171">详细级别</span><span class="sxs-lookup"><span data-stu-id="f471d-171">Verbosity</span></span> | <span data-ttu-id="f471d-172">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="f471d-172">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f471d-173">版本</span><span class="sxs-lookup"><span data-stu-id="f471d-173">Version</span></span> | <span data-ttu-id="f471d-174">覆盖文件中的版本号 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-174">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="f471d-175">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f471d-175">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="f471d-176">排除开发依赖项</span><span class="sxs-lookup"><span data-stu-id="f471d-176">Excluding development dependencies</span></span>

<span data-ttu-id="f471d-177">某些 NuGet 包可用作开发依赖项，它们可帮助你创作自己的库，但不一定是实际的包依赖项。</span><span class="sxs-lookup"><span data-stu-id="f471d-177">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="f471d-178">`pack`命令将忽略 `package` 中 `packages.config` `developmentDependency` 属性设置为的项 `true` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-178">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="f471d-179">这些项不会作为依赖项包含在所创建的包中。</span><span class="sxs-lookup"><span data-stu-id="f471d-179">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="f471d-180">例如，请考虑 `packages.config` 源项目中的以下文件：</span><span class="sxs-lookup"><span data-stu-id="f471d-180">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="f471d-181">对于此项目，创建的包 `nuget pack` 将依赖于 `jQuery` 和， `microsoft-web-helpers` 而不是 `netfx-Guard` 。</span><span class="sxs-lookup"><span data-stu-id="f471d-181">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="f471d-182">抑制包警告</span><span class="sxs-lookup"><span data-stu-id="f471d-182">Suppressing pack warnings</span></span>

<span data-ttu-id="f471d-183">尽管建议你在包操作期间解决所有 NuGet 警告，但在某些情况下禁止它们是保证的。</span><span class="sxs-lookup"><span data-stu-id="f471d-183">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="f471d-184">可以通过以下方式实现此目的：</span><span class="sxs-lookup"><span data-stu-id="f471d-184">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="f471d-185">nuget.exe pack nuspec-Properties NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="f471d-185">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="f471d-186">示例</span><span class="sxs-lookup"><span data-stu-id="f471d-186">Examples</span></span>

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
