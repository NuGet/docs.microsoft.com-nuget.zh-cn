---
title: NuGet CLI 包命令
description: nuget.exe pack 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780046"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="4373e-103"> (NuGet CLI) 打包命令</span><span class="sxs-lookup"><span data-stu-id="4373e-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="4373e-104">**适用于：** 创建包的 &bullet; **支持版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="4373e-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="4373e-105">基于指定的 [nuspec](../nuspec.md) 或项目文件创建 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4373e-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="4373e-106">`dotnet pack`命令 (参阅[dotnet 命令](../dotnet-Commands.md)) 和 `msbuild -t:pack` (查看[MSBuild 目标](../msbuild-targets.md)) 可用作备用项。</span><span class="sxs-lookup"><span data-stu-id="4373e-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="4373e-107">[`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) 为基于[PackageReference](../../consume-packages/package-references-in-project-files.md)的项目使用或。</span><span class="sxs-lookup"><span data-stu-id="4373e-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="4373e-108">在 Mono 下，不支持从项目文件创建包。</span><span class="sxs-lookup"><span data-stu-id="4373e-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="4373e-109">还需要将文件中的非本地路径调整 `.nuspec` 为 Unix 样式路径，因为 nuget.exe 不会转换 Windows 路径名本身。</span><span class="sxs-lookup"><span data-stu-id="4373e-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="4373e-110">使用情况</span><span class="sxs-lookup"><span data-stu-id="4373e-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="4373e-111">， `<nuspecPath>` 并 `<projectPath>` 分别指定 `.nuspec` 或项目文件。</span><span class="sxs-lookup"><span data-stu-id="4373e-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="4373e-112">选项</span><span class="sxs-lookup"><span data-stu-id="4373e-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="4373e-113">设置在 [nuspec](../nuspec.md) 文件中定义的文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="4373e-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="4373e-114">指定应在生成包之前生成项目。</span><span class="sxs-lookup"><span data-stu-id="4373e-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="4373e-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4373e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4373e-116">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="4373e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="4373e-117">指定创建包时要排除的一个或多个通配符模式。</span><span class="sxs-lookup"><span data-stu-id="4373e-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="4373e-118">若要指定多个模式，请重复-Exclude 标志。</span><span class="sxs-lookup"><span data-stu-id="4373e-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="4373e-119">请参阅以下示例。</span><span class="sxs-lookup"><span data-stu-id="4373e-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="4373e-120">在生成包时阻止包含空目录。</span><span class="sxs-lookup"><span data-stu-id="4373e-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="4373e-121">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4373e-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="4373e-122">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="4373e-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="4373e-123">指示生成的包应包含作为依赖项或包的一部分的引用项目。</span><span class="sxs-lookup"><span data-stu-id="4373e-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="4373e-124">如果引用的项目具有与 `.nuspec` 项目具有相同名称的相应文件，则会将引用的项目添加为依赖项。</span><span class="sxs-lookup"><span data-stu-id="4373e-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="4373e-125">否则，被引用项目作为包的一部分添加。</span><span class="sxs-lookup"><span data-stu-id="4373e-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="4373e-126">指定该命令是否应准备包输出目录以支持共享作为源。</span><span class="sxs-lookup"><span data-stu-id="4373e-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="4373e-127">设置所创建的包的 *minClientVersion* 属性。</span><span class="sxs-lookup"><span data-stu-id="4373e-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="4373e-128">如果文件中有任何)  (，此值将覆盖现有的 *minClientVersion* 属性的值 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="4373e-129">*(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="4373e-130">*(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="4373e-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="4373e-131">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="4373e-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="4373e-132">默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="4373e-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="4373e-133">禁止默认排除 NuGet 包文件和以点（例如和）开头的文件和文件夹 `.svn` `.gitignore` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="4373e-134">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="4373e-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="4373e-135">指定 pack 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="4373e-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="4373e-136">指定在其中存储创建的包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4373e-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="4373e-137">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="4373e-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="4373e-138">指定该命令是否应在不包含版本的情况下准备包输出名称。</span><span class="sxs-lookup"><span data-stu-id="4373e-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="4373e-139">指定包文件夹。</span><span class="sxs-lookup"><span data-stu-id="4373e-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="4373e-140">应在其他选项后出现在命令行的最后。</span><span class="sxs-lookup"><span data-stu-id="4373e-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="4373e-141">指定重写项目文件中的值的属性的列表;请参阅属性名称的 [常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties) 。</span><span class="sxs-lookup"><span data-stu-id="4373e-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="4373e-142">此处的 Properties 参数是标记 = 值对列表，用分号分隔，其中每个 `$token$` 在文件中出现的 `.nuspec` 都将替换为给定的值。</span><span class="sxs-lookup"><span data-stu-id="4373e-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="4373e-143">值可以是用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="4373e-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="4373e-144">请注意，对于 "配置" 属性，默认值为 "调试"。</span><span class="sxs-lookup"><span data-stu-id="4373e-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="4373e-145">若要更改为发布配置，请使用 `-Properties Configuration=Release` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="4373e-146">**一般情况** 下，属性应该与在相应的项目生成过程中使用的属性相同，以避免潜在的异常行为。</span><span class="sxs-lookup"><span data-stu-id="4373e-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="4373e-147">指定解决方案目录。</span><span class="sxs-lookup"><span data-stu-id="4373e-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="4373e-148">*(3.4.4 +)* 将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。</span><span class="sxs-lookup"><span data-stu-id="4373e-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="4373e-149">例如，使用 `-suffix nightly` 将创建一个版本号与相同的包 `1.2.3-nightly` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="4373e-150">后缀必须以字母开头，以避免与不同版本的 NuGet 和 NuGet 包管理器的警告、错误和可能的不兼容性。</span><span class="sxs-lookup"><span data-stu-id="4373e-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="4373e-151">创建符号包时，允许在和格式之间进行 `snupkg` 选择 `symbols.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="4373e-152">指定包包含源和符号。</span><span class="sxs-lookup"><span data-stu-id="4373e-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="4373e-153">与文件一起使用时 `.nuspec` ，将创建一个常规 NuGet 包文件和相应的符号包。</span><span class="sxs-lookup"><span data-stu-id="4373e-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="4373e-154">默认情况下，它会创建 [旧的符号包](../../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="4373e-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="4373e-155">符号包的新推荐格式为 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="4373e-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="4373e-156">请参阅[创建符号包 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="4373e-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="4373e-157">指定应将项目的输出文件放在 `tool` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4373e-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="4373e-158">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="4373e-159">覆盖文件中的版本号 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="4373e-160">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4373e-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="4373e-161">排除开发依赖项</span><span class="sxs-lookup"><span data-stu-id="4373e-161">Excluding development dependencies</span></span>

<span data-ttu-id="4373e-162">某些 NuGet 包可用作开发依赖项，它们可帮助你创作自己的库，但不一定是实际的包依赖项。</span><span class="sxs-lookup"><span data-stu-id="4373e-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="4373e-163">`pack`命令将忽略 `package` 中 `packages.config` `developmentDependency` 属性设置为的项 `true` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="4373e-164">这些项不会作为依赖项包含在所创建的包中。</span><span class="sxs-lookup"><span data-stu-id="4373e-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="4373e-165">例如，请考虑 `packages.config` 源项目中的以下文件：</span><span class="sxs-lookup"><span data-stu-id="4373e-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="4373e-166">对于此项目，创建的包 `nuget pack` 将依赖于 `jQuery` 和， `microsoft-web-helpers` 而不是 `netfx-Guard` 。</span><span class="sxs-lookup"><span data-stu-id="4373e-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="4373e-167">抑制包警告</span><span class="sxs-lookup"><span data-stu-id="4373e-167">Suppressing pack warnings</span></span>

<span data-ttu-id="4373e-168">尽管建议你在包操作期间解决所有 NuGet 警告，但在某些情况下禁止它们是保证的。</span><span class="sxs-lookup"><span data-stu-id="4373e-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="4373e-169">可以通过以下方式实现此目的：</span><span class="sxs-lookup"><span data-stu-id="4373e-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="4373e-170">nuget.exe pack nuspec-Properties NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="4373e-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="4373e-171">示例</span><span class="sxs-lookup"><span data-stu-id="4373e-171">Examples</span></span>

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
