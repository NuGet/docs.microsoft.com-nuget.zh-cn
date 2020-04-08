---
title: 适用于 NuGet 包的源和配置文件转换
description: 详细介绍在安装 NuGet 包时将包转换为源代码和配置 (XML) 文件的功能。
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231170"
---
# <a name="transforming-source-code-and-configuration-files"></a>转换源代码和配置文件

安装包时，“源代码转化”会对包的 `content` 或 `contentFiles` 文件夹（对于为 `PackageReference` 使用 `packages.config` 和 `contentFiles` 的用户，则为 `content`）中的文件应用单向令牌替换，其中令牌表示 Visual Studio [项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)  。 这样就可以将文件插入到项目的命名空间中，或者自定义通常转到 ASP.NET 项目的 `global.asax` 中的代码。

通过“配置文件转换”可以修改目标项目中已存在的文件，例如 `web.config` 和 `app.config`  。 例如，包可能需要将某个项添加到配置文件中的 `modules` 部分。 此转换通过将特殊文件包含在描述要添加到配置文件的部分的包中完成。 卸载包时，会接着反转相同的更改，使其变为双向转换。

## <a name="specifying-source-code-transformations"></a>指定源代码转换

1. 需要从包插入到项目的文件必须位于包的 `content` 和 `contentFiles` 文件夹中。 例如，如果希望将一个名为 `ContosoData.cs` 的文件安装在目标项目的 `Models` 文件夹中，则它必须位于包的 `content\Models` 和 `contentFiles\{lang}\{tfm}\Models` 文件夹中。

1. 若要指示 NuGet 在安装时应用令牌替换，请将 `.pp` 追加到源代码文件名。 安装后，文件不会具有 `.pp` 扩展名。

    例如，若要在 `ContosoData.cs` 中转换，请在包 `ContosoData.cs.pp` 中命名文件。 安装后，它将以 `ContosoData.cs` 形式出现。

1. 在源代码文件中，使用 `$token$` 形式的不区分大小写令牌指示 NuGet 应使用项目属性替换的值：

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

    安装后，NuGet 将 `$rootnamespace$` 替换为 `Fabrikam`（假设目标项目的根命名空间为 `Fabrikam`）。

`$rootnamespace$` 令牌是最常用的项目属性；其他所有项目属性均列在[项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)中。 请注意，有些属性可能特定于某一项目类型。

## <a name="specifying-config-file-transformations"></a>指定配置文件转换

如以下部分所述，可以通过两种方法完成配置文件转换：

- 在包的 `content` 文件夹中包含 `app.config.transform` 和 `web.config.transform` 文件，其中 `.transform` 扩展名告知 NuGet 这些文件包含在安装包时要与现有配置文件合并的 XML。 卸载包时，该相同 XML 被删除。
- 在包的 `content` 文件夹中包含 `app.config.install.xdt` 和 `web.config.install.xdt` 文件，并使用 [XDT 语法](https://msdn.microsoft.com/library/dd465326.aspx)描述所需更改。 使用此选项还可以包含 `.uninstall.xdt` 文件，在从项目删除包时撤销更改。

> [!Note]
> 转换不适用于在 Visual Studio 中作为链接引用的 `.config` 文件。

使用 XDT 的优点是，它不是简单地合并两个静态文件，而是提供一种语法来操纵 XML DOM 的结构，这种语法使用元素和特性，支持完整的 XPath 路径。 然后 XDT 可以添加、更新或删除元素、将新元素放在特定位置，或者替换/删除元素（包括子节点）。 这使得创建卸载转换非常简单，卸载转换指退出包安装期间所完成的全部转换。

### <a name="xml-transforms"></a>XML 转换

包的 `content` 文件夹中的 `app.config.transform` 和 `web.config.transform` 仅包含要合并到项目现有 `app.config` 和 `web.config` 文件中的元素。

例如，假设项目最初在 `web.config` 中包含以下内容：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

若要在包安装期间将 `MyNuModule` 元素添加到 `modules` 部分，请在包的 `content` 文件夹中创建 `web.config.transform` 文件，如下所示：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet 安装包后，`web.config` 将显示为：

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

注意，NuGet 未替换 `modules` 部分，只是通过仅添加新元素和特性合并了新条目。 NuGet 不会更改任何现有元素或特性。

卸载包时，NuGet 会再次检查 `.transform` 文件，并从相应的 `.config` 文件中删除它包含的元素。 注意，此过程不会影响包安装后修改的 `.config` 文件中的任何行。

一个更广泛的示例是[适用于 ASP.NET 的 错误日志记录模块和处理程序 (ELMAH)](https://www.nuget.org/packages/elmah/) 包将多个条目添加到 `web.config` 中，这些条目在卸载包时会再次删除。

若要检查其 `web.config.transform` 文件，请从上述链接下载 ELMAH 包，将包扩展名从 `.nupkg` 更改为 `.zip`，然后打开该 ZIP 文件中的 `content\web.config.transform`。

若要查看安装和卸载包的影响，请在 Visual Studio 中创建新的 ASP.NET 项目（模板位于“新建项目”对话框的“Visual C#”>“Web”下），并选择一个空的 ASP.NET 应用程序  。 打开 `web.config` 查看其初始状态。 然后右键单击项目，选择“管理 NuGet 包”，在 nuget.org 上浏览 ELMAH 并安装最新版本  。 注意对 `web.config` 进行的所有更改。 现在卸载包，你会看见 `web.config` 还原到其之前的状态。

### <a name="xdt-transforms"></a>XDT 转换

> [!Note]
> 如[从 `packages.config` 迁移到 `PackageReference` 文档的包兼容性问题一节](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)所述，下述 XDT 转换仅受 `packages.config` 支持。 如果将以下文件添加到包中，则使用者在使用具有 `PackageReference` 的包时无需应用转换（参考[本示例](https://github.com/NuGet/Samples/tree/master/XDTransformExample)，了解如何让 XDT 转换适用于 `PackageReference`）。

可以使用 [XDT 语法](https://msdn.microsoft.com/library/dd465326.aspx)修改配置文件。 此外，还可通过在 `$` 分隔符内包含属性名称（不区分大小写），让 NuGet 将令牌替换为[项目属性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)。

例如，以下 `app.config.install.xdt` 文件会将 `appSettings` 元素插入到包含项目 `FullPath`、`FileName` 和 `ActiveConfigurationSettings` 值的 `app.config` 中：

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

有关另一个示例，假设项目最初在 `web.config` 中包含以下内容：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

若要在安装包期间将 `MyNuModule` 元素添加到 `modules` 部分，包的 `web.config.install.xdt` 应包含以下内容：

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

安装包以后，`web.config` 将如下所示：

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

若要在卸载包期间仅删除 `MyNuModule` 元素，`web.config.uninstall.xdt` 文件应包含以下内容：

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
