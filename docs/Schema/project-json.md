---
title: "适用于 NuGet 的 project.json 文件引用 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d64fa6d8-a3f7-4c72-95d3-1a964375ccb8
description: "在某些项目类型中，project.json 维护项目中使用的 NuGet 包列表。"
keywords: "NuGet project.json, NuGet 包引用, NuGet 依赖项, project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e8763c22bda0c384b8bb1a00078a314e4bedc262
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-reference"></a><span data-ttu-id="fca93-104">project.json 引用</span><span class="sxs-lookup"><span data-stu-id="fca93-104">project.json reference</span></span>

<span data-ttu-id="fca93-105">NuGet 3.x+</span><span class="sxs-lookup"><span data-stu-id="fca93-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="fca93-106">`project.json` 文件维护项目中使用的包列表，称为包引用格式。</span><span class="sxs-lookup"><span data-stu-id="fca93-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="fca93-107">它会取代 `packages.config`，但在 NuGet 4.0+ 中又被 [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) 取代。</span><span class="sxs-lookup"><span data-stu-id="fca93-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="fca93-108">[`project.lock.json`](#projectlockjson) 文件（如下所述）也用于采用 `project.json` 的项目。</span><span class="sxs-lookup"><span data-stu-id="fca93-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="fca93-109">`project.json` 具有以下基本结构，其中四个顶层对象均可拥有任意数量的子对象：</span><span class="sxs-lookup"><span data-stu-id="fca93-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }  
}
```
 
## <a name="dependencies"></a><span data-ttu-id="fca93-110">依赖项</span><span class="sxs-lookup"><span data-stu-id="fca93-110">Dependencies</span></span>

<span data-ttu-id="fca93-111">以下面的形式列出项目的 NuGet 包依赖项：</span><span class="sxs-lookup"><span data-stu-id="fca93-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```
  
<span data-ttu-id="fca93-112">例如: </span><span class="sxs-lookup"><span data-stu-id="fca93-112">For example:</span></span>

```json
"dependencies": {   
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"   
}
```

<span data-ttu-id="fca93-113">`dependencies` 部分是“NuGet 包管理器”对话框向项目中添加包依赖项的位置。</span><span class="sxs-lookup"><span data-stu-id="fca93-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="fca93-114">包 ID 对应于 nuget.org 上包的 ID，与包管理器控制台中使用的 ID 相同：`Install-Package Microsoft.NETCore`。</span><span class="sxs-lookup"><span data-stu-id="fca93-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="fca93-115">还原包时，`"5.0.0"` 版本约束意味着 `>= 5.0.0`。</span><span class="sxs-lookup"><span data-stu-id="fca93-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="fca93-116">也就是说，如果 5.0.0 在服务器上不可用，但 5.0.1 可用，则 NuGet 安装 5.0.1，并发出有关升级的警告。</span><span class="sxs-lookup"><span data-stu-id="fca93-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="fca93-117">否则，NuGet 尽可能在服务器上选取最低的版本，以与约束匹配。</span><span class="sxs-lookup"><span data-stu-id="fca93-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="fca93-118">请参阅[依赖项解析](../consume-packages/dependency-resolution.md)深入了解解析规则。</span><span class="sxs-lookup"><span data-stu-id="fca93-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="fca93-119">管理依赖项资产</span><span class="sxs-lookup"><span data-stu-id="fca93-119">Managing dependency assets</span></span>

<span data-ttu-id="fca93-120">依赖项的哪些资产流入顶级项目是通过在依赖项引用的 `include` 和 `exclude` 属性中指定一组以逗号分隔的标记来控制的。</span><span class="sxs-lookup"><span data-stu-id="fca93-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="fca93-121">下表中列出了这些标记：</span><span class="sxs-lookup"><span data-stu-id="fca93-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="fca93-122">包括/排除标记</span><span class="sxs-lookup"><span data-stu-id="fca93-122">Include/Exclude tag</span></span> | <span data-ttu-id="fca93-123">受影响的目标文件夹</span><span class="sxs-lookup"><span data-stu-id="fca93-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="fca93-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fca93-124">contentFiles</span></span> | <span data-ttu-id="fca93-125">内容</span><span class="sxs-lookup"><span data-stu-id="fca93-125">Content</span></span>  |
| <span data-ttu-id="fca93-126">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="fca93-126">runtime</span></span> | <span data-ttu-id="fca93-127">运行时、资源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="fca93-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="fca93-128">编译</span><span class="sxs-lookup"><span data-stu-id="fca93-128">compile</span></span> | <span data-ttu-id="fca93-129">lib</span><span class="sxs-lookup"><span data-stu-id="fca93-129">lib</span></span> |
| <span data-ttu-id="fca93-130">生成</span><span class="sxs-lookup"><span data-stu-id="fca93-130">build</span></span> | <span data-ttu-id="fca93-131">生成（MSBuild 属性和目标）</span><span class="sxs-lookup"><span data-stu-id="fca93-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="fca93-132">本机</span><span class="sxs-lookup"><span data-stu-id="fca93-132">native</span></span> | <span data-ttu-id="fca93-133">本机</span><span class="sxs-lookup"><span data-stu-id="fca93-133">native</span></span> |
| <span data-ttu-id="fca93-134">无</span><span class="sxs-lookup"><span data-stu-id="fca93-134">none</span></span> | <span data-ttu-id="fca93-135">无文件夹</span><span class="sxs-lookup"><span data-stu-id="fca93-135">No folders</span></span> |
| <span data-ttu-id="fca93-136">全部</span><span class="sxs-lookup"><span data-stu-id="fca93-136">all</span></span> | <span data-ttu-id="fca93-137">全部文件夹</span><span class="sxs-lookup"><span data-stu-id="fca93-137">All folders</span></span> |

<span data-ttu-id="fca93-138">用 `exclude` 指定的标记优先于用 `include` 指定的标记。</span><span class="sxs-lookup"><span data-stu-id="fca93-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="fca93-139">例如，`include="runtime, compile" exclude="compile"` 和 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="fca93-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="fca93-140">例如，若要包括依赖项的 `build` 和 `native` 文件夹，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="fca93-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="fca93-141">若要排除依赖项的 `content` 和 `build` 文件夹，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="fca93-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="fca93-142">框架</span><span class="sxs-lookup"><span data-stu-id="fca93-142">Frameworks</span></span>

<span data-ttu-id="fca93-143">列出项目运行的框架，如 `net45`、`netcoreapp`、`netstandard`。</span><span class="sxs-lookup"><span data-stu-id="fca93-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="fca93-144">`frameworks` 部分仅允许一个条目。</span><span class="sxs-lookup"><span data-stu-id="fca93-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="fca93-145">（例外情况是用于 ASP.NET 项目的 `project.json` 文件，它们通过弃用的 DNX 工具链生成，可允许多个目标。）</span><span class="sxs-lookup"><span data-stu-id="fca93-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="fca93-146">运行时</span><span class="sxs-lookup"><span data-stu-id="fca93-146">Runtimes</span></span>

<span data-ttu-id="fca93-147">列出应用运行的操作系统和体系结构，如 `win10-arm`、`win8-x64`、`win8-x86`。</span><span class="sxs-lookup"><span data-stu-id="fca93-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="fca93-148">可在任何运行时上运行的包含 PCL 的包不需要指定运行时。</span><span class="sxs-lookup"><span data-stu-id="fca93-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="fca93-149">这还必须对任何依赖项适用，否则必须指定运行时。</span><span class="sxs-lookup"><span data-stu-id="fca93-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="fca93-150">支持</span><span class="sxs-lookup"><span data-stu-id="fca93-150">Supports</span></span>

<span data-ttu-id="fca93-151">为包依赖项定义一组检查。</span><span class="sxs-lookup"><span data-stu-id="fca93-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="fca93-152">可以定义期望 PCL 或应用运行的位置。</span><span class="sxs-lookup"><span data-stu-id="fca93-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="fca93-153">定义限制并不严格，因为代码可在其他位置运行。</span><span class="sxs-lookup"><span data-stu-id="fca93-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="fca93-154">但指定这些检查会让 NuGet 检查所有依赖项在所列 TxM 上是否满足。</span><span class="sxs-lookup"><span data-stu-id="fca93-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="fca93-155">此支持的值的示例有：`net46.app`、`uwp.10.0.app` 等。</span><span class="sxs-lookup"><span data-stu-id="fca93-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="fca93-156">在“可移植类库目标”对话框中选择条目时，此部分应自动填充。</span><span class="sxs-lookup"><span data-stu-id="fca93-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="fca93-157">导入</span><span class="sxs-lookup"><span data-stu-id="fca93-157">Imports</span></span>

<span data-ttu-id="fca93-158">导入旨在允许使用 `dotnet` TxM 的包处理未声明 dotnet TxM 的包。</span><span class="sxs-lookup"><span data-stu-id="fca93-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="fca93-159">如果项目使用的是 `dotnet` TxM，那么依赖的所有包也必须有 `dotnet` TxM，除非将以下内容添加到 `project.json` 中，以允许非 `dotnet` 平台与 `dotnet` 兼容：</span><span class="sxs-lookup"><span data-stu-id="fca93-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="fca93-160">如果使用的是 `dotnet` TxM，那么 PCL 项目系统会基于支持的目标添加相应的 `imports` 语句。</span><span class="sxs-lookup"><span data-stu-id="fca93-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="fca93-161">可移植应用和 Web 项目的区别</span><span class="sxs-lookup"><span data-stu-id="fca93-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="fca93-162">NuGet 使用的 `project.json` 文件是 ASP.NET Core 项目中该文件的子集。</span><span class="sxs-lookup"><span data-stu-id="fca93-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="fca93-163">在 ASP.NET Core 中，`project.json` 用于项目元数据、编译信息和依赖项。</span><span class="sxs-lookup"><span data-stu-id="fca93-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="fca93-164">在其他项目系统中使用时，这三项内容则拆分为单独的文件，并且 `project.json` 包含的信息更少。</span><span class="sxs-lookup"><span data-stu-id="fca93-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="fca93-165">明显的区别包括：</span><span class="sxs-lookup"><span data-stu-id="fca93-165">Notable differences include:</span></span>

- <span data-ttu-id="fca93-166">`frameworks` 部分仅可有一个框架。</span><span class="sxs-lookup"><span data-stu-id="fca93-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="fca93-167">该文件不能包含 DNX `project.json` 文件中可看到的依赖项、编译选项等。</span><span class="sxs-lookup"><span data-stu-id="fca93-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="fca93-168">鉴于只能有一个框架，输入框架特定的依赖项毫无意义。</span><span class="sxs-lookup"><span data-stu-id="fca93-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="fca93-169">编译由 MSBuild 处理，因此编译选项、预处理器定义等都属于 MSBuild 项目文件而不是 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="fca93-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="fca93-170">在 NuGet 3+ 中，不需要开发人员手动编辑 `project.json`，因为 Visual Studio 中的包管理器 UI 会操作内容。</span><span class="sxs-lookup"><span data-stu-id="fca93-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="fca93-171">即便如此，当然还是可以编辑文件，但必须生成项目以启动包还原或以其他方式调用还原。</span><span class="sxs-lookup"><span data-stu-id="fca93-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="fca93-172">请参阅[包还原](../Consume-Packages/Package-Restore.md)。</span><span class="sxs-lookup"><span data-stu-id="fca93-172">See [Package restore](../Consume-Packages/Package-Restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="fca93-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="fca93-173">project.lock.json</span></span>

<span data-ttu-id="fca93-174">在还原使用 `project.json` 的项目中的 NuGet 包的过程中，会生成 `project.lock.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="fca93-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="fca93-175">它拥有 NuGet 在走包的关系图时生成的所有信息的快照，并包括项目中所有包的版本、内容和依赖项。</span><span class="sxs-lookup"><span data-stu-id="fca93-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="fca93-176">生成项目时，生成系统根据此快照从相关的全局位置选择包，而不是依靠项目本身中的本地包文件夹。</span><span class="sxs-lookup"><span data-stu-id="fca93-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="fca93-177">这使得生成性能更快，因为仅需读取 `project.lock.json` 而不是许多单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="fca93-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="fca93-178">`project.lock.json` 在包还原时自动生成，因此可通过将其添加到 `.gitignore` 和 `.tfignore` 文件，将其从源代码管理去掉（请参阅[包和源代码管理](../Consume-Packages/Packages-and-Source-Control.md)）。</span><span class="sxs-lookup"><span data-stu-id="fca93-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../Consume-Packages/Packages-and-Source-Control.md).</span></span> <span data-ttu-id="fca93-179">但是，如果将其包括在源代码管理中，更改历史记录会显示随着时间推移解析的依赖项的更改。</span><span class="sxs-lookup"><span data-stu-id="fca93-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
