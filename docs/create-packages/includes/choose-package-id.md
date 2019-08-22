---
ms.openlocfilehash: 7ebe3c0f75b8de158879119bce4df26217849251
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488945"
---
包标识符和版本号是项目中最重要的两个值，因为它们唯一标识包中包含的确切代码。

**针对包标识符的最佳做法：**

- **唯一性**：标识符必须在 nuget.org 或托管包的任意库中是唯一的。 确定标识符之前，请搜索适用库以检查该名称是否已使用。 为了避免冲突，最好使用公司名作为标识符的第一部分（例如 `Contoso.`）。
- **类似于命名空间的名称**：遵循类似于 .NET 中命名空间的模式，使用点表示法（而不是连字符）。 例如，使用 `Contoso.Utility.UsefulStuff` 而不是 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。 当包标识符与代码中使用的命名空间相匹配时，这个方法也很有用。
- **示例包**：如果生成展示如何使用另一个包的示例代码包，请附加 `.Sample` 作为标识符的后缀，就像 `Contoso.Utility.UsefulStuff.Sample` 中一样。 （当然，示例包会在其他包上有依赖项。）创建示例包时，请在 `<IncludeAssets>` 中使用 `contentFiles` 值。 在 `content` 文件夹中，在名为 `\Samples\<identifier>` 的文件夹中排列示例代码，与 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相似。

**针对包版本的最佳做法：**

- 一般情况下，将包的版本设置为与项目（或程序集）相匹配，但这不是必须的。 如果将包限制为单个程序集，那么这是一个简单的问题。 总的来说，请记住解析依赖项时，NuGet 自己处理包版本而不是程序集版本。
- 使用非标准版本方案时，请确保考虑使用 NuGet 版本控制规则，如[包版本控制](../../concepts/package-versioning.md)中所述。 NuGet 主要与 [semver 2 兼容](../../concepts/package-versioning.md#semantic-versioning-200)。

> 有关依赖项解析的信息，请参阅[使用 PackageReference 的依赖项解析](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)。 对于可能有助于更好地理解版本控制的较旧信息，请参阅此系列博客文章。
>
> - [第 1 部分：解决 DLL 地狱](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部分：核心算法](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部分：通过绑定重定向实现统一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)