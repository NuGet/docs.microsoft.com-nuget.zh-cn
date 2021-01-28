---
title: 适用于 NuGet 包的源和配置文件转换
description: 详细介绍在安装 NuGet 包时将包转换为源代码和配置 (XML) 文件的功能。
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5bd0e409f527fb668008204fb16ad002f4784c46
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774579"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="04f8a-103">转换源代码和配置文件</span><span class="sxs-lookup"><span data-stu-id="04f8a-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="04f8a-104">安装包时，“源代码转化”会对包的 `content` 或 `contentFiles` 文件夹（对于为 `PackageReference` 使用 `packages.config` 和 `contentFiles` 的用户，则为 `content`）中的文件应用单向令牌替换，其中令牌表示 Visual Studio [项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)。</span><span class="sxs-lookup"><span data-stu-id="04f8a-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="04f8a-105">这样就可以将文件插入到项目的命名空间中，或者自定义通常转到 ASP.NET 项目的 `global.asax` 中的代码。</span><span class="sxs-lookup"><span data-stu-id="04f8a-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="04f8a-106">通过“配置文件转换”可以修改目标项目中已存在的文件，例如 `web.config` 和 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="04f8a-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="04f8a-107">例如，包可能需要将某个项添加到配置文件中的 `modules` 部分。</span><span class="sxs-lookup"><span data-stu-id="04f8a-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="04f8a-108">此转换通过将特殊文件包含在描述要添加到配置文件的部分的包中完成。</span><span class="sxs-lookup"><span data-stu-id="04f8a-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="04f8a-109">卸载包时，会接着反转相同的更改，使其变为双向转换。</span><span class="sxs-lookup"><span data-stu-id="04f8a-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="04f8a-110">指定源代码转换</span><span class="sxs-lookup"><span data-stu-id="04f8a-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="04f8a-111">需要从包插入到项目的文件必须位于包的 `content` 和 `contentFiles` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="04f8a-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="04f8a-112">例如，如果希望将一个名为 `ContosoData.cs` 的文件安装在目标项目的 `Models` 文件夹中，则它必须位于包的 `content\Models` 和 `contentFiles\{lang}\{tfm}\Models` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="04f8a-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="04f8a-113">若要指示 NuGet 在安装时应用令牌替换，请将 `.pp` 追加到源代码文件名。</span><span class="sxs-lookup"><span data-stu-id="04f8a-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="04f8a-114">安装后，文件不会具有 `.pp` 扩展名。</span><span class="sxs-lookup"><span data-stu-id="04f8a-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="04f8a-115">例如，若要在 `ContosoData.cs` 中转换，请在包 `ContosoData.cs.pp` 中命名文件。</span><span class="sxs-lookup"><span data-stu-id="04f8a-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="04f8a-116">安装后，它将以 `ContosoData.cs` 形式出现。</span><span class="sxs-lookup"><span data-stu-id="04f8a-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="04f8a-117">在源代码文件中，使用 `$token$` 形式的不区分大小写令牌指示 NuGet 应使用项目属性替换的值：</span><span class="sxs-lookup"><span data-stu-id="04f8a-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="04f8a-118">安装后，NuGet 将 `$rootnamespace$` 替换为 `Fabrikam`（假设目标项目的根命名空间为 `Fabrikam`）。</span><span class="sxs-lookup"><span data-stu-id="04f8a-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="04f8a-119">`$rootnamespace$` 令牌是最常用的项目属性；其他所有项目属性均列在[项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)中。</span><span class="sxs-lookup"><span data-stu-id="04f8a-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="04f8a-120">请注意，有些属性可能特定于某一项目类型。</span><span class="sxs-lookup"><span data-stu-id="04f8a-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="04f8a-121">指定配置文件转换</span><span class="sxs-lookup"><span data-stu-id="04f8a-121">Specifying config file transformations</span></span>

<span data-ttu-id="04f8a-122">如以下部分所述，可以通过两种方法完成配置文件转换：</span><span class="sxs-lookup"><span data-stu-id="04f8a-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="04f8a-123">在包的 `content` 文件夹中包含 `app.config.transform` 和 `web.config.transform` 文件，其中 `.transform` 扩展名告知 NuGet 这些文件包含在安装包时要与现有配置文件合并的 XML。</span><span class="sxs-lookup"><span data-stu-id="04f8a-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="04f8a-124">卸载包时，该相同 XML 被删除。</span><span class="sxs-lookup"><span data-stu-id="04f8a-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="04f8a-125">在包的 `content` 文件夹中包含 `app.config.install.xdt` 和 `web.config.install.xdt` 文件，并使用 [XDT 语法](/previous-versions/aspnet/dd465326(v=vs.110))描述所需更改。</span><span class="sxs-lookup"><span data-stu-id="04f8a-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)) to describe the desired changes.</span></span> <span data-ttu-id="04f8a-126">使用此选项还可以包含 `.uninstall.xdt` 文件，在从项目删除包时撤销更改。</span><span class="sxs-lookup"><span data-stu-id="04f8a-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="04f8a-127">转换不适用于在 Visual Studio 中作为链接引用的 `.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="04f8a-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="04f8a-128">使用 XDT 的优点是，它不是简单地合并两个静态文件，而是提供一种语法来操纵 XML DOM 的结构，这种语法使用元素和特性，支持完整的 XPath 路径。</span><span class="sxs-lookup"><span data-stu-id="04f8a-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="04f8a-129">然后 XDT 可以添加、更新或删除元素、将新元素放在特定位置，或者替换/删除元素（包括子节点）。</span><span class="sxs-lookup"><span data-stu-id="04f8a-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="04f8a-130">这使得创建卸载转换非常简单，卸载转换指退出包安装期间所完成的全部转换。</span><span class="sxs-lookup"><span data-stu-id="04f8a-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="04f8a-131">XML 转换</span><span class="sxs-lookup"><span data-stu-id="04f8a-131">XML transforms</span></span>

<span data-ttu-id="04f8a-132">包的 `content` 文件夹中的 `app.config.transform` 和 `web.config.transform` 仅包含要合并到项目现有 `app.config` 和 `web.config` 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="04f8a-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="04f8a-133">例如，假设项目最初在 `web.config` 中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="04f8a-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="04f8a-134">若要在包安装期间将 `MyNuModule` 元素添加到 `modules` 部分，请在包的 `content` 文件夹中创建 `web.config.transform` 文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="04f8a-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="04f8a-135">NuGet 安装包后，`web.config` 将显示为：</span><span class="sxs-lookup"><span data-stu-id="04f8a-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="04f8a-136">注意，NuGet 未替换 `modules` 部分，只是通过仅添加新元素和特性合并了新条目。</span><span class="sxs-lookup"><span data-stu-id="04f8a-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="04f8a-137">NuGet 不会更改任何现有元素或特性。</span><span class="sxs-lookup"><span data-stu-id="04f8a-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="04f8a-138">卸载包时，NuGet 会再次检查 `.transform` 文件，并从相应的 `.config` 文件中删除它包含的元素。</span><span class="sxs-lookup"><span data-stu-id="04f8a-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="04f8a-139">注意，此过程不会影响包安装后修改的 `.config` 文件中的任何行。</span><span class="sxs-lookup"><span data-stu-id="04f8a-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="04f8a-140">一个更广泛的示例是[适用于 ASP.NET 的 错误日志记录模块和处理程序 (ELMAH)](https://www.nuget.org/packages/elmah/) 包将多个条目添加到 `web.config` 中，这些条目在卸载包时会再次删除。</span><span class="sxs-lookup"><span data-stu-id="04f8a-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="04f8a-141">若要检查其 `web.config.transform` 文件，请从上述链接下载 ELMAH 包，将包扩展名从 `.nupkg` 更改为 `.zip`，然后打开该 ZIP 文件中的 `content\web.config.transform`。</span><span class="sxs-lookup"><span data-stu-id="04f8a-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="04f8a-142">若要查看安装和卸载包的影响，请在 Visual Studio 中创建新的 ASP.NET 项目（模板位于“新建项目”对话框的“Visual C#”>“Web”下），并选择一个空的 ASP.NET 应用程序  。</span><span class="sxs-lookup"><span data-stu-id="04f8a-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="04f8a-143">打开 `web.config` 查看其初始状态。</span><span class="sxs-lookup"><span data-stu-id="04f8a-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="04f8a-144">然后右键单击项目，选择“管理 NuGet 包”，在 nuget.org 上浏览 ELMAH 并安装最新版本  。</span><span class="sxs-lookup"><span data-stu-id="04f8a-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="04f8a-145">注意对 `web.config` 进行的所有更改。</span><span class="sxs-lookup"><span data-stu-id="04f8a-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="04f8a-146">现在卸载包，你会看见 `web.config` 还原到其之前的状态。</span><span class="sxs-lookup"><span data-stu-id="04f8a-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="04f8a-147">XDT 转换</span><span class="sxs-lookup"><span data-stu-id="04f8a-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="04f8a-148">如[从 `packages.config` 迁移到 `PackageReference` 文档的包兼容性问题一节](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)所述，下述 XDT 转换仅受 `packages.config` 支持。</span><span class="sxs-lookup"><span data-stu-id="04f8a-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="04f8a-149">如果将以下文件添加到包中，则使用者在使用具有 `PackageReference` 的包时无需应用转换（参考[本示例](https://github.com/NuGet/Samples/tree/master/XDTransformExample)，了解如何让 XDT 转换适用于 `PackageReference`）。</span><span class="sxs-lookup"><span data-stu-id="04f8a-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="04f8a-150">可以使用 [XDT 语法](/previous-versions/aspnet/dd465326(v=vs.110))修改配置文件。</span><span class="sxs-lookup"><span data-stu-id="04f8a-150">You can modify config files using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)).</span></span> <span data-ttu-id="04f8a-151">此外，还可通过在 `$` 分隔符内包含属性名称（不区分大小写），让 NuGet 将令牌替换为[项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)。</span><span class="sxs-lookup"><span data-stu-id="04f8a-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="04f8a-152">例如，以下 `app.config.install.xdt` 文件会将 `appSettings` 元素插入到包含项目 `FullPath`、`FileName` 和 `ActiveConfigurationSettings` 值的 `app.config` 中：</span><span class="sxs-lookup"><span data-stu-id="04f8a-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="04f8a-153">有关另一个示例，假设项目最初在 `web.config` 中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="04f8a-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="04f8a-154">若要在安装包期间将 `MyNuModule` 元素添加到 `modules` 部分，包的 `web.config.install.xdt` 应包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="04f8a-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="04f8a-155">安装包以后，`web.config` 将如下所示：</span><span class="sxs-lookup"><span data-stu-id="04f8a-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="04f8a-156">若要在卸载包期间仅删除 `MyNuModule` 元素，`web.config.uninstall.xdt` 文件应包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="04f8a-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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