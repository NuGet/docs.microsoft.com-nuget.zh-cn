---
title: 如何创建本地化 NuGet 包 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 详细介绍创建本地化 NuGet 包的两种方法：将所有程序集包含在一个包中，或者发布单独的程序集。
keywords: NuGet 包本地化, NuGet 附属程序集, 创建本地化包, NuGet 本地化约定
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 39ff6d300ec1a1f7941cad5953599f25f55117f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="creating-localized-nuget-packages"></a>创建本地化 NuGet 包

有两种方法可创建库的本地化版本：

1. 将所有本地化资源程序集包含在一个包中。
1. 遵循一组严格的约定，创建单独的本地化附属包。

两种方法各有优缺点，如以下部分中所述。

## <a name="localized-resource-assemblies-in-a-single-package"></a>本地化资源程序集位于一个包中

将本地化资源程序集包含在一个包中通常是最简单的方法。 若要执行此操作，请在 `lib` 中创建文件夹用于支持的语言，而不是包默认语言（假定为 en-us）。 在这些文件夹中，可以放置资源程序集和本地化 IntelliSense XML 文件。

例如，以下文件夹结构支持德语 (de)、意大利语 (it)、日语 (ja)、俄语 (ru)、简体中文 (zh-Hans) 和繁体中文 (zh-Hant)：

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

可以看到，这些语言全都列在 `net40` 目标框架文件夹下。 如果[支持多个框架](../create-packages/supporting-multiple-target-frameworks.md)，则 `lib` 下将有每个变体的文件夹。

这些文件夹准备就绪后，即可在 `.nuspec` 中引用所有文件：

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

使用此方法的一个包示例为 [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0)。

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>优点和缺点（本地化资源程序集）

将所有语言捆绑到一个包中存在几个缺点：

1. **共享元数据**：由于 NuGet 包只可包含一个 `.nuspec` 文件，因此仅可以为一种语言提供元数据。 也就是说，NuGet 当前不支持本地化元数据。
1. **包大小**：根据支持的语言数量，库可能变得相当大，这会减慢包的安装和还原速度。
1. **同时发布**：将本地化文件捆绑到一个包中需要同时发布该包中的所有资产，而不是能够单独发布每个本地化。 此外，对任何一个本地化的任何更新都需要整个包的新版本。

然而，它也存在几个优点：

1. **简单**：包的使用者安装一次即可获得支持的所有语言，而不必单独安装每种语言。 在 nuget.org 上查找单个包也更加轻松。
1. **耦合版本**：由于所有资源程序集与主程序集都位于相同的包中，因此它们共享相同的版本号，且不存在错误分离的风险。

## <a name="localized-satellite-packages"></a>本地化附属包

类似于 .NET Framework 支持附属程序集的方式，此方法将本地化资源和 IntelliSense XML 文件分离为附属包。

若要执行此操作，主包会使用命名约定 `{identifier}.{version}.nupkg` 并包含默认语言（如 en-US）的程序集。 例如，`ContosoUtilities.1.0.0.nupkg` 将包含以下结构：

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

附属程序集然后会使用命名约定 `{identifier}.{language}.{version}.nupkg`，如 `ContosoUtilities.de.1.0.0.nupkg`。 标识符必须与主包完全匹配。

由于这是单独的包，因此它本身具有包含本地化元数据的 `.nuspec` 文件。 请注意，`.nuspec` 中的语言必须与文件名中所使用的语言匹配。

附属程序集还必须使用 [] 版本表示法，将主包的确切版本声明为依赖项（请参阅[包版本控制](../reference/package-versioning.md)）。 例如，`ContosoUtilities.de.1.0.0.nupkg` 必须使用 `[1.0.0]` 表示法声明对 `ContosoUtilities.1.0.0.nupkg` 的依赖项。 当然，附属包的版本号可以与主包不同。

然后，附属包结构必须将资源程序集和 XML IntelliSense 包含在与包文件名中的 `{language}` 匹配的子文件夹中：

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

注意：除非需要特定的子区域性（如 `ja-JP`），否则请始终使用更高级别的语言标识符，如 `ja`。

在附属程序集中，NuGet 仅会识别文件名与 `{language}` 匹配的文件夹中的这些文件。 将忽略所有其他成员。

如果满足所有这些约定，NuGet 会将包识别为附属包并将本地化文件安装到主包的 `lib` 文件夹中，就好像它们最初就进行了捆绑。 卸载附属程序包将从该相同文件夹中删除其文件。

你将以相同方式为支持的每种语言创建其他附属程序集。 例如，检查一组 ASP.NET MVC 包：

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc)（主要为英语）
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de)（德语）
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja)（日语）
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans)（简体中文）
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant)（繁体中文）

### <a name="summary-of-required-conventions"></a>所需约定摘要

- 主包必须命名为 `{identifier}.{version}.nupkg`
- 附属包必须命名为 `{identifier}.{language}.{version}.nupkg`
- 附属包的 `.nuspec` 必须指定其语言以与文件名匹配。
- 附属包必须在其 `.nuspec` 文件中使用 [] 表示法，声明对主包确切版本的依赖项。 不支持范围。
- 附属包必须将文件放置于文件名与 `{language}` 完全匹配的 `lib\[{framework}\]{language}` 文件夹中。

### <a name="advantages-and-disadvantages-satellite-packages"></a>优点和缺点（附属包）

使用附属包有几个优点：

1. **包大小**：主包的总内存占用量最小化，而且使用者仅承担要使用的语言的费用。
1. **单独的元数据**：每个附属包都有自己的 `.nuspec` 文件，因此也拥有自己的本地化元数据。 借此，一些使用者可通过使用本地化术语搜索 nuget.org，更加轻松地查找包。
1. **分离发布**：附属程序集可随着时间推移进行发布，而不是一次完成，从而分散了本地化工作量。

然而，附属包也有其自身的一些缺点：

1. **混乱**：许多包（而不是一个包）可能会导致 nuget.org 上的搜索结果混乱以及 Visual Studio 项目中的引用列表变长。
1. **严格的约定**。 附属包必须完全遵循约定，否则将不会正确选取本地化版本。
1. **版本控制**：每个附属包必须对主包具有确切版本的依赖项。 这意味着更新主包可能也需要更新所有附属程序包，即使未更改资源。
