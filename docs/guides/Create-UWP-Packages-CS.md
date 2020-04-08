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
# <a name="create-uwp-packages-c"></a>创建 UWP 包 (C#)

[通用 Windows 平台 (UWP)](/windows/uwp) 为运行 Windows 10 的每台设备提供了一个通用应用平台。 在此模型中，UWP 应用可以调用所有设备通用的 WinRT API，以及特定于运行该应用的设备系列的 API（包括 Win32 和 .NET）。

在本演练中，将创建一个具有 C# UWP 组件（包括 XAML 控件）的 NuGet 包，以便在托管项目和本机项目中使用。

## <a name="prerequisites"></a>必备条件

1. Visual Studio 2019。 可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版；也可以使用 Professional 和 Enterprise 版。

1. NuGet CLI。 从 `nuget.exe`nuget.org/downloads[ 下载 ](https://nuget.org/downloads) 的最新版本，将其保存到选择的位置（`.exe` 是直接下载的）。 然后将该位置添加到 PATH 环境变量（如果尚未添加）。 [更多详细信息](/nuget/reference/nuget-exe-cli-reference#windows)。

## <a name="create-a-uwp-windows-runtime-component"></a>创建 UWP Windows 运行时组件

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，搜索“uwp c#”，然后选择“Windows 运行时组件(通用 Windows)”模板，单击“下一步”，将名称更改为 ImageEnhancer，然后单击“创建”   。 出现提示时，接受“目标版本”和“最低版本”的默认值。

    ![创建新的 UWP Windows 运行时组件项目](media/UWP-NewProject-CS.png)

1. 右键单击“解决方案资源管理器”中的项目，选择“添加”>“新建项目”，选择“模板控制”，将名称改为 AwesomeImageControl.cs，然后单击“添加”    ：

    ![将新的 XAML 模板化控件项添加到项目](media/UWP-NewXAMLControl-CS.png)

1. 右键单击“解决方案资源管理器”中的项目，然后选择“属性”  在“属性”页面上，选择“生成”选项卡并启用“XML 文档文件”   ：

    ![将“生成 XML 文档文件”的值设置为“Yes”](media/UWP-GenerateXMLDocFiles-CS.png)

1. 右键单击“解决方案”，选择“批生成”，选中对话框中的五个生成框，如下所示   。 这样可确保在生成时，将为 Windows 支持的每个目标系统生成一套完整的项目。

    ![批生成](media/UWP-BatchBuild-CS.png)

1. 在“批生成”对话框中，单击“生成”，验证项目并创建 NuGet 包所需的输出文件  。

> [!Note]
> 在本演练中，将使用包的 Debug 项目。 对于非调试包，请选中“批量生成”对话框中的 Release 选项，然后在以下步骤中引用生成的 Release 文件夹。

## <a name="create-and-update-the-nuspec-file"></a>创建并更新 .nuspec 文件

若要创建初始 `.nuspec` 文件，请执行以下三个步骤。 后续部分将引导你完成其他必要的更新。

1. 打开命令提示符并导航到包含 `ImageEnhancer.csproj` 的文件夹（这将是解决方案文件下方的子文件夹）。
1. 运行 [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) 命令生成 `ImageEnhancer.nuspec`（此文件的名称取自 `.csroj` 文件的名称）：

    ```cli
    nuget spec
    ```

1. 在编辑器中打开 `ImageEnhancer.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。 $propertyName$ 值均不得留空。 具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。 另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。

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
> 对于供公共使用而生成的包，请特别注意 `<tags>` 元素，因为这些标记可帮助其他人查找包并了解其用途。

### <a name="adding-windows-metadata-to-the-package"></a>将 Windows 元数据添加到包

Windows 运行时组件需要描述其所有公共可用类型的元数据，这使得其他应用和库可使用该组件。 该元数据包含在 .winmd 文件中，此文件在编译项目时创建，并且必须包含在 NuGet 包中。 同时还生成具有 IntelliSense 数据的 XML 文件，并且应该包含在内。

将以下 `<files>` 节点添加到 `.nuspec` 文件：

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

### <a name="adding-xaml-content"></a>添加 XAML 内容

若要在组件中包含 XAML 控件，需要添加具有默认控件模板的 XAML 文件（由项目模板生成）。 这也将进入 `<files>` 部分：

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

### <a name="adding-the-native-implementation-libraries"></a>添加本机实现库

在组件中，ImageEnhancer 类型的核心逻辑是本机代码，包含在针对每个目标运行时（ARM、ARM64、x86 和 x64）生成的各种 `ImageEnhancer.winmd` 程序集中。 若要在包中包含这些文件，请在 `<files>` 部分中引用它们及其关联的 .pri 资源文件：

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

### <a name="final-nuspec"></a>最终 .nuspec

现在，最终 `.nuspec` 文件应该如下所示，其中应再次将 YOUR_NAME 替换为适当的值：

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

## <a name="package-the-component"></a>打包组件

如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) 命令：

```cli
nuget pack ImageEnhancer.nuspec
```

这将生成 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。 在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容：

![显示 ImageEnhancer 包的 NuGet 包资源管理器](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。 然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。

若要使你的包可供其他开发人员使用，请按照[发布包](../nuget-org/publish-a-package.md)中的说明进行操作。

## <a name="related-topics"></a>相关主题

- [.nuspec 引用](../reference/nuspec.md)
- [符号包](../create-packages/symbol-packages-snupkg.md)
- [包版本控制](../concepts/package-versioning.md)
- [支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [创建本地化包](../create-packages/creating-localized-packages.md)
