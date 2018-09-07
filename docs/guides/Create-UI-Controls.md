---
title: 如何使用 NuGet 打包 UI 控件
description: 如何创建包含 UWP 或 WPF 控件的 NuGet 包，包括必要的元数据和 Visual Studio 和 Blend 设计器的支持文件。
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ce5ad07209a06010150b14092aa1b15ee6f84146
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548733"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>以 NuGet 包形式创建 UI 控件

通过 Visual Studio 2017，可以利用在 NuGet 包中提供的 UWP 和 WPF 控件新增功能。 本指南使用 [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)来演练 UWP 控件上下文中的这些功能。 这同样适用于 WPF 控件，除非另行指定。

## <a name="prerequisites"></a>系统必备

1. Visual Studio 2017
1. 了解如何[创建 UWP 包](create-uwp-packages.md)

## <a name="generate-library-layout"></a>生成库布局

> [!Note]
> 这仅适用于 UWP 控件。

设置 `GenerateLibraryLayout` 属性可确保项目生成输出在已准备好打包的布局中生成，而无需 nuspec 中的单独文件项。

在项目属性中，转到“生成”选项卡并选中“生成库布局”复选框。 这将修改项目文件，并针对当前所选的生成配置和平台将 `GenerateLibraryLayout` 标志设置为“true”。

或者，编辑项目文件以将 `<GenerateLibraryLayout>true</GenerateLibraryLayout>` 添加到第一个无条件属性组。 无论生成配置和平台如何，这都将应用该属性。

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>添加对 XAML 控件的工具箱/资产窗格支持

要使 XAML 控件出现在 Visual Studio 中的 XAML 设计器工具箱和 Blend 的“资产”窗格中，请在包项目的 `tools` 文件夹根中创建 `VisualStudioToolsManifest.xml` 文件。 如果不需要控件显示在工具箱或“资产”窗格中，则不需要此文件。

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

文件的结构如下所示：

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

其中：

- *your_package_file*：控件文件的名称，例如 `ManagedPackage.winmd`（“ManagedPackage”是本示例中随意起的名称，没有其他意义）。
- *vs_category*：Visual Studio 设计器工具箱中应出现控件的组的标签。 `VSCategory` 对控件出现在工具箱中是必要的。
- *blend_category*：Blend 设计器的“资产”窗格中应出现控件的组的标签。 `BlendCategory` 对控件出现在“资产”中是必要的。
- *type_full_name_n*：每个控件的完全限定名称，包括命名空间，例如 `ManagedPackage.MyCustomControl`。 注意，点格式用于托管和本机类型。

在更高级的方案中，当单个包包含多个控件程序集时，还可以在 `<FileList>` 中包括多个 `<File>` 元素。 如果需要将控件整理为单独的分类，则还可以在单个 `<File>` 中有多个 `<ToolboxItems>` 节点。

在以下示例中，`ManagedPackage.winmd` 中实现的控件将出现在 Visual Studio 和 Blend 名为“托管包”的组中，“MyCustomControl”将出现在该组中。 所有名称都是随意起的。

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
> 必须显式指定每个需要在工具箱/资产窗格中看见的控件。 请确保以 `Namespace.ControlName` 格式指定它们。

## <a name="add-custom-icons-to-your-controls"></a>将自定义图标添加到控件

要在工具箱/资产窗格中显示自定义图标，请将图像添加到项目或名为“Namespace.ControlName.extension”的对应 `design.dll` 项目，并将生成操作设为“嵌入资源”。 支持的格式为 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。 建议图像大小为 64 像素乘 64 像素。

在以下示例中，项目包含名为“ManagedPackage.MyCustomControl.png”的图像文件。

![在项目中设置自定义图标](media/UWP-control-custom-icon.png)

> [!Note]
> 对于本机控件，必须将图标以资源的形式放在 `design.dll` 项目中。

## <a name="support-specific-windows-platform-versions"></a>支持特定 Windows 平台版本

UWP 包有 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV)，定义了可以安装应用的 OS 版本的上限和下线。 TPV 进一步指定生成应用的 SDK 的版本。 创作 UWP 包时注意这些属性：使用应用定义的平台版本界限意外的 API 将导致生成失败或应用在运行时失败。

例如，假如已将控件包的 TPMinV 设为 Windows 10 Anniversary Edition（10.0；版本 14393），因此需要确保仅与下限相匹配的 UWP 项目使用此包。 要使得包被 UWP 项目使用，你必须使用以下文件夹名称打包控件：

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet 将自动检查正在使用项目的 TPMinV，如果低于 Windows 10 Anniversary Edition（10.0；版本 14393），则安装失败

在 WPF 中，我们假设你希望 WPF 控件包由面向 .NET Framework v4.6.1 或更高版本的项目使用。 若要强制执行此操作，必须使用以下文件夹名称来打包控件：

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>添加设计时支持

要配置控件属性在属性检查器中显示的位置、添加自定义装饰器等，请将 `design.dll` 文件放在目标平台对应的 `lib\uap10.0.14393\Design` 文件夹中。 此外，要确保[“编辑模板”>“编辑副本”](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)功能正常工作，必须包含 `Generic.xaml` 及其在 `<your_assembly_name>\Themes` 文件夹中合并的任何资源字典（同样，使用实际的程序集名称）。 （此文件对控件的运行时行为不产生影响。）文件夹结构将如下所示：

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


对于 WPF，请继续上述示例，即希望由面向 .NET Framework v4.6.1 或更高版本的项目来使用 WPF 控件包：

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> 默认情况下，控件属性将显示在属性检查器的“杂项”类别下。

## <a name="use-strings-and-resources"></a>使用字符串和资源

可以将字符创资源 (`.resw`) 嵌入在控件或者使用的 UWP 项目可使用的包中，将 `.resw` 文件的“生成操作”属性设为 PRIResource。

有关示例，请参考 ExtensionSDKasNuGetPackage 示例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。

> [!Note]
> 这仅适用于 UWP 控件。

## <a name="see-also"></a>请参阅

- [创建 UWP 包](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
