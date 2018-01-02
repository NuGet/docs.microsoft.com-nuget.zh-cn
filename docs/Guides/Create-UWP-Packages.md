---
title: "创建适用于通用 Windows 平台的 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: d98524b1-a674-4803-8ac5-3c6bce867f86
description: "从头到尾演练如何使用适用于通用 Windows 平台的 Windows 运行时组件创建 NuGet 包。"
keywords: "创建包, 适用于 UWP 的包, Windows 运行时组件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0513ad063d01e573672b6c84a9e819b6df516f03
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="create-uwp-packages"></a><span data-ttu-id="4d1fd-104">创建 UWP 包</span><span class="sxs-lookup"><span data-stu-id="4d1fd-104">Create UWP packages</span></span>

<span data-ttu-id="4d1fd-105">[通用 Windows 平台 (UWP)](https://developer.microsoft.com/windows) 为运行 Windows 10 的每台设备提供了一个通用应用平台。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-105">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="4d1fd-106">在此模型中，UWP 应用可以调用所有设备通用的 WinRT API，以及特定于运行该应用的设备系列的 API（包括 Win32 和 .NET）。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-106">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="4d1fd-107">在本演练中，将创建一个具有本机 UWP 组件（包括 XAML 控件）的 NuGet 包，以便在托管项目和本机项目中使用。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-107">In this walkthrough you'll create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

1. [<span data-ttu-id="4d1fd-108">先决条件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="4d1fd-109">创建 UWP Windows 运行时组件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-109">Create a UWP Windows Runtime Component</span></span>](#create-a-uwp-windows-runtime-component)
1. [<span data-ttu-id="4d1fd-110">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="4d1fd-111">打包组件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="4d1fd-112">相关主题</span><span class="sxs-lookup"><span data-stu-id="4d1fd-112">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="4d1fd-113">先决条件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-113">Pre-requisites</span></span>

1. <span data-ttu-id="4d1fd-114">Visual Studio 2017 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-114">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="4d1fd-115">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版；也可以使用 Professional 和 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>
1. <span data-ttu-id="4d1fd-116">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-116">NuGet CLI.</span></span> <span data-ttu-id="4d1fd-117">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-117">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="4d1fd-118">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-118">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="4d1fd-119">nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-119">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="4d1fd-120">创建 UWP Windows 运行时组件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-120">Create a UWP Windows Runtime Component</span></span>

1. <span data-ttu-id="4d1fd-121">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C++”>“Windows”>“Universal”节点，选择“Windows 运行时组件(通用 Windows)”，将名称更改为“ImageEnhancer”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="4d1fd-122">出现提示时，接受“目标版本”和“最低版本”的默认值。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![创建新的 UWP Windows 运行时组件项目](media/UWP-NewProject.png)

1. <span data-ttu-id="4d1fd-124">右键单击“解决方案资源管理器”中的项目，选择“添加”>“新建项目”，单击“Visual C++”>“XAML”节点，选择“模板控制”，将名称更改为“AwesomeImageControl.cpp”，然后单击“添加”：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-124">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![将新的 XAML 模板化控件项添加到项目](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="4d1fd-126">右键单击“解决方案资源管理器”中的项目，然后选择“属性”</span><span class="sxs-lookup"><span data-stu-id="4d1fd-126">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="4d1fd-127">在“属性”页中，展开“配置属性”>“C/C++”，然后单击“输出文件”。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-127">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="4d1fd-128">在右侧窗格中，将“生成 XML 文档文件”的值更改为“Yes”：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-128">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![将“生成 XML 文档文件”的值设置为“Yes”](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="4d1fd-130">现在，右键单击“解决方案”，选择“批生成”，选中对话框中的三个 Debug 框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-130">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="4d1fd-131">这样可确保在生成时，将为 Windows 支持的每个目标系统生成一套完整项目。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-131">This makes sure that when you do a build, you'll generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![批生成](media/UWP-BatchBuild.png)

1. <span data-ttu-id="4d1fd-133">在“批生成”对话框中，单击“生成”，验证项目并创建 NuGet 程序包所需的输出文件。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-133">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you'll need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="4d1fd-134">在本演练中，将使用包的 Debug 项目。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-134">In this walkthrough you'll use the Debug artifacts for the package.</span></span> <span data-ttu-id="4d1fd-135">对于非调试包，请选中“批量生成”对话框中的 Release 选项，然后在以下步骤中引用生成的 Release 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-135">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="4d1fd-136">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-136">Create and update the .nuspec file</span></span>

<span data-ttu-id="4d1fd-137">若要创建初始 `.nuspec` 文件，请执行以下三个步骤。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-137">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="4d1fd-138">后续部分将引导你完成其他必要的更新。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-138">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="4d1fd-139">打开命令提示符并导航到包含 `ImageEnhancer.vcxproj` 的文件夹（这将是解决方案文件下方的子文件夹）。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-139">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="4d1fd-140">运行 NuGet `spec` 命令生成 `ImageEnhancer.nuspec`（文件的名称取自 `.vcxproj` 文件的名称）：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-140">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="4d1fd-141">在编辑器中打开 `ImageEnhancer.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-141">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="4d1fd-142">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-142">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="4d1fd-143">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-143">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="4d1fd-144">对于供公共使用而生成的包，请特别注意 `<tags>` 元素，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-144">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>



### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="4d1fd-145">将 Windows 元数据添加到包</span><span class="sxs-lookup"><span data-stu-id="4d1fd-145">Adding Windows metadata to the package</span></span>

<span data-ttu-id="4d1fd-146">Windows 运行时组件需要描述其所有公共可用类型的元数据，这使得其他应用和库可使用该组件。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-146">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="4d1fd-147">该元数据包含在 .winmd 文件中，此文件在编译项目时创建，并且必须包含在 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-147">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="4d1fd-148">同时还生成具有 IntelliSense 数据的 XML 文件，并且应该包含在内。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-148">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="4d1fd-149">将以下 `<files>` 节点添加到 `.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-149">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="4d1fd-150">添加 XAML 内容</span><span class="sxs-lookup"><span data-stu-id="4d1fd-150">Adding XAML content</span></span>

<span data-ttu-id="4d1fd-151">若要在组件中包含 XAML 控件，需要添加具有默认控件模板的 XAML 文件（由项目模板生成）。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-151">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="4d1fd-152">这也将进入 `<files>` 部分：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-152">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="4d1fd-153">添加本机实现库</span><span class="sxs-lookup"><span data-stu-id="4d1fd-153">Adding the native implementation libraries</span></span>

<span data-ttu-id="4d1fd-154">在组件中，ImageEnhancer 类型的核心逻辑是本机代码，包含在针对每个目标运行时（ARM、x86 和 x64）生成的各种 `ImageEnhancer.dll` 程序集中。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-154">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="4d1fd-155">若要在包中包含这些文件，请在 `<files>` 部分中引用它们及其关联的 .pri 资源文件：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-155">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="4d1fd-156">添加 .targets</span><span class="sxs-lookup"><span data-stu-id="4d1fd-156">Adding .targets</span></span>

<span data-ttu-id="4d1fd-157">接下来，可能使用 NuGet 包的 C++ 和 JavaScript 项目需要一个 .targets 文件来标识必要的程序集和 winmd 文件。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-157">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="4d1fd-158">（C# 和 Visual Basic 项目自动执行此操作。）通过将下方文本复制到 `ImageEnhancer.targets` 创建此文件，并将其保存在与 `.nuspec` 文件相同的文件夹中：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-158">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="4d1fd-159">然后在 `.nuspec` 文件中引用 `ImageEnhancer.targets`：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-159">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="4d1fd-160">最终 .nuspec</span><span class="sxs-lookup"><span data-stu-id="4d1fd-160">Final .nuspec</span></span>

<span data-ttu-id="4d1fd-161">现在，最终 `.nuspec` 文件应该如下所示，其中应再次将 YOUR_NAME 替换为适当的值：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-161">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```


## <a name="package-the-component"></a><span data-ttu-id="4d1fd-162">打包组件</span><span class="sxs-lookup"><span data-stu-id="4d1fd-162">Package the component</span></span>

<span data-ttu-id="4d1fd-163">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-163">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="4d1fd-164">将生成 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-164">This will generate `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="4d1fd-165">在 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)（NuGet 包资源管理器）之类的工具中打开此文件，并展开所有节点，随即将看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="4d1fd-165">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![显示 ImageEnhancer 包的 NuGet 包资源管理器](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="4d1fd-167">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-167">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="4d1fd-168">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-168">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="4d1fd-169">若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="4d1fd-169">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="4d1fd-170">相关主题</span><span class="sxs-lookup"><span data-stu-id="4d1fd-170">Related topics</span></span>

- [<span data-ttu-id="4d1fd-171">.nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="4d1fd-171">.nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="4d1fd-172">符号包</span><span class="sxs-lookup"><span data-stu-id="4d1fd-172">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="4d1fd-173">包版本控制</span><span class="sxs-lookup"><span data-stu-id="4d1fd-173">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4d1fd-174">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="4d1fd-174">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4d1fd-175">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="4d1fd-175">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4d1fd-176">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="4d1fd-176">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)