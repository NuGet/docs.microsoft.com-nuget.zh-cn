---
title: 如何使用 NuGet 打包 UWP 控件 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: 如何创建包含 UWP 控件的 NuGet 包，包括必要的元数据和 Visual Studio 和 Blend 设计器的支持文件。
keywords: NuGet UWP 控件, Visual Studio XAML 设计器, Blend 设计器, 自定义控件
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f024fd1823c77d57d30c4f841bf03494194c8339
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="bea6f-104">以 NuGet 包形式创建 UWP 控件</span><span class="sxs-lookup"><span data-stu-id="bea6f-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="bea6f-105">通过 Visual Studio 2017，可以利用在 NuGet 包中提供的 UWP 控件新增功能。</span><span class="sxs-lookup"><span data-stu-id="bea6f-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="bea6f-106">本指南使用 [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)来演练这些功能。</span><span class="sxs-lookup"><span data-stu-id="bea6f-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bea6f-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="bea6f-107">Prerequisites</span></span>

1. <span data-ttu-id="bea6f-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bea6f-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="bea6f-109">了解如何[创建 UWP 包](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="bea6f-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="bea6f-110">添加对 XAML 控件的工具箱/资产窗格支持</span><span class="sxs-lookup"><span data-stu-id="bea6f-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="bea6f-111">要使 XAML 控件出现在 Visual Studio 中的 XAML 设计器工具箱和 Blend 的“资产”窗格中，请在包项目的 `tools` 文件夹根中创建 `VisualStudioToolsManifest.xml` 文件。</span><span class="sxs-lookup"><span data-stu-id="bea6f-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="bea6f-112">如果不需要控件显示在工具箱或“资产”窗格中，则不需要此文件。</span><span class="sxs-lookup"><span data-stu-id="bea6f-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="bea6f-113">文件的结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="bea6f-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="bea6f-114">其中：</span><span class="sxs-lookup"><span data-stu-id="bea6f-114">where:</span></span>

- <span data-ttu-id="bea6f-115">*your_package_file*：控件文件的名称，例如 `ManagedPackage.winmd`（“ManagedPackage”是本示例中随意起的名称，没有其他意义）。</span><span class="sxs-lookup"><span data-stu-id="bea6f-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="bea6f-116">*vs_category*：Visual Studio 设计器工具箱中应出现控件的组的标签。</span><span class="sxs-lookup"><span data-stu-id="bea6f-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="bea6f-117">`VSCategory` 对控件出现在工具箱中是必要的。</span><span class="sxs-lookup"><span data-stu-id="bea6f-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="bea6f-118">*blend_category*：Blend 设计器的“资产”窗格中应出现控件的组的标签。</span><span class="sxs-lookup"><span data-stu-id="bea6f-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="bea6f-119">`BlendCategory` 对控件出现在“资产”中是必要的。</span><span class="sxs-lookup"><span data-stu-id="bea6f-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="bea6f-120">*type_full_name_n*：每个控件的完全限定名称，包括命名空间，例如 `ManagedPackage.MyCustomControl`。</span><span class="sxs-lookup"><span data-stu-id="bea6f-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="bea6f-121">注意，点格式用于托管和本机类型。</span><span class="sxs-lookup"><span data-stu-id="bea6f-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="bea6f-122">在更高级的方案中，当单个包包含多个控件程序集时，还可以在 `<FileList>` 中包括多个 `<File>` 元素。</span><span class="sxs-lookup"><span data-stu-id="bea6f-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="bea6f-123">如果需要将控件整理为单独的分类，则还可以在单个 `<File>` 中有多个 `<ToolboxItems>` 节点。</span><span class="sxs-lookup"><span data-stu-id="bea6f-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="bea6f-124">在以下示例中，`ManagedPackage.winmd` 中实现的控件将出现在 Visual Studio 和 Blend 名为“托管包”的组中，“MyCustomControl”将出现在该组中。</span><span class="sxs-lookup"><span data-stu-id="bea6f-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="bea6f-125">所有名称都是随意起的。</span><span class="sxs-lookup"><span data-stu-id="bea6f-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![出现在 Visual Studio 中的示例控件](media/UWP-control-vs-toolbox.png)

![出现在 Blend 中的示例控件](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="bea6f-128">必须显式指定每个需要在工具箱/资产窗格中看见的控件。</span><span class="sxs-lookup"><span data-stu-id="bea6f-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="bea6f-129">请确保以 `Namespace.ControlName` 格式指定它们。</span><span class="sxs-lookup"><span data-stu-id="bea6f-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="bea6f-130">将自定义图标添加到控件</span><span class="sxs-lookup"><span data-stu-id="bea6f-130">Add custom icons to your controls</span></span>

<span data-ttu-id="bea6f-131">要在工具箱/资产窗格中显示自定义图标，请将图像添加到项目或名为“Namespace.ControlName.extension”的对应 `design.dll` 项目，并将生成操作设为“嵌入资源”。</span><span class="sxs-lookup"><span data-stu-id="bea6f-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="bea6f-132">支持的格式为 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。</span><span class="sxs-lookup"><span data-stu-id="bea6f-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="bea6f-133">建议图像大小为 64 像素乘 64 像素。</span><span class="sxs-lookup"><span data-stu-id="bea6f-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="bea6f-134">在以下示例中，项目包含名为“ManagedPackage.MyCustomControl.png”的图像文件。</span><span class="sxs-lookup"><span data-stu-id="bea6f-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![在项目中设置自定义图标](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="bea6f-136">对于本机控件，必须将图标以资源的形式放在 `design.dll` 项目中。</span><span class="sxs-lookup"><span data-stu-id="bea6f-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="bea6f-137">支持特定 Windows 平台版本</span><span class="sxs-lookup"><span data-stu-id="bea6f-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="bea6f-138">UWP 包有 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV)，定义了可以安装应用的 OS 版本的上限和下线。</span><span class="sxs-lookup"><span data-stu-id="bea6f-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="bea6f-139">TPV 进一步指定生成应用的 SDK 的版本。</span><span class="sxs-lookup"><span data-stu-id="bea6f-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="bea6f-140">创作 UWP 包时注意这些属性：使用应用定义的平台版本界限意外的 API 将导致生成失败或应用在运行时失败。</span><span class="sxs-lookup"><span data-stu-id="bea6f-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="bea6f-141">例如，假如已将控件包的 TPMinV 设为 Windows 10 Anniversary Edition（10.0；版本 14393），因此需要确保仅与下限相匹配的 UWP 项目使用此包。</span><span class="sxs-lookup"><span data-stu-id="bea6f-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="bea6f-142">要使得包被 UWP 项目使用，你必须使用以下文件夹名称打包控件：</span><span class="sxs-lookup"><span data-stu-id="bea6f-142">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="bea6f-143">要强制实施正确的 TPMinV 检查，请创建一个 [MSBuild 目标文件](/visualstudio/msbuild/msbuild-targets)并在 `build\uap10.0` 文件夹下将其打包为 `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `，使用特定程序集名称替换 `your_assembly_name`。</span><span class="sxs-lookup"><span data-stu-id="bea6f-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="bea6f-144">目标文件应如此处示例所示：</span><span class="sxs-lookup"><span data-stu-id="bea6f-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="bea6f-145">添加设计时支持</span><span class="sxs-lookup"><span data-stu-id="bea6f-145">Add design-time support</span></span>

<span data-ttu-id="bea6f-146">要配置控件属性在属性检查器中显示的位置、添加自定义装饰器等，请将 `design.dll` 文件放在目标平台对应的 `lib\uap10.0\Design` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bea6f-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="bea6f-147">此外，要确保[“编辑模板”>“编辑副本”](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)功能正常工作，必须包含 `Generic.xaml` 及其在 `<your_assembly_name>\Themes` 文件夹中合并的任何资源字典（同样，使用实际的程序集名称）。</span><span class="sxs-lookup"><span data-stu-id="bea6f-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="bea6f-148">（此文件对控件的运行时行为不产生影响。）文件夹结构将如下所示：</span><span class="sxs-lookup"><span data-stu-id="bea6f-148">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="bea6f-149">默认情况下，控件属性将显示在属性检查器的“杂项”类别下。</span><span class="sxs-lookup"><span data-stu-id="bea6f-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="bea6f-150">使用字符串和资源</span><span class="sxs-lookup"><span data-stu-id="bea6f-150">Use strings and resources</span></span>

<span data-ttu-id="bea6f-151">可以将字符创资源 (`.resw`) 嵌入在控件或者使用的 UWP 项目可使用的包中，将 `.resw` 文件的“生成操作”属性设为 PRIResource。</span><span class="sxs-lookup"><span data-stu-id="bea6f-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="bea6f-152">有关示例，请参考 ExtensionSDKasNuGetPackage 示例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。</span><span class="sxs-lookup"><span data-stu-id="bea6f-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="bea6f-153">打包图像等内容</span><span class="sxs-lookup"><span data-stu-id="bea6f-153">Package content such as images</span></span>

<span data-ttu-id="bea6f-154">若要打包图像等可由控件或使用的 UWP 项目使用的内容，请将这些文件放在 `lib\uap10.0` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bea6f-154">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="bea6f-155">可能还要创作 [MSBuild 目标文件](/visualstudio/msbuild/msbuild-targets)，确保资产复制到使用的项目的输出文件夹：</span><span class="sxs-lookup"><span data-stu-id="bea6f-155">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="bea6f-156">请参阅</span><span class="sxs-lookup"><span data-stu-id="bea6f-156">See also</span></span>

- [<span data-ttu-id="bea6f-157">创建 UWP 包</span><span class="sxs-lookup"><span data-stu-id="bea6f-157">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="bea6f-158">ExtensionSDKasNuGetPackage 示例</span><span class="sxs-lookup"><span data-stu-id="bea6f-158">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
