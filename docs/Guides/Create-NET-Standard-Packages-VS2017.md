---
title: "使用 Visual Studio 2017 创建 .NET Standard 2.0 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "从头到尾演练如何使用 NuGet 4.x 和 Visual Studio 2017 创建 .NET Standard 2.0 NuGet 包。"
keywords: "创建包, .NET Standard 包, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="dc091-104">使用 Visual Studio 2017 创建 .NET Standard 2.0 包</span><span class="sxs-lookup"><span data-stu-id="dc091-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="dc091-105">*在提供 Visual Studio 2017 Update 3 的情况下适用于 NuGet 4.x+ 和 MSBuild 15.3+。对于更早版本的 Visual Studio 2017，可以更改 \<TargetFramework\> 属性使这些说明适用于 .NET Standard 1.4 到 1.6。还可参阅[使用 Visual Studio 2015 创建 .NET Standard 包](../guides/create-net-standard-packages-vs2015.md)，了解如何使用 NuGet 3.x+。*</span><span class="sxs-lookup"><span data-stu-id="dc091-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="dc091-106">[.NET Standard 库](/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。</span><span class="sxs-lookup"><span data-stu-id="dc091-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="dc091-107">.NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。</span><span class="sxs-lookup"><span data-stu-id="dc091-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="dc091-108">它使得开发人员可以生成跨所有 .NET 运行时可用的 PCL，并减少（如果不能消除）共享代码中平台特定的条件编译指令。</span><span class="sxs-lookup"><span data-stu-id="dc091-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="dc091-109">本指南将指导你使用 Visual Studio 2017 Update 3 和 NuGet 4.0 创建面向 .NET Standard 2.0 库的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="dc091-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="dc091-110">先决条件</span><span class="sxs-lookup"><span data-stu-id="dc091-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="dc091-111">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="dc091-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="dc091-112">在 .csproj 文件中编辑元数据</span><span class="sxs-lookup"><span data-stu-id="dc091-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="dc091-113">打包组件</span><span class="sxs-lookup"><span data-stu-id="dc091-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="dc091-114">相关主题</span><span class="sxs-lookup"><span data-stu-id="dc091-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="dc091-115">先决条件</span><span class="sxs-lookup"><span data-stu-id="dc091-115">Pre-requisites</span></span>

<span data-ttu-id="dc091-116">本演练需要带“.NET Core 跨平台开发”工作负荷的 Visual Studio 2017 Update 3。</span><span class="sxs-lookup"><span data-stu-id="dc091-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="dc091-117">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版，也可以使用 Professional 和 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="dc091-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="dc091-118">所需工作负荷在 Visual Studio 安装程序中显示为：</span><span class="sxs-lookup"><span data-stu-id="dc091-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="dc091-120">创建 .NET Standard 类库项目</span><span class="sxs-lookup"><span data-stu-id="dc091-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="dc091-121">在 Visual Studio 中，单击“文件”>“新建”>“项目”，展开“Visual C#”>“.NET Standard”节点，选择“类库(Net Standard)”，将名称更改为 AppLogger，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="dc091-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![创建新类库项目](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="dc091-123">将生成配置更改为“Release”。</span><span class="sxs-lookup"><span data-stu-id="dc091-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="dc091-124">右键单击解决方案资源管理器中的 `AppLogger` 项目，选择“属性”，选择“生成”选项卡，选中“XML 文档文件”框，然后将文件名设为 `AppLogger.xml`。</span><span class="sxs-lookup"><span data-stu-id="dc091-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="dc091-125">然后保存项目。</span><span class="sxs-lookup"><span data-stu-id="dc091-125">Then save the project.</span></span>

1. <span data-ttu-id="dc091-126">将代码添加到组件，如以下内容（这些内容明显只是到控制台的输出消息）：</span><span class="sxs-lookup"><span data-stu-id="dc091-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

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

1. <span data-ttu-id="dc091-127">生成项目（使用 Release 配置）并检查 `bin\Release\netstandard2.0` 文件夹中生成了 DLL 和 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="dc091-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="dc091-128">在 .csproj 文件中编辑元数据</span><span class="sxs-lookup"><span data-stu-id="dc091-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="dc091-129">有了 NuGet 4.0 和 .NET Core 项目，包元数据直接包含在 `.csproj` 文件中，而不是 `.nuspec` 等外部文件中。</span><span class="sxs-lookup"><span data-stu-id="dc091-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="dc091-130">可以在[作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md#pack-target)中找到该元数据的完整说明。</span><span class="sxs-lookup"><span data-stu-id="dc091-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="dc091-131">右键单击解决方案资源管理器中的项目，选择“编辑 AppLogger.csproj”，然后将第一个属性组编辑为包含如下包信息：</span><span class="sxs-lookup"><span data-stu-id="dc091-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="dc091-132">保存项目，然后右键单击解决方案并选择“生成解决方案”再次为包生成所有文件，这一次使用正确的元数据。</span><span class="sxs-lookup"><span data-stu-id="dc091-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="dc091-133">打包组件</span><span class="sxs-lookup"><span data-stu-id="dc091-133">Package the component</span></span>

<span data-ttu-id="dc091-134">项目包含必要包元数据时（如上一部分所添加），NuGet 4.0 支持包目标使用 MSBuild 版本 15.1+（包括作为 Visual Studio 2017 Update 3 一部分的 MSBuild 15.3）。</span><span class="sxs-lookup"><span data-stu-id="dc091-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="dc091-135">若要使用此方法调用 MSBuild，只需在与 `.csproj` 文件相同的文件夹的命令行上指定包目标：</span><span class="sxs-lookup"><span data-stu-id="dc091-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="dc091-136">有关 `msbuild /t:pack` 的其他选项，例如包含内容文件、符号和源代码，请参阅[作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="dc091-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="dc091-137">在任何情况下，上述命令都会默认在 `bin\Release` 文件夹中生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`，因为它生成该配置。</span><span class="sxs-lookup"><span data-stu-id="dc091-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="dc091-138">如果忽略 `/p` 开关，默认配置将为 `Debug`。</span><span class="sxs-lookup"><span data-stu-id="dc091-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="dc091-139">在 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)（NuGet 包资源管理器）之类的工具中打开此文件，并展开所有节点，随即将看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="dc091-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![显示 AppLogger 包的 NuGet 包资源管理器](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="dc091-141">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="dc091-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="dc091-142">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="dc091-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="dc091-143">若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="dc091-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="dc091-144">相关主题</span><span class="sxs-lookup"><span data-stu-id="dc091-144">Related topics</span></span>

- <span data-ttu-id="dc091-145">[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)介绍直接在项目文件中描述包的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="dc091-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="dc091-146">[作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md)介绍使用 `msbuild /t:pack` 创建包的所有选项。</span><span class="sxs-lookup"><span data-stu-id="dc091-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="dc091-147">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="dc091-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="dc091-148">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc091-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
