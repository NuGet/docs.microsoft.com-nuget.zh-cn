---
title: "创建跨平台的 NuGet 包（适用于 iOS、Android 和 Windows）| Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "从头到尾演练如何为 Xamarin 创建在 iOS、Android 和 Windows 上使用本机 API 的 NuGet 包。"
keywords: "创建包, 适用于 Xamarin 的包, 跨平台包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f0131e4f447e2e0ab5a1d17e476a425eaa01b61
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="2bd7f-104">创建跨平台包</span><span class="sxs-lookup"><span data-stu-id="2bd7f-104">Create cross-platform packages</span></span>

<span data-ttu-id="2bd7f-105">跨平台包包含在 iOS、Android 和 Windows 上使用本机 API 的代码，具体取决于运行时操作系统。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="2bd7f-106">虽然这很简单，但最好让开发人员通过通用的 API 外围应用从 PCL 或 .NET Standard 库中使用包。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="2bd7f-107">在本演练中，将创建可在 iOS、Android 和 Windows 的移动项目中使用的跨平台 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-107">In this walkthrough you create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="2bd7f-108">先决条件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="2bd7f-109">创建项目结构和抽象代码</span><span class="sxs-lookup"><span data-stu-id="2bd7f-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="2bd7f-110">编写平台特定的代码</span><span class="sxs-lookup"><span data-stu-id="2bd7f-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="2bd7f-111">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="2bd7f-112">打包组件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="2bd7f-113">相关主题</span><span class="sxs-lookup"><span data-stu-id="2bd7f-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="2bd7f-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-114">Pre-requisites</span></span>

1. <span data-ttu-id="2bd7f-115">在通用 Windows 平台 (UWP) 和 Xamarin 中使用 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="2bd7f-116">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版；当然，也可以使用 Professional 和 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="2bd7f-117">若要包含 UWP 和 Xamarin 工具，请选择自定义安装并选中相应的选项。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="2bd7f-118">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-118">NuGet CLI.</span></span> <span data-ttu-id="2bd7f-119">从 [nuget.org/downloads](https://nuget.org/downloads) 下载 nuget.exe 的最新版本，将其保存到选择的位置。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="2bd7f-120">然后将该位置添加到 PATH 环境变量（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="2bd7f-121">nuget.exe 是 CLI 工具本身，不是安装程序，因此一定要保存从浏览器下载的文件，而非运行。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="2bd7f-122">创建项目结构和抽象代码</span><span class="sxs-lookup"><span data-stu-id="2bd7f-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="2bd7f-123">下载并运行适用于 Visual Studio 的 [适用于 Xamarin 的插件模板扩展组件](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="2bd7f-124">使用这些模板可轻松创建本演练所需的项目结构。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="2bd7f-125">在 Visual Studio 中，选择“文件”>“新建”>“项目”，搜索 `Plugin`，选择“适用于 Xamarin 的插件”模板，将名称更改为“LoggingLibrary”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio 中的新空白应用（Xamarin.Forms 可移植）](media/CrossPlatform-NewProject.png)

<span data-ttu-id="2bd7f-127">生成的解决方案包含两个 PCL 项目，以及各种平台特定的项目：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="2bd7f-128">名为 `Plugin.LoggingLibrary.Abstractions (Portable)` 的 PCL 定义组件的公共接口（API 外围应用），在本例中，即为 ILoggingLibrary.cs 文件中包含的 `ILoggingLibrary` 接口。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="2bd7f-129">你将在此文件中定义库的接口。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-129">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="2bd7f-130">另一个 PCL `Plugin.LoggingLibrary (Portable)` 包含 CrossLoggingLibrary.cs 中的代码，这些代码将在运行时定位抽象接口的平台特定实现。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="2bd7f-131">通常不需要修改此文件。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="2bd7f-132">每个平台特定的项目（如 `Plugin.LoggingLibrary.Android`）在其各自的 LoggingLibraryImplementation.cs 文件中都包含该接口的本机实现。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="2bd7f-133">你将在此文件中生成库的代码。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-133">This is where you build out your library's code.</span></span>

<span data-ttu-id="2bd7f-134">默认情况下，Abstractions 项目的 ILoggingLibrary.cs 文件包含接口定义，但不包含方法。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="2bd7f-135">为进行本演练，请按如下所示添加 `Log` 方法：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="2bd7f-136">编写平台特定的代码</span><span class="sxs-lookup"><span data-stu-id="2bd7f-136">Write your platform-specific code</span></span>

<span data-ttu-id="2bd7f-137">若要实现 `ILoggingLibrary` 接口及其方法的平台特定实现，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="2bd7f-138">打开每个平台项目的 `LoggingLibraryImplementation.cs` 文件并添加必要的代码。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="2bd7f-139">例如（使用 `Plugin.LoggingLibrary.Android` 项目）：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. <span data-ttu-id="2bd7f-140">在想要支持的每个平台的项目中重复此实现。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="2bd7f-141">右键单击 iOS 项目，选择“属性”，单击“生成”选项卡，然后从“输出路径”和“XML 文档文件”设置中删除“\iPhone”。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="2bd7f-142">这样做只是为了方便后面的演练。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="2bd7f-143">完成后，保存文件。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-143">Save the file when done.</span></span>
1. <span data-ttu-id="2bd7f-144">右键单击解决方案，选择“配置管理器...”，然后选中支持的 PCL 和每个平台的“生成”框。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="2bd7f-145">右键单击解决方案，选择“生成解决方案”，检查工作并生成接下来将要打包的项目。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="2bd7f-146">如果遇到关于缺少引用的错误，请右键单击解决方案，选择“还原 NuGet 包”，安装依赖项并重新生成。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="2bd7f-147">若要为 iOS 生成，需要一台连接到 Visual Studio 的联网 Mac，如 [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)（Xamarin.iOS for Visual Studio 简介）中所述。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="2bd7f-148">如果没有可用的 Mac，请清除配置管理器中的 iOS 项目（上面的步骤 3）。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="2bd7f-149">创建并更新 .nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="2bd7f-150">打开命令提示符，导航到 `.sln` 文件下一级的 `LoggingLibrary` 文件夹，然后运行 NuGet `spec` 命令，创建初始 `Package.nuspec` 文件：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```cli
nuget spec
```

1. <span data-ttu-id="2bd7f-151">将该文件重命名为 `LoggingLibrary.nuspec` 并在编辑器中打开。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="2bd7f-152">将文件更新为与以下内容匹配，并将 YOUR_NAME 替换为适当的值。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="2bd7f-153">具体而言，`<id>` 值在 nuget.org 中必须是唯一的（请参阅[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定）。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="2bd7f-154">另请注意，还必须更新创建者和说明标记，否则在打包步骤中会出现错误。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-154">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="2bd7f-155">可使用 `-alpha`、`-beta` 或 `-rc` 为包版本添加后缀，将包标记为预发行版本，有关预发行版本的详细信息，请查阅[预发行版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="2bd7f-156">添加引用程序集</span><span class="sxs-lookup"><span data-stu-id="2bd7f-156">Add reference assemblies</span></span>

<span data-ttu-id="2bd7f-157">若要包含平台特定的引用程序集，请将以下内容添加到 `LoggingLibrary.nuspec` 的 `<files>` 元素，以适用于支持的平台：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="2bd7f-158">若要缩短 DLL 和 XML 文件的名称，请右键单击任何给定项目，选择“库”选项卡，然后更改程序集名称。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="2bd7f-159">添加依赖项</span><span class="sxs-lookup"><span data-stu-id="2bd7f-159">Add dependencies</span></span>

<span data-ttu-id="2bd7f-160">如果有特定的本机实现依赖项，请使用带有 `<group>` 元素的 `<dependencies>` 元素来指定它们，例如：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="2bd7f-161">例如，以下代码用于将 iTextSharp 设置为 UAP 目标的依赖项：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="2bd7f-162">最终 .nuspec</span><span class="sxs-lookup"><span data-stu-id="2bd7f-162">Final .nuspec</span></span>

<span data-ttu-id="2bd7f-163">现在，最终 `.nuspec` 文件应该如下所示，其中应再次将 YOUR_NAME 替换为适当的值：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="2bd7f-164">打包组件</span><span class="sxs-lookup"><span data-stu-id="2bd7f-164">Package the component</span></span>

<span data-ttu-id="2bd7f-165">如果已完成的 `.nuspec` 引用需要包含在包中的所有文件，便可运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="2bd7f-166">将生成 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="2bd7f-167">在类似 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中打开此文件并展开所有节点，即可看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="2bd7f-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![显示 LoggingLibrary 包的 NuGet 包资源管理器](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="2bd7f-169">`.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="2bd7f-170">然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="2bd7f-171">若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="2bd7f-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="2bd7f-172">相关主题</span><span class="sxs-lookup"><span data-stu-id="2bd7f-172">Related topics</span></span>

- [<span data-ttu-id="2bd7f-173">Nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="2bd7f-173">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="2bd7f-174">符号包</span><span class="sxs-lookup"><span data-stu-id="2bd7f-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="2bd7f-175">包版本控制</span><span class="sxs-lookup"><span data-stu-id="2bd7f-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2bd7f-176">支持多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="2bd7f-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2bd7f-177">将 MSBuild 属性和目标包含到包中</span><span class="sxs-lookup"><span data-stu-id="2bd7f-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="2bd7f-178">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="2bd7f-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)