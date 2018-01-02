---
title: "使用 Visual Studio 2015 创建 .NET Standard NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "从头到尾介绍如何使用 NuGet 3.x 和 Visual Studio 2015 创建 .NET Standard NuGet 包。"
keywords: "创建包, .NET Standard 包, .NET Standard 映射表"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="c059a-104">使用 Visual Studio 2015 创建 .NET Standard 包</span><span class="sxs-lookup"><span data-stu-id="c059a-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="c059a-105">适用于 NuGet 3.x。有关使用 NuGet 4.x+ 的详细信息，请参阅[使用 Visual Studio 2017 创建 .NET Standard 包](../guides/create-net-standard-packages-vs2017.md)。</span><span class="sxs-lookup"><span data-stu-id="c059a-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="c059a-106">[.NET Standard 库](https://docs.microsoft.com/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。</span><span class="sxs-lookup"><span data-stu-id="c059a-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="c059a-107">.NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。</span><span class="sxs-lookup"><span data-stu-id="c059a-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="c059a-108">它使得开发人员可以生成跨所有 .NET 运行时可用的 PCL，并减少（如果不能消除）共享代码中平台特定的条件编译指令。</span><span class="sxs-lookup"><span data-stu-id="c059a-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="c059a-109">本指南将指导你创建一个面向 .NET Standard 库 1.4 的 nuget 包。</span><span class="sxs-lookup"><span data-stu-id="c059a-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="c059a-110">将在 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 上可用。</span><span class="sxs-lookup"><span data-stu-id="c059a-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="c059a-111">有关详细信息，请参阅本主题后面的 [.NET Standard 映射表](#net-standard-mapping-table)。</span><span class="sxs-lookup"><span data-stu-id="c059a-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="c059a-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="c059a-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="c059a-113">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="c059a-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="c059a-114">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="c059a-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="c059a-115">打包组件</span><span class="sxs-lookup"><span data-stu-id="c059a-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="c059a-116">附加选项</span><span class="sxs-lookup"><span data-stu-id="c059a-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="c059a-117">.NET Standard 映射表</span><span class="sxs-lookup"><span data-stu-id="c059a-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="c059a-118">相关主题</span><span class="sxs-lookup"><span data-stu-id="c059a-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="c059a-119">先决条件</span><span class="sxs-lookup"><span data-stu-id="c059a-119">Pre-requisites</span></span>

1. <span data-ttu-id="c059a-120">Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="c059a-120">Visual Studio 2015.</span></span> <span data-ttu-id="c059a-121">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版；当然，也可以使用 Professional 和 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="c059a-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="c059a-122">.NET Core：从 [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) 安装 .NET Core 以及适用于 Visual Studio 2015 的模板和其他工具。</span><span class="sxs-lookup"><span data-stu-id="c059a-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="c059a-123">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="c059a-123">NuGet CLI.</span></span> <span data-ttu-id="c059a-124">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。</span><span class="sxs-lookup"><span data-stu-id="c059a-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="c059a-125">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="c059a-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="c059a-126">nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。</span><span class="sxs-lookup"><span data-stu-id="c059a-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="c059a-127">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="c059a-127">Create the class library project</span></span>

1. <span data-ttu-id="c059a-128">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C#”>“Windows”节点，选择“类库(可移植)”，将名称更改为“AppLogger”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="c059a-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![创建新类库项目](media/NetStandard-NewProject.png)

1. <span data-ttu-id="c059a-130">在“添加可移植类库”对话框中，选择 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 选项。</span><span class="sxs-lookup"><span data-stu-id="c059a-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="c059a-131">右键单击解决方案资源管理器中的 `AppLogger (Portable)`，选择“属性”，选择“库”选项卡，然后单击“目标”部分中的“目标 .NET 平台标准”。</span><span class="sxs-lookup"><span data-stu-id="c059a-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="c059a-132">这将提示进行确认，之后可从下拉列表中选择 `.NET Standard 1.4`：</span><span class="sxs-lookup"><span data-stu-id="c059a-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![将目标设置为 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="c059a-134">单击“生成”选项卡，将“配置”更改为 `Release`，然后选中“XML 文档文件”框。</span><span class="sxs-lookup"><span data-stu-id="c059a-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="c059a-135">将代码添加到组件，例如：</span><span class="sxs-lookup"><span data-stu-id="c059a-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="c059a-136">生成项目（使用 Release 配置）并检查 bin\Release 文件夹中是否生成了 DLL 和 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="c059a-137">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="c059a-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="c059a-138">打开命令提示符，导航到包含 `AppLogg.csproj` 文件夹的文件夹（`.sln` 文件的下一级），然后运行 NuGet `spec` 命令，创建初始 `AppLogger.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="c059a-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="c059a-139">在编辑器中打开 `AppLogger.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="c059a-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="c059a-140">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="c059a-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="c059a-141">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="c059a-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="c059a-142">将引用程序集添加到 `.nuspec` 文件，也就是库的 DLL 和 IntelliSense XML 文件：</span><span class="sxs-lookup"><span data-stu-id="c059a-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="c059a-143">右键单击解决方案，选择“生成解决方案”，生成包的所有文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="c059a-144">打包组件</span><span class="sxs-lookup"><span data-stu-id="c059a-144">Package the component</span></span>

<span data-ttu-id="c059a-145">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="c059a-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="c059a-146">将生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="c059a-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="c059a-147">在 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)（NuGet 包资源管理器）之类的工具中打开此文件，并展开所有节点，随即将看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="c059a-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![显示 AppLogger 包的 NuGet 包资源管理器](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="c059a-149">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="c059a-150">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="c059a-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="c059a-151">若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="c059a-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="c059a-152">请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。</span><span class="sxs-lookup"><span data-stu-id="c059a-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="c059a-153">在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。</span><span class="sxs-lookup"><span data-stu-id="c059a-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="c059a-154">附加选项</span><span class="sxs-lookup"><span data-stu-id="c059a-154">Additional options</span></span>

<span data-ttu-id="c059a-155">以下部分介绍 NuGet 包创建的附加选项：</span><span class="sxs-lookup"><span data-stu-id="c059a-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="c059a-156">声明依赖项</span><span class="sxs-lookup"><span data-stu-id="c059a-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="c059a-157">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="c059a-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="c059a-158">添加 MSBuild 的目标和属性</span><span class="sxs-lookup"><span data-stu-id="c059a-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="c059a-159">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="c059a-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="c059a-160">添加自述文件</span><span class="sxs-lookup"><span data-stu-id="c059a-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="c059a-161">声明依赖项</span><span class="sxs-lookup"><span data-stu-id="c059a-161">Declaring dependencies</span></span>

<span data-ttu-id="c059a-162">如果具有其他 NuGet 包的任何依赖项，请使用 `<group>` 元素在 `<dependencies>` 元素中列出这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="c059a-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="c059a-163">例如，若要在 NewtonSoft.Json 8.0.3 或更高版本上声明依赖项，请添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="c059a-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="c059a-164">此处 version 特性的语法指示可接受版本 8.0.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="c059a-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="c059a-165">若要指定不同的版本范围，请参阅[包版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="c059a-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="c059a-166">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="c059a-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="c059a-167">假设想要利用 .NET Framework 4.6.2 中 .NET Standard 1.4 不可用的 API。</span><span class="sxs-lookup"><span data-stu-id="c059a-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="c059a-168">若要执行此操作，首先需要使用条件编译或共享项目确保 .NET 4.6.2 的库编译。</span><span class="sxs-lookup"><span data-stu-id="c059a-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="c059a-169">（在 Visual Studio 中，可创建一个 NetCore 项目，将选择的框架添加到多个框架部分，然后生成。）然后使用基于约定的简单工作目录技术创建包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c059a-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="c059a-170">在包含 `.nuspec` 文件的项目根文件夹中，创建一个名为 `lib` 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c059a-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="c059a-171">在 `lib` 中，为想要支持的每个平台创建文件夹：</span><span class="sxs-lookup"><span data-stu-id="c059a-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="c059a-172">在 `.nuspec` 文件中，在 `package` 节点下添加一个 `files` 节点，并使用通配符引用 `lib` 中的文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="c059a-173">注意：基于约定的工作目录方法不支持令牌替换，因此请将其替换为文本值：</span><span class="sxs-lookup"><span data-stu-id="c059a-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="c059a-174">使用 `nuget pack AppLogger.spec` 再次创建包。</span><span class="sxs-lookup"><span data-stu-id="c059a-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="c059a-175">有关使用此技术的详细信息，请参阅[支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="c059a-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="c059a-176">添加 MSBuild 的目标和属性</span><span class="sxs-lookup"><span data-stu-id="c059a-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="c059a-177">在某些情况下，可能需要在使用包的项目中添加自定义生成目标或属性，例如在生成过程中运行自定义工具或进程。</span><span class="sxs-lookup"><span data-stu-id="c059a-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="c059a-178">可通过在 `\build` 文件夹中添加文件来执行此操作，如以下步骤所述。</span><span class="sxs-lookup"><span data-stu-id="c059a-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="c059a-179">当 NuGet 使用 \build 文件夹安装包时，会在指向.targets 和 .props 文件的项目文件中添加 MSBuild 元素。</span><span class="sxs-lookup"><span data-stu-id="c059a-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="c059a-180">使用 `project.json` 时，目标不添加到项目，而是通过 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="c059a-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="c059a-181">在包含 `.nuspec` 文件的项目文件夹中，创建一个名为 `build` 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c059a-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="c059a-182">在 `build` 中，为支持的每个平台创建文件夹，并在这些文件夹中放置 `.targets` 和 `.props` 文件：</span><span class="sxs-lookup"><span data-stu-id="c059a-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="c059a-183">在 `.nuspec` 文件中，在 `package` 节点下添加一个 `files` 节点，并使用通配符引用 `build` 中的文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="c059a-184">使用 `nuget pack AppLogger.nuspec` 再次创建包。</span><span class="sxs-lookup"><span data-stu-id="c059a-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="c059a-185">有关更多详细信息，请参阅[将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)。</span><span class="sxs-lookup"><span data-stu-id="c059a-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="c059a-186">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="c059a-186">Creating localized packages</span></span>

<span data-ttu-id="c059a-187">若要创建库的本地化版本，可为不同的区域设置创建单独的包，也可将本地化的资源程序集包含到一个包中。</span><span class="sxs-lookup"><span data-stu-id="c059a-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="c059a-188">以下是如何为德语和意大利语执行后一种方法的操作步骤：</span><span class="sxs-lookup"><span data-stu-id="c059a-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="c059a-189">在 `lib` 下的每个目标框架文件夹中，为英语（默认）以外的每种受支持语言创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="c059a-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="c059a-190">在这些文件夹中，可放置资源程序集和本地化的 IntelliSense XML 文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="c059a-191">例如: </span><span class="sxs-lookup"><span data-stu-id="c059a-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="c059a-192">在 `.nuspec` 文件中，在 `<files>` 节点中引用这些文件：</span><span class="sxs-lookup"><span data-stu-id="c059a-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="c059a-193">使用 `nuget pack AppLogger.nuspec` 再次创建包。</span><span class="sxs-lookup"><span data-stu-id="c059a-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="c059a-194">添加自述文件</span><span class="sxs-lookup"><span data-stu-id="c059a-194">Adding a readme</span></span>

<span data-ttu-id="c059a-195">在包的根目录中包含 `readme.txt` 文件时，Visual Studio 将在直接安装包时显示该文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="c059a-196">不会显示作为依赖项安装的包或 .NET Core 项目的自述文件。</span><span class="sxs-lookup"><span data-stu-id="c059a-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="c059a-197">若要执行此操作，请创建 `readme.txt` 文件，将其放在项目根文件夹中，然后在 `.nuspec` 文件中引用：</span><span class="sxs-lookup"><span data-stu-id="c059a-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="c059a-198">.NET Standard 映射表</span><span class="sxs-lookup"><span data-stu-id="c059a-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="c059a-199">平台名称</span><span class="sxs-lookup"><span data-stu-id="c059a-199">Platform Name</span></span> |<span data-ttu-id="c059a-200">Alias</span><span class="sxs-lookup"><span data-stu-id="c059a-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="c059a-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="c059a-201">.NET Standard</span></span> | <span data-ttu-id="c059a-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="c059a-202">netstandard</span></span>| <span data-ttu-id="c059a-203">1.0</span><span class="sxs-lookup"><span data-stu-id="c059a-203">1.0</span></span>| <span data-ttu-id="c059a-204">1.1</span><span class="sxs-lookup"><span data-stu-id="c059a-204">1.1</span></span>| <span data-ttu-id="c059a-205">1.2</span><span class="sxs-lookup"><span data-stu-id="c059a-205">1.2</span></span>| <span data-ttu-id="c059a-206">1.3</span><span class="sxs-lookup"><span data-stu-id="c059a-206">1.3</span></span>| <span data-ttu-id="c059a-207">1.4</span><span class="sxs-lookup"><span data-stu-id="c059a-207">1.4</span></span>| <span data-ttu-id="c059a-208">1.5</span><span class="sxs-lookup"><span data-stu-id="c059a-208">1.5</span></span>| <span data-ttu-id="c059a-209">1.6</span><span class="sxs-lookup"><span data-stu-id="c059a-209">1.6</span></span>|
|<span data-ttu-id="c059a-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c059a-210">.NET Core</span></span> | <span data-ttu-id="c059a-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="c059a-211">netcoreapp</span></span>| <span data-ttu-id="c059a-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-212">&#x2192;</span></span>| <span data-ttu-id="c059a-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-213">&#x2192;</span></span>| <span data-ttu-id="c059a-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-214">&#x2192;</span></span>| <span data-ttu-id="c059a-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-215">&#x2192;</span></span>| <span data-ttu-id="c059a-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-216">&#x2192;</span></span>| <span data-ttu-id="c059a-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-217">&#x2192;</span></span>| <span data-ttu-id="c059a-218">1.0</span><span class="sxs-lookup"><span data-stu-id="c059a-218">1.0</span></span>|
|<span data-ttu-id="c059a-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c059a-219">.NET Framework</span></span>| <span data-ttu-id="c059a-220">net</span><span class="sxs-lookup"><span data-stu-id="c059a-220">net</span></span>| <span data-ttu-id="c059a-221">4.5</span><span class="sxs-lookup"><span data-stu-id="c059a-221">4.5</span></span>| <span data-ttu-id="c059a-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="c059a-222">4.5.1</span></span>| <span data-ttu-id="c059a-223">4.6</span><span class="sxs-lookup"><span data-stu-id="c059a-223">4.6</span></span>| <span data-ttu-id="c059a-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="c059a-224">4.6.1</span></span>| <span data-ttu-id="c059a-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="c059a-225">4.6.2</span></span>| <span data-ttu-id="c059a-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="c059a-226">4.6.3</span></span>|
|<span data-ttu-id="c059a-227">Mono/Xamarin 平台</span><span class="sxs-lookup"><span data-stu-id="c059a-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="c059a-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-228">&#x2192;</span></span>| <span data-ttu-id="c059a-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-229">&#x2192;</span></span>| <span data-ttu-id="c059a-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-230">&#x2192;</span></span>| <span data-ttu-id="c059a-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-231">&#x2192;</span></span>| <span data-ttu-id="c059a-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-232">&#x2192;</span></span>| <span data-ttu-id="c059a-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-233">&#x2192;</span></span>|
|<span data-ttu-id="c059a-234">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="c059a-234">Universal Windows Platform</span></span>| <span data-ttu-id="c059a-235">uap</span><span class="sxs-lookup"><span data-stu-id="c059a-235">uap</span></span>| <span data-ttu-id="c059a-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-236">&#x2192;</span></span>| <span data-ttu-id="c059a-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-237">&#x2192;</span></span>| <span data-ttu-id="c059a-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-238">&#x2192;</span></span>| <span data-ttu-id="c059a-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-239">&#x2192;</span></span>|<span data-ttu-id="c059a-240">10.0</span><span class="sxs-lookup"><span data-stu-id="c059a-240">10.0</span></span>|
|<span data-ttu-id="c059a-241">Windows</span><span class="sxs-lookup"><span data-stu-id="c059a-241">Windows</span></span>| <span data-ttu-id="c059a-242">win</span><span class="sxs-lookup"><span data-stu-id="c059a-242">win</span></span>| <span data-ttu-id="c059a-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-243">&#x2192;</span></span>| <span data-ttu-id="c059a-244">8.0</span><span class="sxs-lookup"><span data-stu-id="c059a-244">8.0</span></span>| <span data-ttu-id="c059a-245">8.1</span><span class="sxs-lookup"><span data-stu-id="c059a-245">8.1</span></span>|
|<span data-ttu-id="c059a-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c059a-246">Windows Phone</span></span>| <span data-ttu-id="c059a-247">wpa</span><span class="sxs-lookup"><span data-stu-id="c059a-247">wpa</span></span>| <span data-ttu-id="c059a-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-248">&#x2192;</span></span>| <span data-ttu-id="c059a-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="c059a-249">&#x2192;</span></span>|<span data-ttu-id="c059a-250">8.1</span><span class="sxs-lookup"><span data-stu-id="c059a-250">8.1</span></span>|
|<span data-ttu-id="c059a-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c059a-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="c059a-252">wp</span><span class="sxs-lookup"><span data-stu-id="c059a-252">wp</span></span>| <span data-ttu-id="c059a-253">8.0</span><span class="sxs-lookup"><span data-stu-id="c059a-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="c059a-254">相关主题</span><span class="sxs-lookup"><span data-stu-id="c059a-254">Related topics</span></span>

- [<span data-ttu-id="c059a-255">Nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="c059a-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="c059a-256">符号包</span><span class="sxs-lookup"><span data-stu-id="c059a-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="c059a-257">包版本控制</span><span class="sxs-lookup"><span data-stu-id="c059a-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c059a-258">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="c059a-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c059a-259">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="c059a-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="c059a-260">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="c059a-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c059a-261">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="c059a-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="c059a-262">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="c059a-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
