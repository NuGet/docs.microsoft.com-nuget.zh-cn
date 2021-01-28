---
title: 创建适用于通用 Windows 平台的 NuGet 包
description: 从头到尾演练如何使用适用于通用 Windows 平台的 Windows 运行时组件创建 NuGet 包。
author: JonDouglas
ms.author: jodou
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c077645508cb10e86b3ed1e1f2bf61adcd2013d9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774231"
---
# <a name="create-uwp-packages"></a>创建 UWP 包

[通用 Windows 平台 (UWP)](https://developer.microsoft.com/windows) 为运行 Windows 10 的每台设备提供了一个通用应用平台。 在此模型中，UWP 应用可以调用所有设备通用的 WinRT API，以及特定于运行该应用的设备系列的 API（包括 Win32 和 .NET）。

在本演练中，将创建一个具有本机 UWP 组件（包括 XAML 控件）的 NuGet 包，以便在托管项目和本机项目中使用。

## <a name="prerequisites"></a>先决条件

1. Visual Studio 2017 或 Visual Studio 2015。 可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2017 Community 版；也可以使用 Professional 和 Enterprise 版。

1. NuGet CLI。 从 [nuget.org/downloads](https://nuget.org/downloads) 下载 `nuget.exe` 的最新版本，将其保存到选择的位置（`.exe` 是直接下载的）。 然后将该位置添加到 PATH 环境变量（如果尚未添加）。

## <a name="create-a-uwp-windows-runtime-component"></a>创建 UWP Windows 运行时组件

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C++”>“Windows”>“Universal”节点，选择“Windows 运行时组件(通用 Windows)”，将名称更改为“ImageEnhancer”，然后单击“确定”    。 出现提示时，接受“目标版本”和“最低版本”的默认值。

    ![创建新的 UWP Windows 运行时组件项目](media/UWP-NewProject.png)

1. 右键单击“解决方案资源管理器”中的项目，选择“添加”>“新建项目”，单击“Visual C++”>“XAML”节点，选择“模板控制”，将名称更改为“AwesomeImageControl.cpp”，然后单击“添加”     ：

    ![将新的 XAML 模板化控件项添加到项目](media/UWP-NewXAMLControl.png)

1. 右键单击“解决方案资源管理器”中的项目，然后选择“属性”  在“属性”页中，展开“配置属性”>“C/C++”，然后单击“输出文件”   。 在右侧窗格中，将“生成 XML 文档文件”的值更改为“Yes”  ：

    ![将“生成 XML 文档文件”的值设置为“Yes”](media/UWP-GenerateXMLDocFiles.png)

1. 现在，右键单击“解决方案”，选择“批生成”，选中对话框中的三个 Debug 框，如下所示   。 这样可确保在生成时，将为 Windows 支持的每个目标系统生成一套完整的项目。

    ![批生成](media/UWP-BatchBuild.png)

1. 在“批生成”对话框中，单击“生成”，验证项目并创建 NuGet 包所需的输出文件  。

> [!Note]
> 在本演练中，将使用包的 Debug 项目。 对于非调试包，请选中“批量生成”对话框中的 Release 选项，然后在以下步骤中引用生成的 Release 文件夹。

## <a name="create-and-update-the-nuspec-file"></a>创建并更新 .nuspec 文件

若要创建初始 `.nuspec` 文件，请执行以下三个步骤。 后续部分将引导你完成其他必要的更新。

1. 打开命令提示符并导航到包含 `ImageEnhancer.vcxproj` 的文件夹（这将是解决方案文件下方的子文件夹）。
1. 运行 NuGet `spec` 命令生成 `ImageEnhancer.nuspec`（文件的名称取自 `.vcxproj` 文件的名称）：

    ```cli
    nuget spec
    ```

1. 在编辑器中打开 `ImageEnhancer.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。 具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。 另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。

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
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
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

在组件中，ImageEnhancer 类型的核心逻辑是本机代码，包含在针对每个目标运行时（ARM、x86 和 x64）生成的各种 `ImageEnhancer.dll` 程序集中。 若要在包中包含这些文件，请在 `<files>` 部分中引用它们及其关联的 .pri 资源文件：

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

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>添加 .targets

接下来，可能使用 NuGet 包的 C++ 和 JavaScript 项目需要一个 .targets 文件来标识必要的程序集和 winmd 文件。 （C# 和 Visual Basic 项目自动执行此操作。）通过将下方文本复制到 `ImageEnhancer.targets` 创建此文件，并将其保存在与 `.nuspec` 文件相同的文件夹中。 _说明_：此 `.targets` 文件需要与包 ID（例如 `.nupspec` 文件中的 `<Id>` 元素）名称相同：

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

然后在 `.nuspec` 文件中引用 `ImageEnhancer.targets`：

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
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>打包组件

如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：

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
