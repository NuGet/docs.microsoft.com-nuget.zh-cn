---
title: 使用 Visual Studio 2015 创建 .NET Standard 和 .NET Framework NuGet 包
description: 从头到尾介绍如何使用 NuGet 3.x 和 Visual Studio 2015 创建 .NET Standard 和 .NET Framework NuGet 包。
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842445"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="79340-103">使用 Visual Studio 2015 创建 NET Standard 和 .NET Framework 包</span><span class="sxs-lookup"><span data-stu-id="79340-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="79340-104">**注意：** 建议使用 Visual Studio 2017 来开发 .NET Standard 库。</span><span class="sxs-lookup"><span data-stu-id="79340-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="79340-105">Visual Studio 2015 可以工作，但 .NET Core 工具仅处于预览状态。</span><span class="sxs-lookup"><span data-stu-id="79340-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="79340-106">有关使用 NuGet 4.x+ 和 Visual Studio 2017 的详细信息，请参阅[使用 Visual Studio 2017 创建和发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="79340-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="79340-107">[.NET Standard 库](/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。</span><span class="sxs-lookup"><span data-stu-id="79340-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="79340-108">.NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。</span><span class="sxs-lookup"><span data-stu-id="79340-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="79340-109">它使得开发人员可以生成跨所有 .NET 运行时可用的代码，并减少（如果不能消除）共享代码中平台特定的条件编译指令。</span><span class="sxs-lookup"><span data-stu-id="79340-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="79340-110">本指南将为你逐步介绍如何创建面向 .NET Standard 库 1.4 的 NuGet 包或面向 .NET Framework 4.6 的包。</span><span class="sxs-lookup"><span data-stu-id="79340-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="79340-111">.NET Standard 1.4 库可在 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 上使用。</span><span class="sxs-lookup"><span data-stu-id="79340-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="79340-112">有关详细信息，请参阅 [.NET Standard 映射表](/dotnet/standard/net-standard#net-implementation-support)（.NET 文档）。</span><span class="sxs-lookup"><span data-stu-id="79340-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="79340-113">如果需要，可以选择其他版本的 .NET Standard 库。</span><span class="sxs-lookup"><span data-stu-id="79340-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79340-114">系统必备</span><span class="sxs-lookup"><span data-stu-id="79340-114">Prerequisites</span></span>

1. <span data-ttu-id="79340-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="79340-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="79340-116">（仅适用于 .NET Standard）[.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="79340-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="79340-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="79340-117">NuGet CLI.</span></span> <span data-ttu-id="79340-118">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。</span><span class="sxs-lookup"><span data-stu-id="79340-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="79340-119">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="79340-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="79340-120">nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。</span><span class="sxs-lookup"><span data-stu-id="79340-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="79340-121">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="79340-121">Create the class library project</span></span>

1. <span data-ttu-id="79340-122">在 Visual Studio 中，选择“文件”>“新建”>“项目”  ，展开“Visual C#”>“Windows”  节点，选择“类库(可移植)”  ，将名称更改为“AppLogger”，然后选择“确定”  。</span><span class="sxs-lookup"><span data-stu-id="79340-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![创建新类库项目](media/NetStandard-NewProject.png)

1. <span data-ttu-id="79340-124">在显示的“添加可移植类库”  对话框中，选择 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 选项。</span><span class="sxs-lookup"><span data-stu-id="79340-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="79340-125">（如果面向 .NET Framework，则可以选择任何相应选项。）</span><span class="sxs-lookup"><span data-stu-id="79340-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="79340-126">如果面向 .NET Standard，右键单击解决方案资源管理器中的 `AppLogger (Portable)`，选择“属性”  ，选择“库”  选项卡，然后选择“目标”  部分中的“目标 .NET 平台标准”  。</span><span class="sxs-lookup"><span data-stu-id="79340-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="79340-127">此操作将提示进行确认，在确认后可以从下拉列表中选择 `.NET Standard 1.4`（或其他可用版本）：</span><span class="sxs-lookup"><span data-stu-id="79340-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![将目标设置为 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="79340-129">单击“生成”选项卡，将“配置”更改为 `Release`，然后选中“XML 文档文件”框    。</span><span class="sxs-lookup"><span data-stu-id="79340-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="79340-130">将代码添加到组件，例如：</span><span class="sxs-lookup"><span data-stu-id="79340-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="79340-131">将配置设置为“发布”，生成项目，并检查 `bin\Release` 文件夹中生成了 DLL 和 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="79340-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="79340-132">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="79340-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="79340-133">打开命令提示符，导航到包含 `AppLogger.csproj` 文件夹的文件夹（`.sln` 文件的下一级），然后运行 NuGet `spec` 命令，创建初始 `AppLogger.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="79340-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="79340-134">在编辑器中打开 `AppLogger.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="79340-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="79340-135">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="79340-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="79340-136">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="79340-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="79340-137">将引用程序集添加到 `.nuspec` 文件，也就是库的 DLL 和 IntelliSense XML 文件：</span><span class="sxs-lookup"><span data-stu-id="79340-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="79340-138">如果面向 .NET Standard，则条目类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="79340-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="79340-139">如果面向 .NET Framework ，则条目类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="79340-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="79340-140">右键单击解决方案，选择“生成解决方案”，生成包的所有文件  。</span><span class="sxs-lookup"><span data-stu-id="79340-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="79340-141">声明依赖项</span><span class="sxs-lookup"><span data-stu-id="79340-141">Declaring dependencies</span></span>

<span data-ttu-id="79340-142">如果具有其他 NuGet 包的任何依赖项，请使用 `<group>` 元素在清单的 `<dependencies>` 元素中列出这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="79340-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="79340-143">例如，若要在 NewtonSoft.Json 8.0.3 或更高版本上声明依赖项，请添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="79340-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="79340-144">此处 version 特性的语法指示可接受版本 8.0.3 或更高版本  。</span><span class="sxs-lookup"><span data-stu-id="79340-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="79340-145">若要指定不同的版本范围，请参阅[包版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="79340-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="79340-146">添加自述文件</span><span class="sxs-lookup"><span data-stu-id="79340-146">Adding a readme</span></span>

<span data-ttu-id="79340-147">创建 `readme.txt` 文件，将其放在项目根文件夹中，然后在 `.nuspec` 文件中引用：</span><span class="sxs-lookup"><span data-stu-id="79340-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="79340-148">将包安装到项目中时，Visual Studio 显示 `readme.txt`。</span><span class="sxs-lookup"><span data-stu-id="79340-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="79340-149">当安装到 .NET Core 项目中或其作为依赖项安装的包时，不会显示该文件。</span><span class="sxs-lookup"><span data-stu-id="79340-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="79340-150">打包组件</span><span class="sxs-lookup"><span data-stu-id="79340-150">Package the component</span></span>

<span data-ttu-id="79340-151">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="79340-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="79340-152">这将生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="79340-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="79340-153">在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容（显示为 .NET Standard）：</span><span class="sxs-lookup"><span data-stu-id="79340-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![显示 AppLogger 包的 NuGet 包资源管理器](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="79340-155">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="79340-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="79340-156">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="79340-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="79340-157">若要使你的包可供其他开发人员使用，请按照[发布包](../nuget-org/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="79340-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="79340-158">请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。</span><span class="sxs-lookup"><span data-stu-id="79340-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="79340-159">在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。</span><span class="sxs-lookup"><span data-stu-id="79340-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="79340-160">相关主题</span><span class="sxs-lookup"><span data-stu-id="79340-160">Related topics</span></span>

- [<span data-ttu-id="79340-161">Nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="79340-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="79340-162">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="79340-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="79340-163">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="79340-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="79340-164">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="79340-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="79340-165">符号包</span><span class="sxs-lookup"><span data-stu-id="79340-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="79340-166">包版本控制</span><span class="sxs-lookup"><span data-stu-id="79340-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="79340-167">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="79340-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="79340-168">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="79340-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
