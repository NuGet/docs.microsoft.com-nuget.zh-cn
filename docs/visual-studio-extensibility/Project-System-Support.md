---
title: NuGet 对 Visual Studio 项目系统的支持
description: 将 NuGet 集成到第三方项目类型的 Visual Studio 项目系统中。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551365"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>NuGet 对 Visual Studio 项目系统的支持

为在 Visual Studio 中支持第三方项目类型，NuGet 3.x+ 支持[公共项目系统 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)，且 NuGet 3.2+ 也支持非 CPS 项目系统。

若要与 NuGet 集成，项目系统必须播发自己对本主题中介绍的所有项目功能的支持。

> [!Note]
> 不声明项目实际上没有的功能，以便在项目中安装程序包。 除 NuGet 客户端之外，Visual Studio 的许多功能和其他扩展还依赖于项目功能。 项目的错误播发功能会导致这些组件出现故障，同时对用户体验产生负面影响。

## <a name="advertise-project-capabilities"></a>播发项目功能

NuGet 客户端基于[项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)确定与项目类型兼容的包，如下表所述。

| 功能 | 描述 |
| --- | --- |
| AssemblyReferences | 指示项目支持程序集引用（与 WinRTReferences 不同）。 |
| DeclaredSourceItems | 指示项目是一个典型的 MSBuild 项目（不是 DNX），因为它在项目本身中声明源项目。 |
| UserSourceItems|指示允许用户向其项目添加任意文件。 |

有关基于 CPS 的项目系统，本节剩余部分中介绍了项目功能的实现详细信息。 请参阅[声明 CPS 项目中的项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)。

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>实现 VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` 类必须实现 `IVsBooleanSymbolPresenceChecker` 接口，定义如下：

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

此接口的示例实现是：

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

请记住，基于项目系统实际支持的内容添加/删除 `ActualProjectCapabilities` 集的功能。 若要了解完整说明，请参阅[项目功能文档](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)。

## <a name="responding-to-queries"></a>对查询作出响应

项目通过 `IVsHierarchy::GetProperty` 支持 `VSHPROPID_ProjectCapabilitiesChecker` 属性来声明此功能。 它应返回 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` 的实例，`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 程序集中对其进行了定义。 通过安装[相应的 NuGet 包](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)引用此程序集。

例如，可将以下 `case` 语句添加到 `IVsHierarchy::GetProperty` 方法的 `switch` 语句中：

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE 支持

NuGet 通过调用到 [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)（Visual Studio 的顶级自动化接口），使项目系统添加引用、内容项和 MSBuild 导入。 DTE 是一组可能已经实现的 COM 接口。

如果项目类型基于 CPS，则已实现 DTE。
