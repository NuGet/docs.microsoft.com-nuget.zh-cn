---
title: 创建适用于通用 Windows 平台的 NuGet 包
description: 从头到尾演练如何使用 C# 语言通过适用于通用 Windows 平台的 Windows 运行时组件创建 NuGet 包。
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231751"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="9c34c-103">创建 UWP 包 (C#)</span><span class="sxs-lookup"><span data-stu-id="9c34c-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="9c34c-104">[通用 Windows 平台 (UWP)](/windows/uwp) 为运行 Windows 10 的每台设备提供了一个通用应用平台。</span><span class="sxs-lookup"><span data-stu-id="9c34c-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="9c34c-105">在此模型中，UWP 应用可以调用所有设备通用的 WinRT API，以及特定于运行该应用的设备系列的 API（包括 Win32 和 .NET）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="9c34c-106">在本演练中，将创建一个具有 C# UWP 组件（包括 XAML 控件）的 NuGet 包，以便在托管项目和本机项目中使用。</span><span class="sxs-lookup"><span data-stu-id="9c34c-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c34c-107">必备条件</span><span class="sxs-lookup"><span data-stu-id="9c34c-107">Prerequisites</span></span>

1. <span data-ttu-id="9c34c-108">Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="9c34c-108">Visual Studio 2019.</span></span> <span data-ttu-id="9c34c-109">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版；也可以使用 Professional 和 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="9c34c-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="9c34c-110">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="9c34c-110">NuGet CLI.</span></span> <span data-ttu-id="9c34c-111">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 `nuget.exe` 的最新版本，将其保存到选择的位置（`.exe` 是直接下载的）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="9c34c-112">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="9c34c-113">[更多详细信息](/nuget/reference/nuget-exe-cli-reference#windows)。</span><span class="sxs-lookup"><span data-stu-id="9c34c-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="9c34c-114">创建 UWP Windows 运行时组件</span><span class="sxs-lookup"><span data-stu-id="9c34c-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="9c34c-115">在 Visual Studio 中，选择“文件”>“新建”>“项目”，搜索“uwp c#”，然后选择“Windows 运行时组件(通用 Windows)”模板，单击“下一步”，将名称更改为 ImageEnhancer，然后单击“创建”   。</span><span class="sxs-lookup"><span data-stu-id="9c34c-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="9c34c-116">出现提示时，接受“目标版本”和“最低版本”的默认值。</span><span class="sxs-lookup"><span data-stu-id="9c34c-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![创建新的 UWP Windows 运行时组件项目](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="9c34c-118">右键单击“解决方案资源管理器”中的项目，选择“添加”>“新建项目”，选择“模板控制”，将名称改为 AwesomeImageControl.cs，然后单击“添加”    ：</span><span class="sxs-lookup"><span data-stu-id="9c34c-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![将新的 XAML 模板化控件项添加到项目](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="9c34c-120">右键单击“解决方案资源管理器”中的项目，然后选择“属性” </span><span class="sxs-lookup"><span data-stu-id="9c34c-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="9c34c-121">在“属性”页面上，选择“生成”选项卡并启用“XML 文档文件”   ：</span><span class="sxs-lookup"><span data-stu-id="9c34c-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![将“生成 XML 文档文件”的值设置为“Yes”](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="9c34c-123">右键单击“解决方案”，选择“批生成”，选中对话框中的五个生成框，如下所示   。</span><span class="sxs-lookup"><span data-stu-id="9c34c-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="9c34c-124">这样可确保在生成时，将为 Windows 支持的每个目标系统生成一套完整的项目。</span><span class="sxs-lookup"><span data-stu-id="9c34c-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![批生成](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="9c34c-126">在“批生成”对话框中，单击“生成”，验证项目并创建 NuGet 包所需的输出文件  。</span><span class="sxs-lookup"><span data-stu-id="9c34c-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="9c34c-127">在本演练中，将使用包的 Debug 项目。</span><span class="sxs-lookup"><span data-stu-id="9c34c-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="9c34c-128">对于非调试包，请选中“批量生成”对话框中的 Release 选项，然后在以下步骤中引用生成的 Release 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9c34c-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9c34c-129">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="9c34c-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="9c34c-130">若要创建初始 `.nuspec` 文件，请执行以下三个步骤。</span><span class="sxs-lookup"><span data-stu-id="9c34c-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="9c34c-131">后续部分将引导你完成其他必要的更新。</span><span class="sxs-lookup"><span data-stu-id="9c34c-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="9c34c-132">打开命令提示符并导航到包含 `ImageEnhancer.csproj` 的文件夹（这将是解决方案文件下方的子文件夹）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="9c34c-133">运行 [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) 命令生成 `ImageEnhancer.nuspec`（此文件的名称取自 `.csroj` 文件的名称）：</span><span class="sxs-lookup"><span data-stu-id="9c34c-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9c34c-134">在编辑器中打开 `ImageEnhancer.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="9c34c-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9c34c-135">$propertyName$ 值均不得留空。</span><span class="sxs-lookup"><span data-stu-id="9c34c-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="9c34c-136">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="9c34c-137">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="9c34c-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="9c34c-138">对于供公共使用而生成的包，请特别注意 `<tags>` 元素，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="9c34c-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="9c34c-139">将 Windows 元数据添加到包</span><span class="sxs-lookup"><span data-stu-id="9c34c-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="9c34c-140">Windows 运行时组件需要描述其所有公共可用类型的元数据，这使得其他应用和库可使用该组件。</span><span class="sxs-lookup"><span data-stu-id="9c34c-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="9c34c-141">该元数据包含在 .winmd 文件中，此文件在编译项目时创建，并且必须包含在 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="9c34c-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="9c34c-142">同时还生成具有 IntelliSense 数据的 XML 文件，并且应该包含在内。</span><span class="sxs-lookup"><span data-stu-id="9c34c-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="9c34c-143">将以下 `<files>` 节点添加到 `.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="9c34c-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="9c34c-144">添加 XAML 内容</span><span class="sxs-lookup"><span data-stu-id="9c34c-144">Adding XAML content</span></span>

<span data-ttu-id="9c34c-145">若要在组件中包含 XAML 控件，需要添加具有默认控件模板的 XAML 文件（由项目模板生成）。</span><span class="sxs-lookup"><span data-stu-id="9c34c-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="9c34c-146">这也将进入 `<files>` 部分：</span><span class="sxs-lookup"><span data-stu-id="9c34c-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="9c34c-147">添加本机实现库</span><span class="sxs-lookup"><span data-stu-id="9c34c-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="9c34c-148">在组件中，ImageEnhancer 类型的核心逻辑是本机代码，包含在针对每个目标运行时（ARM、ARM64、x86 和 x64）生成的各种 `ImageEnhancer.winmd` 程序集中。</span><span class="sxs-lookup"><span data-stu-id="9c34c-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="9c34c-149">若要在包中包含这些文件，请在 `<files>` 部分中引用它们及其关联的 .pri 资源文件：</span><span class="sxs-lookup"><span data-stu-id="9c34c-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="9c34c-150">最终 .nuspec</span><span class="sxs-lookup"><span data-stu-id="9c34c-150">Final .nuspec</span></span>

<span data-ttu-id="9c34c-151">现在，最终 `.nuspec` 文件应该如下所示，其中应再次将 YOUR_NAME 替换为适当的值：</span><span class="sxs-lookup"><span data-stu-id="9c34c-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="9c34c-152">打包组件</span><span class="sxs-lookup"><span data-stu-id="9c34c-152">Package the component</span></span>

<span data-ttu-id="9c34c-153">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) 命令：</span><span class="sxs-lookup"><span data-stu-id="9c34c-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="9c34c-154">这将生成 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="9c34c-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9c34c-155">在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="9c34c-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![显示 ImageEnhancer 包的 NuGet 包资源管理器](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9c34c-157">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="9c34c-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9c34c-158">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="9c34c-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9c34c-159">若要使你的包可供其他开发人员使用，请按照[发布包](../nuget-org/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="9c34c-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="9c34c-160">相关主题</span><span class="sxs-lookup"><span data-stu-id="9c34c-160">Related topics</span></span>

- [<span data-ttu-id="9c34c-161">.nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="9c34c-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9c34c-162">符号包</span><span class="sxs-lookup"><span data-stu-id="9c34c-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="9c34c-163">包版本控制</span><span class="sxs-lookup"><span data-stu-id="9c34c-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="9c34c-164">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="9c34c-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9c34c-165">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="9c34c-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9c34c-166">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="9c34c-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
