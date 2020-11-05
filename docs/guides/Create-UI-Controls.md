---
title: 如何使用 NuGet 打包 UI 控件
description: 如何创建包含 UWP 或 WPF 控件的 NuGet 包，包括必要的元数据和 Visual Studio 和 Blend 设计器的支持文件。
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 17062d83349fe1b8cd28e57dd888686a226ac9cb
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238018"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="335f6-103">以 NuGet 包形式创建 UI 控件</span><span class="sxs-lookup"><span data-stu-id="335f6-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="335f6-104">从 Visual Studio 2017 开始，可以利用在 NuGet 包中提供的 UWP 和 WPF 控件的附加功能。</span><span class="sxs-lookup"><span data-stu-id="335f6-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="335f6-105">本指南使用 [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)来演练 UWP 控件上下文中的这些功能。</span><span class="sxs-lookup"><span data-stu-id="335f6-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="335f6-106">这同样适用于 WPF 控件，除非另行指定。</span><span class="sxs-lookup"><span data-stu-id="335f6-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="335f6-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="335f6-107">Prerequisites</span></span>

1. <span data-ttu-id="335f6-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="335f6-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="335f6-109">了解如何[创建 UWP 包](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="335f6-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="335f6-110">生成库布局</span><span class="sxs-lookup"><span data-stu-id="335f6-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="335f6-111">这仅适用于 UWP 控件。</span><span class="sxs-lookup"><span data-stu-id="335f6-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="335f6-112">设置 `GenerateLibraryLayout` 属性可确保项目生成输出在已准备好打包的布局中生成，而无需 nuspec 中的单独文件项。</span><span class="sxs-lookup"><span data-stu-id="335f6-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="335f6-113">在项目属性中，转到“生成”选项卡并选中“生成库布局”复选框。</span><span class="sxs-lookup"><span data-stu-id="335f6-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="335f6-114">这将修改项目文件，并针对当前所选的生成配置和平台将 `GenerateLibraryLayout` 标志设置为“true”。</span><span class="sxs-lookup"><span data-stu-id="335f6-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="335f6-115">或者，编辑项目文件以将 `<GenerateLibraryLayout>true</GenerateLibraryLayout>` 添加到第一个无条件属性组。</span><span class="sxs-lookup"><span data-stu-id="335f6-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="335f6-116">无论生成配置和平台如何，这都将应用该属性。</span><span class="sxs-lookup"><span data-stu-id="335f6-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="335f6-117">添加对 XAML 控件的工具箱/资产窗格支持</span><span class="sxs-lookup"><span data-stu-id="335f6-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="335f6-118">要使 XAML 控件出现在 Visual Studio 中的 XAML 设计器工具箱和 Blend 的“资产”窗格中，请在包项目的 `tools` 文件夹根中创建 `VisualStudioToolsManifest.xml` 文件。</span><span class="sxs-lookup"><span data-stu-id="335f6-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="335f6-119">如果不需要控件显示在工具箱或“资产”窗格中，则不需要此文件。</span><span class="sxs-lookup"><span data-stu-id="335f6-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="335f6-120">文件的结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="335f6-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="335f6-121">其中：</span><span class="sxs-lookup"><span data-stu-id="335f6-121">where:</span></span>

- <span data-ttu-id="335f6-122">*your_package_file* ：控件文件的名称，例如 `ManagedPackage.winmd`（“ManagedPackage”是本示例中随意起的名称，没有其他意义）。</span><span class="sxs-lookup"><span data-stu-id="335f6-122">*your_package_file* : the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="335f6-123">*vs_category* ：Visual Studio 设计器工具箱中应出现控件的组的标签。</span><span class="sxs-lookup"><span data-stu-id="335f6-123">*vs_category* : The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="335f6-124">`VSCategory` 对控件出现在工具箱中是必要的。</span><span class="sxs-lookup"><span data-stu-id="335f6-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="335f6-125">*ui_framework* ：框架的名称（例如“WPF”），请注意，Visual Studio 16.7 预览版 3 或更高版本的 ToolboxItems 节点上必须具有 `UIFramework` 属性，控件才能出现在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="335f6-125">*ui_framework* : The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="335f6-126">*blend_category* ：Blend 设计器的“资产”窗格中应出现控件的组的标签。</span><span class="sxs-lookup"><span data-stu-id="335f6-126">*blend_category* : The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="335f6-127">`BlendCategory` 对控件出现在“资产”中是必要的。</span><span class="sxs-lookup"><span data-stu-id="335f6-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="335f6-128">*type_full_name_n* ：每个控件的完全限定名称，包括命名空间，例如 `ManagedPackage.MyCustomControl`。</span><span class="sxs-lookup"><span data-stu-id="335f6-128">*type_full_name_n* : The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="335f6-129">注意，点格式用于托管和本机类型。</span><span class="sxs-lookup"><span data-stu-id="335f6-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="335f6-130">在更高级的方案中，当单个包包含多个控件程序集时，还可以在 `<FileList>` 中包括多个 `<File>` 元素。</span><span class="sxs-lookup"><span data-stu-id="335f6-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="335f6-131">如果需要将控件整理为单独的分类，则还可以在单个 `<File>` 中有多个 `<ToolboxItems>` 节点。</span><span class="sxs-lookup"><span data-stu-id="335f6-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="335f6-132">在以下示例中，`ManagedPackage.winmd` 中实现的控件将出现在 Visual Studio 和 Blend 名为“托管包”的组中，“MyCustomControl”将出现在该组中。</span><span class="sxs-lookup"><span data-stu-id="335f6-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="335f6-133">所有名称都是随意起的。</span><span class="sxs-lookup"><span data-stu-id="335f6-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![出现在 Visual Studio 中的示例控件](media/UWP-control-vs-toolbox.png)

![出现在 Blend 中的示例控件](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="335f6-136">必须显式指定每个需要在工具箱/资产窗格中看见的控件。</span><span class="sxs-lookup"><span data-stu-id="335f6-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="335f6-137">请确保以 `Namespace.ControlName` 格式指定它们。</span><span class="sxs-lookup"><span data-stu-id="335f6-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="335f6-138">将自定义图标添加到控件</span><span class="sxs-lookup"><span data-stu-id="335f6-138">Add custom icons to your controls</span></span>

<span data-ttu-id="335f6-139">要在工具箱/资产窗格中显示自定义图标，请将图像添加到项目或名为“Namespace.ControlName.extension”的对应 `design.dll` 项目，并将生成操作设为“嵌入资源”。</span><span class="sxs-lookup"><span data-stu-id="335f6-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="335f6-140">还必须确保关联的 `AssemblyInfo.cs` 指定 ProvideMetadata 属性 - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`。</span><span class="sxs-lookup"><span data-stu-id="335f6-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="335f6-141">请参阅此[示例](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)。</span><span class="sxs-lookup"><span data-stu-id="335f6-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="335f6-142">支持的格式为 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。</span><span class="sxs-lookup"><span data-stu-id="335f6-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="335f6-143">推荐格式为 16 x 16 像素 BMP24。</span><span class="sxs-lookup"><span data-stu-id="335f6-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![工具框图标示例](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="335f6-145">运行时将替换粉色背景。</span><span class="sxs-lookup"><span data-stu-id="335f6-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="335f6-146">更改 Visual Studio 主题且需要设置背景颜色时，图标会重新着色。</span><span class="sxs-lookup"><span data-stu-id="335f6-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="335f6-147">有关详细信息，请参阅 [Visual Studio 的图像和图标](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="335f6-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="335f6-148">在以下示例中，项目包含名为“ManagedPackage.MyCustomControl.png”的图像文件。</span><span class="sxs-lookup"><span data-stu-id="335f6-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![在项目中设置自定义图标](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="335f6-150">对于本机控件，必须将图标以资源的形式放在 `design.dll` 项目中。</span><span class="sxs-lookup"><span data-stu-id="335f6-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="335f6-151">支持特定 Windows 平台版本</span><span class="sxs-lookup"><span data-stu-id="335f6-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="335f6-152">UWP 包有 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV)，定义了可以安装应用的 OS 版本的上限和下线。</span><span class="sxs-lookup"><span data-stu-id="335f6-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="335f6-153">TPV 进一步指定生成应用的 SDK 的版本。</span><span class="sxs-lookup"><span data-stu-id="335f6-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="335f6-154">创作 UWP 包时注意这些属性：使用应用定义的平台版本界限意外的 API 将导致生成失败或应用在运行时失败。</span><span class="sxs-lookup"><span data-stu-id="335f6-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="335f6-155">例如，假如已将控件包的 TPMinV 设为 Windows 10 Anniversary Edition（10.0；版本 14393），因此需要确保仅与下限相匹配的 UWP 项目使用此包。</span><span class="sxs-lookup"><span data-stu-id="335f6-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="335f6-156">要使得包被 UWP 项目使用，你必须使用以下文件夹名称打包控件：</span><span class="sxs-lookup"><span data-stu-id="335f6-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="335f6-157">NuGet 将自动检查正在使用项目的 TPMinV，如果低于 Windows 10 Anniversary Edition（10.0；版本 14393），则安装失败</span><span class="sxs-lookup"><span data-stu-id="335f6-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="335f6-158">在 WPF 中，我们假设你希望 WPF 控件包由面向 .NET Framework v4.6.1 或更高版本的项目使用。</span><span class="sxs-lookup"><span data-stu-id="335f6-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="335f6-159">若要强制执行此操作，必须使用以下文件夹名称来打包控件：</span><span class="sxs-lookup"><span data-stu-id="335f6-159">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="335f6-160">添加设计时支持</span><span class="sxs-lookup"><span data-stu-id="335f6-160">Add design-time support</span></span>

<span data-ttu-id="335f6-161">要配置控件属性在属性检查器中显示的位置、添加自定义装饰器等，请将 `design.dll` 文件放在目标平台对应的 `lib\uap10.0.14393\Design` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="335f6-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="335f6-162">此外，要确保[“编辑模板”>“编辑副本”](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)功能正常工作，必须包含 `Generic.xaml` 及其在 `<your_assembly_name>\Themes` 文件夹中合并的任何资源字典（同样，使用实际的程序集名称）。</span><span class="sxs-lookup"><span data-stu-id="335f6-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="335f6-163">（此文件对控件的运行时行为不产生影响。）文件夹结构将如下所示：</span><span class="sxs-lookup"><span data-stu-id="335f6-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="335f6-164">对于 WPF，请继续上述示例，即希望由面向 .NET Framework v4.6.1 或更高版本的项目来使用 WPF 控件包：</span><span class="sxs-lookup"><span data-stu-id="335f6-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="335f6-165">默认情况下，控件属性将显示在属性检查器的“杂项”类别下。</span><span class="sxs-lookup"><span data-stu-id="335f6-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="335f6-166">使用字符串和资源</span><span class="sxs-lookup"><span data-stu-id="335f6-166">Use strings and resources</span></span>

<span data-ttu-id="335f6-167">可以将字符创资源 (`.resw`) 嵌入在控件或者使用的 UWP 项目可使用的包中，将 `.resw` 文件的“生成操作”属性设为 PRIResource。</span><span class="sxs-lookup"><span data-stu-id="335f6-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="335f6-168">有关示例，请参考 ExtensionSDKasNuGetPackage 示例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。</span><span class="sxs-lookup"><span data-stu-id="335f6-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="335f6-169">这仅适用于 UWP 控件。</span><span class="sxs-lookup"><span data-stu-id="335f6-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="335f6-170">另请参阅</span><span class="sxs-lookup"><span data-stu-id="335f6-170">See also</span></span>

- [<span data-ttu-id="335f6-171">创建 UWP 包</span><span class="sxs-lookup"><span data-stu-id="335f6-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="335f6-172">ExtensionSDKasNuGetPackage 示例</span><span class="sxs-lookup"><span data-stu-id="335f6-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)