---
title: 使用 Visual Studio 2017 或 2019 为 Xamarin 创建 NuGet 包（适用于 iOS、Android 和 Windows）
description: 从头到尾演练如何为 Xamarin 创建在 iOS、Android 和 Windows 上使用本机 API 的 NuGet 包。
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385663"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>使用 Visual Studio 2017 或 2019 为 Xamarin 创建包

Xamarin 包包含在 iOS、Android 和 Windows 上使用本机 API 的代码，具体取决于运行时操作系统。 虽然这很简单，但最好让开发人员通过通用的 API 外围应用从 PCL 或 .NET Standard 库中使用包。

在本演练中，将使用 Visual Studio 2017 或 2019 创建可在 iOS、Android 和 Windows 的移动项目中使用的跨平台 NuGet 包。

1. [系统必备](#prerequisites)
1. [创建项目结构和抽象代码](#create-the-project-structure-and-abstraction-code)
1. [编写平台特定的代码](#write-your-platform-specific-code)
1. [创建并更新 .nuspec 文件](#create-and-update-the-nuspec-file)
1. [打包组件](#package-the-component)
1. [相关主题](#related-topics)

## <a name="prerequisites"></a>先决条件

1. 在通用 Windows 平台 (UWP) 和 Xamarin 中使用 Visual Studio 2017 或 2019。 可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版；当然，也可以使用 Professional 和 Enterprise 版。 若要包含 UWP 和 Xamarin 工具，请选择自定义安装并选中相应的选项。
1. NuGet CLI。 从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。 然后将该位置添加到 PATH 环境变量（如果尚未添加）。

> [!Note]
> nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。

## <a name="create-the-project-structure-and-abstraction-code"></a>创建项目结构和抽象代码

1. 下载并运行适用于 Visual Studio 的[跨平台 .NET Standard 插件模板扩展](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。 使用这些模板可轻松创建本演练所需的项目结构。
1. 在 Visual Studio 2017 中，选择“文件”>“新建”>“项目”，搜索 `Plugin`，选择“跨平台 .NET Standard 库插件”模板，将名称更改为“LoggingLibrary”，然后单击“确定”   。

    ![VS 2017 中的新空白应用（Xamarin.Forms 可移植）](media/CrossPlatform-NewProject.png)

    在 Visual Studio 2019 中，选择“文件”>“新建”>“项目”，搜索 `Plugin`，选择“跨平台 .NET Standard 库插件”模板，然后单击“下一步”   。

    ![VS 2019 中的新空白应用（Xamarin.Forms 可移植）](media/CrossPlatform-NewProject19-Part1.png)

    将名称更改为 LoggingLibrary，然后单击“创建”。

    ![VS 2019 中的新空白应用（Xamarin.Forms 可移植）配置](media/CrossPlatform-NewProject19-Part2.png)

生成的解决方案包含两个共享项目，以及各种平台特定的项目：

- `ILoggingLibrary` 项目，该项目包含在 `ILoggingLibrary.shared.cs` 文件中，用于定义组件的公共接口（API 外围应用）。 你将在此文件中定义库的接口。
- 另一个共享项目包含 `CrossLoggingLibrary.shared.cs` 中的代码，这些代码将在运行时定位抽象接口的平台特定实现。 通常不需要修改此文件。
- 每个平台特定的项目（如 `LoggingLibrary.android.cs`）在其各自的 `LoggingLibraryImplementation.cs` (VS 2017) 或 `LoggingLibrary.<PLATFORM>.cs` (VS 2019) 文件中都包含该接口的本机实现。 你将在此文件中生成库的代码。

默认情况下，`ILoggingLibrary` 项目的 ILoggingLibrary.shared.cs 文件包含接口定义，但不包含方法。 为进行本演练，请按如下所示添加 `Log` 方法：

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>编写平台特定的代码

若要实现 `ILoggingLibrary` 接口及其方法的平台特定实现，请执行以下操作：

1. 打开每个平台项目的 `LoggingLibraryImplementation.cs` (VS 2017) 或 `LoggingLibrary.<PLATFORM>.cs` (VS 2019) 文件并添加必要的代码。 例如（使用 `Android` 平台项目）：

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. 在想要支持的每个平台的项目中重复此实现。
1. 右键单击解决方案，选择“生成解决方案”，检查工作并生成接下来将要打包的项目  。 如果遇到关于缺少引用的错误，请右键单击解决方案，选择“还原 NuGet 包”，安装依赖项并重新生成  。

> [!Note]
> 如果使用的是 Visual Studio 2019，则在选择“还原 NuGet 包”  并尝试重新生成之前，需要将 `MSBuild.Sdk.Extras` 的版本更改为 `LoggingLibrary.csproj` 中的 `2.0.54`。 只能通过以下方式访问此文件：首先右键单击该项目（在解决方案下方）并选择 `Unload Project`，然后右键单击卸载的项目并选择 `Edit LoggingLibrary.csproj`。

> [!Note]
> 若要为 iOS 生成，需要一台连接到 Visual Studio 的联网 Mac，如 [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)（Xamarin.iOS for Visual Studio 简介）中所述。 如果没有可用的 Mac，请清除配置管理器中的 iOS 项目（上面的步骤 3）。

## <a name="create-and-update-the-nuspec-file"></a>创建并更新 .nuspec 文件

1. 打开命令提示符，导航到 `.sln` 文件下一级的 `LoggingLibrary` 文件夹，然后运行 NuGet `spec` 命令，创建初始 `Package.nuspec` 文件：

    ```cli
    nuget spec
    ```

1. 将该文件重命名为 `LoggingLibrary.nuspec` 并在编辑器中打开。
1. 将文件更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。 具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。 另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> 可使用 `-alpha`、`-beta` 或 `-rc` 为包版本添加后缀，将包标记为预发行版本，有关预发行版本的详细信息，请查阅[预发行版本](../create-packages/prerelease-packages.md)。

### <a name="add-reference-assemblies"></a>添加引用程序集

若要包含平台特定的引用程序集，请将以下内容添加到 `LoggingLibrary.nuspec` 的 `<files>` 元素，以适用于支持的平台：

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> 若要缩短 DLL 和 XML 文件的名称，请右键单击任何给定项目，选择“库”选项卡，然后更改程序集名称  。

### <a name="add-dependencies"></a>添加依赖项

如果有特定的本机实现依赖项，请使用带有 `<group>` 元素的 `<dependencies>` 元素来指定它们，例如：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

例如，以下代码用于将 iTextSharp 设置为 UAP 目标的依赖项：

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>最终 .nuspec

现在，最终 `.nuspec` 文件应该如下所示，其中应再次将 YOUR_NAME 替换为适当的值：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>打包组件

如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：

```cli
nuget pack LoggingLibrary.nuspec
```

将生成 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。 在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容：

![显示 LoggingLibrary 包的 NuGet 包资源管理器](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。 然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。

若要使你的包可供其他开发人员使用，请按照[发布包](../nuget-org/publish-a-package.md)中的说明进行操作。

## <a name="related-topics"></a>相关主题

- [Nuspec 引用](../reference/nuspec.md)
- [符号包](../create-packages/symbol-packages.md)
- [包版本控制](../concepts/package-versioning.md)
- [支持多个 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [将 MSBuild 属性和目标包含到包中](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [创建本地化包](../create-packages/creating-localized-packages.md)