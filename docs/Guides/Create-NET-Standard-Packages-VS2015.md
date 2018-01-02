---
title: "使用 Visual Studio 2015 创建 .NET Standard NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "从头到尾介绍如何使用 NuGet 3.x 和 Visual Studio 2015 创建 .NET Standard NuGet 包。"
keywords: "创建包, .NET Standard 包, .NET Standard 映射表"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>使用 Visual Studio 2015 创建 .NET Standard 包

适用于 NuGet 3.x。有关使用 NuGet 4.x+ 的详细信息，请参阅[使用 Visual Studio 2017 创建 .NET Standard 包](../guides/create-net-standard-packages-vs2017.md)。

[.NET Standard 库](https://docs.microsoft.com/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。 .NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。 它使得开发人员可以生成跨所有 .NET 运行时可用的 PCL，并减少（如果不能消除）共享代码中平台特定的条件编译指令。

本指南将指导你创建一个面向 .NET Standard 库 1.4 的 nuget 包。 将在 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 上可用。 有关详细信息，请参阅本主题后面的 [.NET Standard 映射表](#net-standard-mapping-table)。

1. [先决条件](#pre-requisites)
1. [创建类库项目](#create-the-class-library-project)
1. [创建并更新 .nuspec 文件](#create-and-update-the-nuspec-file)
1. [打包组件](#package-the-component)
1. [附加选项](#additional-options)
1. [.NET Standard 映射表](#net-standard-mapping-table)
1. [相关主题](#related-topics)


## <a name="pre-requisites"></a>先决条件

1. Visual Studio 2015。 可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版；当然，也可以使用 Professional 和 Enterprise 版。
1. .NET Core：从 [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) 安装 .NET Core 以及适用于 Visual Studio 2015 的模板和其他工具。
1. NuGet CLI。 从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。 然后将该位置添加到 PATH 环境变量（如果尚未添加）。

> [!Note]
> nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。



## <a name="create-the-class-library-project"></a>创建类库项目

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C#”>“Windows”节点，选择“类库(可移植)”，将名称更改为“AppLogger”，然后单击“确定”。

    ![创建新类库项目](media/NetStandard-NewProject.png)

1. 在“添加可移植类库”对话框中，选择 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 选项。
1. 右键单击解决方案资源管理器中的 `AppLogger (Portable)`，选择“属性”，选择“库”选项卡，然后单击“目标”部分中的“目标 .NET 平台标准”。 这将提示进行确认，之后可从下拉列表中选择 `.NET Standard 1.4`：

    ![将目标设置为 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. 单击“生成”选项卡，将“配置”更改为 `Release`，然后选中“XML 文档文件”框。
1. 将代码添加到组件，例如：

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. 生成项目（使用 Release 配置）并检查 bin\Release 文件夹中是否生成了 DLL 和 XML 文件。

## <a name="create-and-update-the-nuspec-file"></a>创建并更新 .nuspec 文件

1. 打开命令提示符，导航到包含 `AppLogg.csproj` 文件夹的文件夹（`.sln` 文件的下一级），然后运行 NuGet `spec` 命令，创建初始 `AppLogger.nuspec` 文件：

```
nuget spec
```

1. 在编辑器中打开 `AppLogger.nuspec`，将其更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。 具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。 另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。

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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. 将引用程序集添加到 `.nuspec` 文件，也就是库的 DLL 和 IntelliSense XML 文件：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. 右键单击解决方案，选择“生成解决方案”，生成包的所有文件。


## <a name="package-the-component"></a>打包组件

如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：

```
nuget pack AppLogger.nuspec
```

将生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`。 在 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)（NuGet 包资源管理器）之类的工具中打开此文件，并展开所有节点，随即将看到以下内容：

![显示 AppLogger 包的 NuGet 包资源管理器](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。 然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。

若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。

请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。 在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。

## <a name="additional-options"></a>附加选项

以下部分介绍 NuGet 包创建的附加选项：

- [声明依赖项](#declaring-dependencies)
- [支持多个目标框架](#supporting-multiple-target-frameworks)
- [添加 MSBuild 的目标和属性](#adding-targets-and-props-for-msbuild)
- [创建本地化包](#creating-localized-packages)
- [添加自述文件](#adding-a-readme)

### <a name="declaring-dependencies"></a>声明依赖项

如果具有其他 NuGet 包的任何依赖项，请使用 `<group>` 元素在 `<dependencies>` 元素中列出这些依赖项。 例如，若要在 NewtonSoft.Json 8.0.3 或更高版本上声明依赖项，请添加以下内容：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

此处 version 特性的语法指示可接受版本 8.0.3 或更高版本。 若要指定不同的版本范围，请参阅[包版本控制](../reference/package-versioning.md)。

### <a name="supporting-multiple-target-frameworks"></a>支持多个目标框架

假设想要利用 .NET Framework 4.6.2 中 .NET Standard 1.4 不可用的 API。 若要执行此操作，首先需要使用条件编译或共享项目确保 .NET 4.6.2 的库编译。 （在 Visual Studio 中，可创建一个 NetCore 项目，将选择的框架添加到多个框架部分，然后生成。）然后使用基于约定的简单工作目录技术创建包，如下所示：

1. 在包含 `.nuspec` 文件的项目根文件夹中，创建一个名为 `lib` 的文件夹。
1. 在 `lib` 中，为想要支持的每个平台创建文件夹：

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. 在 `.nuspec` 文件中，在 `package` 节点下添加一个 `files` 节点，并使用通配符引用 `lib` 中的文件。 注意：基于约定的工作目录方法不支持令牌替换，因此请将其替换为文本值：

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.spec` 再次创建包。

有关使用此技术的详细信息，请参阅[支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>添加 MSBuild 的目标和属性

在某些情况下，可能需要在使用包的项目中添加自定义生成目标或属性，例如在生成过程中运行自定义工具或进程。 可通过在 `\build` 文件夹中添加文件来执行此操作，如以下步骤所述。 当 NuGet 使用 \build 文件夹安装包时，会在指向.targets 和 .props 文件的项目文件中添加 MSBuild 元素。

> [!Note]
> 使用 `project.json` 时，目标不添加到项目，而是通过 `project.lock.json` 提供。


1. 在包含 `.nuspec` 文件的项目文件夹中，创建一个名为 `build` 的文件夹。
1. 在 `build` 中，为支持的每个平台创建文件夹，并在这些文件夹中放置 `.targets` 和 `.props` 文件：

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. 在 `.nuspec` 文件中，在 `package` 节点下添加一个 `files` 节点，并使用通配符引用 `build` 中的文件。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.nuspec` 再次创建包。

有关更多详细信息，请参阅[将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)。


### <a name="creating-localized-packages"></a>创建本地化包

若要创建库的本地化版本，可为不同的区域设置创建单独的包，也可将本地化的资源程序集包含到一个包中。 以下是如何为德语和意大利语执行后一种方法的操作步骤：

1. 在 `lib` 下的每个目标框架文件夹中，为英语（默认）以外的每种受支持语言创建文件夹。 在这些文件夹中，可放置资源程序集和本地化的 IntelliSense XML 文件。 例如: 

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. 在 `.nuspec` 文件中，在 `<files>` 节点中引用这些文件：

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.nuspec` 再次创建包。


### <a name="adding-a-readme"></a>添加自述文件

在包的根目录中包含 `readme.txt` 文件时，Visual Studio 将在直接安装包时显示该文件。

> [!Note]
> 不会显示作为依赖项安装的包或 .NET Core 项目的自述文件。


若要执行此操作，请创建 `readme.txt` 文件，将其放在项目根文件夹中，然后在 `.nuspec` 文件中引用：

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


## <a name="net-standard-mapping-table"></a>.NET Standard 映射表

|平台名称 |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Mono/Xamarin 平台| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|通用 Windows 平台| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>相关主题

- [Nuspec 引用](../schema/nuspec.md)
- [符号包](../create-packages/symbol-packages.md)
- [包版本控制](../reference/package-versioning.md)
- [支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [创建本地化包](../create-packages/creating-localized-packages.md)
- [.NET Standard 库文档](https://docs.microsoft.com/dotnet/articles/standard/library)
- [从 .NET Framework 移植到 .NET Core](https://docs.microsoft.com/dotnet/articles/core/porting/index)
