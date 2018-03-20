---
title: "使用 Visual Studio 2015 创建 .NET Standard NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "从头到尾介绍如何使用 NuGet 3.x 和 Visual Studio 2015 创建 .NET Standard NuGet 包。"
keywords: "创建包, .NET Standard 包, .NET Standard 映射表"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="37a3a-104">使用 Visual Studio 2015 创建 .NET Standard 包</span><span class="sxs-lookup"><span data-stu-id="37a3a-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="37a3a-105">适用于 NuGet 3.x。有关使用 NuGet 4.x+ 的详细信息，请参阅[使用 Visual Studio 2017 创建和发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="37a3a-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="37a3a-106">[.NET Standard 库](/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。</span><span class="sxs-lookup"><span data-stu-id="37a3a-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="37a3a-107">.NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。</span><span class="sxs-lookup"><span data-stu-id="37a3a-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="37a3a-108">它使得开发人员可以生成跨所有 .NET 运行时可用的代码，并减少（如果不能消除）共享代码中平台特定的条件编译指令。</span><span class="sxs-lookup"><span data-stu-id="37a3a-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="37a3a-109">本指南将指导你创建一个面向 .NET Standard 库 1.4 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="37a3a-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="37a3a-110">此类库可在 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 上使用。</span><span class="sxs-lookup"><span data-stu-id="37a3a-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="37a3a-111">有关详细信息，请参阅本主题后面的 [.NET Standard 映射表](#net-standard-mapping-table)。</span><span class="sxs-lookup"><span data-stu-id="37a3a-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37a3a-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="37a3a-112">Prerequisites</span></span>

1. <span data-ttu-id="37a3a-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="37a3a-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="37a3a-114">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="37a3a-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="37a3a-115">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="37a3a-115">NuGet CLI.</span></span> <span data-ttu-id="37a3a-116">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。</span><span class="sxs-lookup"><span data-stu-id="37a3a-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="37a3a-117">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="37a3a-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="37a3a-118">nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。</span><span class="sxs-lookup"><span data-stu-id="37a3a-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="37a3a-119">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="37a3a-119">Create the class library project</span></span>

1. <span data-ttu-id="37a3a-120">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C#”>“Windows”节点，选择“类库(可移植)”，将名称更改为“AppLogger”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="37a3a-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![创建新类库项目](media/NetStandard-NewProject.png)

1. <span data-ttu-id="37a3a-122">在“添加可移植类库”对话框中，选择 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 选项。</span><span class="sxs-lookup"><span data-stu-id="37a3a-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="37a3a-123">右键单击解决方案资源管理器中的 `AppLogger (Portable)`，选择“属性”，选择“库”选项卡，然后单击“目标”部分中的“目标 .NET 平台标准”。</span><span class="sxs-lookup"><span data-stu-id="37a3a-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="37a3a-124">这将提示进行确认，之后可从下拉列表中选择 `.NET Standard 1.4`：</span><span class="sxs-lookup"><span data-stu-id="37a3a-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![将目标设置为 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="37a3a-126">单击“生成”选项卡，将“配置”更改为 `Release`，然后选中“XML 文档文件”框。</span><span class="sxs-lookup"><span data-stu-id="37a3a-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="37a3a-127">将代码添加到组件，例如：</span><span class="sxs-lookup"><span data-stu-id="37a3a-127">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="37a3a-128">将配置设置为“发布”，生成项目，并检查 `bin\Release` 文件夹中生成了 DLL 和 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="37a3a-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="37a3a-129">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="37a3a-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="37a3a-130">打开命令提示符，导航到包含 `AppLogger.csproj` 文件夹的文件夹（`.sln` 文件的下一级），然后运行 NuGet `spec` 命令，创建初始 `AppLogger.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="37a3a-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="37a3a-131">在编辑器中打开 `AppLogger.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="37a3a-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="37a3a-132">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="37a3a-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="37a3a-133">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="37a3a-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="37a3a-134">将引用程序集添加到 `.nuspec` 文件，也就是库的 DLL 和 IntelliSense XML 文件：</span><span class="sxs-lookup"><span data-stu-id="37a3a-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="37a3a-135">右键单击解决方案，选择“生成解决方案”，生成包的所有文件。</span><span class="sxs-lookup"><span data-stu-id="37a3a-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="37a3a-136">声明依赖项</span><span class="sxs-lookup"><span data-stu-id="37a3a-136">Declaring dependencies</span></span>

<span data-ttu-id="37a3a-137">如果具有其他 NuGet 包的任何依赖项，请使用 `<group>` 元素在清单的 `<dependencies>` 元素中列出这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="37a3a-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="37a3a-138">例如，若要在 NewtonSoft.Json 8.0.3 或更高版本上声明依赖项，请添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="37a3a-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="37a3a-139">此处 version 特性的语法指示可接受版本 8.0.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="37a3a-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="37a3a-140">若要指定不同的版本范围，请参阅[包版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="37a3a-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="37a3a-141">添加自述文件</span><span class="sxs-lookup"><span data-stu-id="37a3a-141">Adding a readme</span></span>

<span data-ttu-id="37a3a-142">创建 `readme.txt` 文件，将其放在项目根文件夹中，然后在 `.nuspec` 文件中引用：</span><span class="sxs-lookup"><span data-stu-id="37a3a-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="37a3a-143">将包安装到项目中时，Visual Studio 显示 `readme.txt`。</span><span class="sxs-lookup"><span data-stu-id="37a3a-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="37a3a-144">当安装到 .NET Core 项目中或其作为依赖项安装的包时，不会显示该文件。</span><span class="sxs-lookup"><span data-stu-id="37a3a-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="37a3a-145">打包组件</span><span class="sxs-lookup"><span data-stu-id="37a3a-145">Package the component</span></span>

<span data-ttu-id="37a3a-146">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="37a3a-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="37a3a-147">将生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="37a3a-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="37a3a-148">在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="37a3a-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![显示 AppLogger 包的 NuGet 包资源管理器](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="37a3a-150">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="37a3a-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="37a3a-151">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="37a3a-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="37a3a-152">若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="37a3a-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="37a3a-153">请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。</span><span class="sxs-lookup"><span data-stu-id="37a3a-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="37a3a-154">在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。</span><span class="sxs-lookup"><span data-stu-id="37a3a-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="37a3a-155">.NET Standard 映射表</span><span class="sxs-lookup"><span data-stu-id="37a3a-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="37a3a-156">平台名称</span><span class="sxs-lookup"><span data-stu-id="37a3a-156">Platform Name</span></span> | <span data-ttu-id="37a3a-157">Alias</span><span class="sxs-lookup"><span data-stu-id="37a3a-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="37a3a-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="37a3a-158">.NET Standard</span></span> | <span data-ttu-id="37a3a-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="37a3a-159">netstandard</span></span> | <span data-ttu-id="37a3a-160">1.0</span><span class="sxs-lookup"><span data-stu-id="37a3a-160">1.0</span></span> | <span data-ttu-id="37a3a-161">1.1</span><span class="sxs-lookup"><span data-stu-id="37a3a-161">1.1</span></span> | <span data-ttu-id="37a3a-162">1.2</span><span class="sxs-lookup"><span data-stu-id="37a3a-162">1.2</span></span> | <span data-ttu-id="37a3a-163">1.3</span><span class="sxs-lookup"><span data-stu-id="37a3a-163">1.3</span></span> | <span data-ttu-id="37a3a-164">1.4</span><span class="sxs-lookup"><span data-stu-id="37a3a-164">1.4</span></span> | <span data-ttu-id="37a3a-165">1.5</span><span class="sxs-lookup"><span data-stu-id="37a3a-165">1.5</span></span> | <span data-ttu-id="37a3a-166">1.6</span><span class="sxs-lookup"><span data-stu-id="37a3a-166">1.6</span></span> |
| <span data-ttu-id="37a3a-167">.NET 核心</span><span class="sxs-lookup"><span data-stu-id="37a3a-167">.NET Core</span></span> | <span data-ttu-id="37a3a-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="37a3a-168">netcoreapp</span></span> | <span data-ttu-id="37a3a-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-169">&#x2192;</span></span> | <span data-ttu-id="37a3a-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-170">&#x2192;</span></span> | <span data-ttu-id="37a3a-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-171">&#x2192;</span></span> | <span data-ttu-id="37a3a-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-172">&#x2192;</span></span> | <span data-ttu-id="37a3a-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-173">&#x2192;</span></span> | <span data-ttu-id="37a3a-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-174">&#x2192;</span></span> | <span data-ttu-id="37a3a-175">1.0</span><span class="sxs-lookup"><span data-stu-id="37a3a-175">1.0</span></span> |
| <span data-ttu-id="37a3a-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="37a3a-176">.NET Framework</span></span> | <span data-ttu-id="37a3a-177">net</span><span class="sxs-lookup"><span data-stu-id="37a3a-177">net</span></span> | <span data-ttu-id="37a3a-178">4.5</span><span class="sxs-lookup"><span data-stu-id="37a3a-178">4.5</span></span> | <span data-ttu-id="37a3a-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="37a3a-179">4.5.1</span></span> | <span data-ttu-id="37a3a-180">4.6</span><span class="sxs-lookup"><span data-stu-id="37a3a-180">4.6</span></span> | <span data-ttu-id="37a3a-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="37a3a-181">4.6.1</span></span> | <span data-ttu-id="37a3a-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="37a3a-182">4.6.2</span></span> | <span data-ttu-id="37a3a-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="37a3a-183">4.6.3</span></span> |
| <span data-ttu-id="37a3a-184">Mono/Xamarin 平台</span><span class="sxs-lookup"><span data-stu-id="37a3a-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="37a3a-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-185">&#x2192;</span></span> | <span data-ttu-id="37a3a-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-186">&#x2192;</span></span> | <span data-ttu-id="37a3a-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-187">&#x2192;</span></span> | <span data-ttu-id="37a3a-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-188">&#x2192;</span></span> | <span data-ttu-id="37a3a-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-189">&#x2192;</span></span> | <span data-ttu-id="37a3a-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-190">&#x2192;</span></span> |
| <span data-ttu-id="37a3a-191">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="37a3a-191">Universal Windows Platform</span></span> | <span data-ttu-id="37a3a-192">uap</span><span class="sxs-lookup"><span data-stu-id="37a3a-192">uap</span></span> | <span data-ttu-id="37a3a-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-193">&#x2192;</span></span> | <span data-ttu-id="37a3a-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-194">&#x2192;</span></span> | <span data-ttu-id="37a3a-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-195">&#x2192;</span></span> | <span data-ttu-id="37a3a-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-196">&#x2192;</span></span> |<span data-ttu-id="37a3a-197">10.0</span><span class="sxs-lookup"><span data-stu-id="37a3a-197">10.0</span></span> |
| <span data-ttu-id="37a3a-198">Windows</span><span class="sxs-lookup"><span data-stu-id="37a3a-198">Windows</span></span> | <span data-ttu-id="37a3a-199">win</span><span class="sxs-lookup"><span data-stu-id="37a3a-199">win</span></span>| <span data-ttu-id="37a3a-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-200">&#x2192;</span></span> | <span data-ttu-id="37a3a-201">8.0</span><span class="sxs-lookup"><span data-stu-id="37a3a-201">8.0</span></span> | <span data-ttu-id="37a3a-202">8.1</span><span class="sxs-lookup"><span data-stu-id="37a3a-202">8.1</span></span> |
| <span data-ttu-id="37a3a-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="37a3a-203">Windows Phone</span></span> | <span data-ttu-id="37a3a-204">wpa</span><span class="sxs-lookup"><span data-stu-id="37a3a-204">wpa</span></span>| <span data-ttu-id="37a3a-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-205">&#x2192;</span></span>| <span data-ttu-id="37a3a-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="37a3a-206">&#x2192;</span></span> | <span data-ttu-id="37a3a-207">8.1</span><span class="sxs-lookup"><span data-stu-id="37a3a-207">8.1</span></span> |
| <span data-ttu-id="37a3a-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="37a3a-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="37a3a-209">wp</span><span class="sxs-lookup"><span data-stu-id="37a3a-209">wp</span></span> | <span data-ttu-id="37a3a-210">8.0</span><span class="sxs-lookup"><span data-stu-id="37a3a-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="37a3a-211">相关主题</span><span class="sxs-lookup"><span data-stu-id="37a3a-211">Related topics</span></span>

- [<span data-ttu-id="37a3a-212">Nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="37a3a-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="37a3a-213">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="37a3a-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="37a3a-214">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="37a3a-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="37a3a-215">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="37a3a-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="37a3a-216">符号包</span><span class="sxs-lookup"><span data-stu-id="37a3a-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="37a3a-217">包版本控制</span><span class="sxs-lookup"><span data-stu-id="37a3a-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="37a3a-218">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="37a3a-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="37a3a-219">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="37a3a-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
