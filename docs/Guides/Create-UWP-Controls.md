---
title: "如何使用 NuGet 打包 UWP 控件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "如何创建包含 UWP 控件的 NuGet 包，包括必要的元数据和 Visual Studio 和 Blend 设计器的支持文件。"
keywords: "NuGet UWP 控件, Visual Studio XAML 设计器, Blend 设计器, 自定义控件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>以 NuGet 包形式创建 UWP 控件

通过 Visual Studio 2017，可以利用在 NuGet 包中提供的 UWP 控件新增功能。 本指南使用 [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)来演练这些功能。 

## <a name="pre-requisites"></a>先决条件：

1.  Visual Studio 2017
1.  了解如何[创建 UWP 包](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>添加对 XAML 控件的工具箱/资产窗格支持

要使 XAML 控件出现在 Visual Studio 中的 XAML 设计器工具箱和 Blend 的“资产”窗格中，请在包项目的 `tools` 文件夹根中创建 `VisualStudioToolsManifest.xml` 文件。 如果不需要控件显示在工具箱或“资产”窗格中，则不需要此文件。

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

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

例如，假如已将控件包的 TPMinV 设为 Windows 10 Anniversary Edition（10.0；版本 14393），因此需要确保仅与下限相匹配的 UWP 项目使用此包。 要使得包被基于 `project.json` 的 UWP 项目使用，则必须使用以下文件夹名称打包控件：

```
\lib\uap10.0\*
\ref\uap10.0\*
```

要强制实施正确的 TPMinV check，请创建一个 [MSBuild 目标文件](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)并将其打包在生成文件夹下（使用特定程序集名称替换“your_assembly_name”）：

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

目标文件应如此处示例所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>添加设计时支持

要配置控件属性在属性检查器中显示的位置、添加自定义装饰器等，请将 `design.dll` 文件放在目标平台对应的 `lib\<platform>\Design` 文件夹中。 此外，要确保[“编辑模板”>“编辑副本”](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)功能正常工作，必须包含 `Generic.xaml` 及其在 `<AssemblyName>\Themes` 文件夹中合并的资源字典。 （此文件对控件的运行时行为不产生影响。）


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> 默认情况下，控件属性将显示在属性检查器的“杂项”类别下。


## <a name="use-strings-and-resources"></a>使用字符串和资源

可以将字符创资源 (`.resw`) 嵌入在控件或者使用的 UWP 项目可使用的包中，将 `.resw` 文件的“生成操作”属性设为 PRIResource。

有关示例，请参考 ExtensionSDKasNuGetPackage 示例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。

## <a name="package-content-such-as-images"></a>打包图像等内容

打包图像等控件或使用的 UWP 项目可使用的内容。 如下所示添加这些文件 `lib\uap10.0.14393.0` 的文件夹（“your_assembly_name”应与特定控件相匹配）：

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

可能还要创作 [MSBuild 目标文件](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)确保资产复制到使用的项目的输出文件夹：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>请参阅

- [创建 UWP 包](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 示例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
