---
title: 使用 Visual Studio 2015 创建 .NET Standard 和 .NET Framework NuGet 包
description: 从头到尾介绍如何使用 NuGet 3.x 和 Visual Studio 2015 创建 .NET Standard 和 .NET Framework NuGet 包。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: a77d977b2abc4cfd8be48e97e4c811e68e09bd61
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>使用 Visual Studio 2015 创建 NET Standard 和 .NET Framework 包

注意：建议使用 Visual Studio 2017 来开发 .NET Standard 库。 Visual Studio 2015 可以工作，但 .NET Core 工具仅处于预览状态。 有关使用 NuGet 4.x+ 和 Visual Studio 2017 的详细信息，请参阅[使用 Visual Studio 2017 创建和发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md)。

[.NET Standard 库](/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。 .NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。 它使得开发人员可以生成跨所有 .NET 运行时可用的代码，并减少（如果不能消除）共享代码中平台特定的条件编译指令。

本指南将为你逐步介绍如何创建面向 .NET Standard 库 1.4 的 NuGet 包或面向 .NET Framework 4.6 的包。 .NET Standard 1.4 库可在 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 上使用。 有关详细信息，请参阅 [.NET Standard 映射表](/dotnet/standard/net-standard#net-implementation-support)（.NET 文档）。 如果需要，可以选择其他版本的 .NET Standard 库。

## <a name="prerequisites"></a>系统必备

1. Visual Studio 2015 Update 3
1. （仅适用于 .NET Standard）[.NET Core SDK](https://www.microsoft.com/net/download/)
1. NuGet CLI。 从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。 然后将该位置添加到 PATH 环境变量（如果尚未添加）。

    > [!Note]
    > nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。

## <a name="create-the-class-library-project"></a>创建类库项目

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C#”>“Windows”节点，选择“类库(可移植)”，将名称更改为“AppLogger”，然后选择“确定”。

    ![创建新类库项目](media/NetStandard-NewProject.png)

1. 在显示的“添加可移植类库”对话框中，选择 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 选项。 （如果面向 .NET Framework，则可以选择任何相应选项。）

1. 如果面向 .NET Standard，右键单击解决方案资源管理器中的 `AppLogger (Portable)`，选择“属性”，选择“库”选项卡，然后选择“目标”部分中的“目标 .NET 平台标准”。 此操作将提示进行确认，在确认后可以从下拉列表中选择 `.NET Standard 1.4`（或其他可用版本）：

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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. 将配置设置为“发布”，生成项目，并检查 `bin\Release` 文件夹中生成了 DLL 和 XML 文件。

## <a name="create-and-update-the-nuspec-file"></a>创建并更新 .nuspec 文件

1. 打开命令提示符，导航到包含 `AppLogger.csproj` 文件夹的文件夹（`.sln` 文件的下一级），然后运行 NuGet `spec` 命令，创建初始 `AppLogger.nuspec` 文件：

    ```cli
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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. 将引用程序集添加到 `.nuspec` 文件，也就是库的 DLL 和 IntelliSense XML 文件：

    如果面向 .NET Standard，则条目类似于以下内容：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    如果面向 .NET Framework ，则条目类似于以下内容：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. 右键单击解决方案，选择“生成解决方案”，生成包的所有文件。

### <a name="declaring-dependencies"></a>声明依赖项

如果具有其他 NuGet 包的任何依赖项，请使用 `<group>` 元素在清单的 `<dependencies>` 元素中列出这些依赖项。 例如，若要在 NewtonSoft.Json 8.0.3 或更高版本上声明依赖项，请添加以下内容：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

此处 version 特性的语法指示可接受版本 8.0.3 或更高版本。 若要指定不同的版本范围，请参阅[包版本控制](../reference/package-versioning.md)。

### <a name="adding-a-readme"></a>添加自述文件

创建 `readme.txt` 文件，将其放在项目根文件夹中，然后在 `.nuspec` 文件中引用：

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

将包安装到项目中时，Visual Studio 显示 `readme.txt`。 当安装到 .NET Core 项目中或其作为依赖项安装的包时，不会显示该文件。

## <a name="package-the-component"></a>打包组件

如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：

```cli
nuget pack AppLogger.nuspec
```

这将生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`。 在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容（显示为 .NET Standard）：

![显示 AppLogger 包的 NuGet 包资源管理器](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。 然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。

若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。

请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。 在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。

## <a name="related-topics"></a>相关主题

- [Nuspec 引用](../reference/nuspec.md)
- [支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [创建本地化包](../create-packages/creating-localized-packages.md)
- [符号包](../create-packages/symbol-packages.md)
- [包版本控制](../reference/package-versioning.md)
- [.NET Standard 库文档](/dotnet/articles/standard/library)
- [从 .NET Framework 移植到 .NET Core](/dotnet/articles/core/porting/index)
