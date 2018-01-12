---
title: "适用于 NuGet 包的源和配置文件转换 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "详细介绍在安装 NuGet 包时将包转换为源代码和配置 (XML) 文件的功能。"
keywords: "NuGet 包安装, NuGet 包转换, 修改配置文件, 修改源代码"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 89a55716ccbc9043cfce4c7f38ec8ab9a0e2f768
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="ea4a1-104">转换源代码和配置文件</span><span class="sxs-lookup"><span data-stu-id="ea4a1-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="ea4a1-105">对于使用 `packages.config` 或 `project.json` 的项目，NuGet 支持在安装和卸载包时将包转换为源代码和配置文件的功能。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-105">For projects using `packages.config` or `project.json`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span>

> [!Note]
> <span data-ttu-id="ea4a1-106">当使用[配置文件中的包引用](../Consume-Packages/Package-References-in-Project-Files.md)在项目中安装包时，不会应用源和配置文件转换。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-106">Source and configuration file transformations are not applied when a package is installed in a project using [Package References in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> 

<span data-ttu-id="ea4a1-107">安装包时，“源代码转化”会对包的 `content` 文件夹中的文件应用单向令牌替换，其中令牌表示 Visual Studio [项目属性](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_)。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_).</span></span> <span data-ttu-id="ea4a1-108">这样就可以将文件插入到项目的命名空间中，或者自定义通常转到 ASP.NET 项目的 `global.asax` 中的代码。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="ea4a1-109">通过“配置文件转换”可以修改目标项目中已存在的文件，例如 `web.config` 和 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="ea4a1-110">例如，包可能需要将某个项添加到配置文件中的 `modules` 部分。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="ea4a1-111">此转换通过将特殊文件包含在描述要添加到配置文件的部分的包中完成。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="ea4a1-112">卸载包时，会接着反转相同的更改，使其变为双向转换。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="ea4a1-113">指定源代码转换</span><span class="sxs-lookup"><span data-stu-id="ea4a1-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="ea4a1-114">需要从包插入到项目的文件必须位于包的 `content` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="ea4a1-115">例如，如果希望将一个名为 `ContosoData.cs` 的文件安装在目标项目的 `Models` 文件夹中，则它必须位于包的 `content\Models` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

1. <span data-ttu-id="ea4a1-116">若要指示 NuGet 在安装时应用令牌替换，请将 `.pp` 追加到源代码文件名。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="ea4a1-117">安装后，文件不会具有 `.pp` 扩展名。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="ea4a1-118">例如，若要在 `ContosoData.cs` 中转换，请在包 `ContosoData.cs.pp` 中命名文件。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="ea4a1-119">安装后，它将以 `ContosoData.cs` 形式出现。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-119">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="ea4a1-120">在源代码文件中，使用 `$token$` 形式的不区分大小写令牌指示 NuGet 应使用项目属性替换的值：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="ea4a1-121">安装后，NuGet 将 `$rootnamespace$` 替换为 `Fabrikam`（假设目标项目的根命名空间为 `Fabrikam`）。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="ea4a1-122">`$rootnamespace$` 令牌是最常用的项目属性；其他所有项目属性列在 MSDN 上的[项目属性](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_)文档中。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in the [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) documentation on MSDN.</span></span> <span data-ttu-id="ea4a1-123">请注意，有些属性可能特定于某一项目类型。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="ea4a1-124">指定配置文件转换</span><span class="sxs-lookup"><span data-stu-id="ea4a1-124">Specifying config file transformations</span></span>

<span data-ttu-id="ea4a1-125">如以下部分所述，可以通过两种方法完成配置文件转换：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="ea4a1-126">在包的 `content` 文件夹中包含 `app.config.transform` 和 `web.config.transform` 文件，其中 `.transform` 扩展名告知 NuGet 这些文件包含在安装包时要与现有配置文件合并的 XML。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="ea4a1-127">卸载包时，该相同 XML 被删除。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="ea4a1-128">（NuGet 2.6 及更高版本）在包的 `content` 文件夹中包含 `app.config.install.xdt` 和 `web.config.install.xdt` 文件，并使用 [XDT 语法](https://msdn.microsoft.com/library/dd465326.aspx)描述所需更改。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="ea4a1-129">使用此选项还可以包含 `.uninstall.xdt` 文件，在从项目删除包时撤销更改。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="ea4a1-130">转换不适用于在 Visual Studio 中作为链接引用的 `.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="ea4a1-131">使用 XDT 的优点是，它不是简单地合并两个静态文件，而是提供一种语法来操纵 XML DOM 的结构，这种语法使用元素和特性，支持完整的 XPath 路径。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="ea4a1-132">然后 XDT 可以添加、更新或删除元素、将新元素放在特定位置，或者替换/删除元素（包括子节点）。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="ea4a1-133">这使得创建卸载转换非常简单，卸载转换指退出包安装期间所完成的全部转换。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="ea4a1-134">XML 转换</span><span class="sxs-lookup"><span data-stu-id="ea4a1-134">XML transforms</span></span>

<span data-ttu-id="ea4a1-135">包的 `content` 文件夹中的 `app.config.transform` 和 `web.config.transform` 仅包含要合并到项目现有 `app.config` 和 `web.config` 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="ea4a1-136">例如，假设项目最初在 `web.config` 中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-137">若要在包安装期间将 `MyNuModule` 元素添加到 `modules` 部分，请在包的 `content` 文件夹中创建 `web.config.transform` 文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-138">NuGet 安装包后，`web.config` 将显示为：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-139">注意，NuGet 未替换 `modules` 部分，只是通过仅添加新元素和特性合并了新条目。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="ea4a1-140">NuGet 不会更改任何现有元素或特性。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="ea4a1-141">卸载包时，NuGet 会再次检查 `.transform` 文件，并从相应的 `.config` 文件中删除它包含的元素。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="ea4a1-142">注意，此过程不会影响包安装后修改的 `.config` 文件中的任何行。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="ea4a1-143">一个更广泛的示例是[适用于 ASP.NET 的 错误日志记录模块和处理程序 (ELMAH)](https://www.nuget.org/packages/elmah/) 包将多个条目添加到 `web.config` 中，这些条目在卸载包时会再次删除。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="ea4a1-144">若要检查其 `web.config.transform` 文件，请从上述链接下载 ELMAH 包，将包扩展名从 `.nupkg` 更改为 `.zip`，然后打开该 ZIP 文件中的 `content\web.config.transform`。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="ea4a1-145">若要查看安装和卸载包的影响，请在 Visual Studio 中创建新的 ASP.NET 项目（模板位于“新建项目”对话框的“Visual C#”>“Web”下），并选择一个空的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="ea4a1-146">打开 `web.config` 查看其初始状态。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="ea4a1-147">然后右键单击项目，选择“管理 NuGet 包”，在 nuget.org 上浏览 ELMAH 并安装最新版本。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="ea4a1-148">注意对 `web.config` 进行的所有更改。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="ea4a1-149">然后，卸载包，将会看见 `web.config` 还原到之前的状态。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-149">Now uninstall the package and you'll see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="ea4a1-150">XDT 转换</span><span class="sxs-lookup"><span data-stu-id="ea4a1-150">XDT transforms</span></span>

<span data-ttu-id="ea4a1-151">有了 NuGet 2.6 和更高版本，可以使用 [XDT 语法](https://msdn.microsoft.com/library/dd465326.aspx)修改配置文件。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="ea4a1-152">还可以通过在 `$` 分隔符内包含属性名称（不区分大小写），让 NuGet 将令牌替换为[项目属性](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_)。</span><span class="sxs-lookup"><span data-stu-id="ea4a1-152">You can also have NuGet replace tokens with [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="ea4a1-153">例如，以下 `app.config.install.xdt` 文件会将 `appSettings` 元素插入到包含项目 `FullPath`、`FileName` 和 `ActiveConfigurationSettings` 值的 `app.config` 中：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="ea4a1-154">有关另一个示例，假设项目最初在 `web.config` 中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-155">若要在安装包期间将 `MyNuModule` 元素添加到 `modules` 部分，包的 `web.config.install.xdt` 应包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-156">安装包以后，`web.config` 将如下所示：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-156">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="ea4a1-157">若要在卸载包期间仅删除 `MyNuModule` 元素，`web.config.uninstall.xdt` 文件应包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="ea4a1-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
