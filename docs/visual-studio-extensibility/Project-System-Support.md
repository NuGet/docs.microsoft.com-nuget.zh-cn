---
title: NuGet 对 Visual Studio 项目系统的支持
description: 将 NuGet 集成到第三方项目类型的 Visual Studio 项目系统中。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 9f1ddfd20835cc3a0f9af40a8b4e712c218b31bc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901403"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="6524c-103">NuGet 对 Visual Studio 项目系统的支持</span><span class="sxs-lookup"><span data-stu-id="6524c-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="6524c-104">为在 Visual Studio 中支持第三方项目类型，NuGet 3.x+ 支持[公共项目系统 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)，且 NuGet 3.2+ 也支持非 CPS 项目系统。</span><span class="sxs-lookup"><span data-stu-id="6524c-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="6524c-105">若要与 NuGet 集成，项目系统必须播发自己对本主题中介绍的所有项目功能的支持。</span><span class="sxs-lookup"><span data-stu-id="6524c-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="6524c-106">不声明项目实际上没有的功能，以便在项目中安装程序包。</span><span class="sxs-lookup"><span data-stu-id="6524c-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="6524c-107">除 NuGet 客户端之外，Visual Studio 的许多功能和其他扩展还依赖于项目功能。</span><span class="sxs-lookup"><span data-stu-id="6524c-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="6524c-108">项目的错误播发功能会导致这些组件出现故障，同时对用户体验产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="6524c-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="6524c-109">播发项目功能</span><span class="sxs-lookup"><span data-stu-id="6524c-109">Advertise project capabilities</span></span>

<span data-ttu-id="6524c-110">NuGet 客户端基于[项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)确定与项目类型兼容的包，如下表所述。</span><span class="sxs-lookup"><span data-stu-id="6524c-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="6524c-111">功能</span><span class="sxs-lookup"><span data-stu-id="6524c-111">Capability</span></span> | <span data-ttu-id="6524c-112">说明</span><span class="sxs-lookup"><span data-stu-id="6524c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6524c-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="6524c-113">AssemblyReferences</span></span> | <span data-ttu-id="6524c-114">指示项目支持程序集引用（与 WinRTReferences 不同）。</span><span class="sxs-lookup"><span data-stu-id="6524c-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="6524c-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="6524c-115">DeclaredSourceItems</span></span> | <span data-ttu-id="6524c-116">指示项目是一个典型的 MSBuild 项目（不是 DNX），因为它在项目本身中声明源项目。</span><span class="sxs-lookup"><span data-stu-id="6524c-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="6524c-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="6524c-117">UserSourceItems</span></span>|<span data-ttu-id="6524c-118">指示允许用户向其项目添加任意文件。</span><span class="sxs-lookup"><span data-stu-id="6524c-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="6524c-119">有关基于 CPS 的项目系统，本节剩余部分中介绍了项目功能的实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="6524c-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="6524c-120">请参阅[声明 CPS 项目中的项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)。</span><span class="sxs-lookup"><span data-stu-id="6524c-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="6524c-121">实现 VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="6524c-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="6524c-122">`VsProjectCapabilitiesPresenceChecker` 类必须实现 `IVsBooleanSymbolPresenceChecker` 接口，定义如下：</span><span class="sxs-lookup"><span data-stu-id="6524c-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="6524c-123">此接口的示例实现是：</span><span class="sxs-lookup"><span data-stu-id="6524c-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="6524c-124">请记住，基于项目系统实际支持的内容添加/删除 `ActualProjectCapabilities` 集的功能。</span><span class="sxs-lookup"><span data-stu-id="6524c-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="6524c-125">若要了解完整说明，请参阅[项目功能文档](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="6524c-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="6524c-126">对查询作出响应</span><span class="sxs-lookup"><span data-stu-id="6524c-126">Responding to queries</span></span>

<span data-ttu-id="6524c-127">项目通过 `IVsHierarchy::GetProperty` 支持 `VSHPROPID_ProjectCapabilitiesChecker` 属性来声明此功能。</span><span class="sxs-lookup"><span data-stu-id="6524c-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="6524c-128">它应返回 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` 的实例，`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 程序集中对其进行了定义。</span><span class="sxs-lookup"><span data-stu-id="6524c-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="6524c-129">通过安装[相应的 NuGet 包](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)引用此程序集。</span><span class="sxs-lookup"><span data-stu-id="6524c-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="6524c-130">例如，可将以下 `case` 语句添加到 `IVsHierarchy::GetProperty` 方法的 `switch` 语句中：</span><span class="sxs-lookup"><span data-stu-id="6524c-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="6524c-131">DTE 支持</span><span class="sxs-lookup"><span data-stu-id="6524c-131">DTE Support</span></span>

<span data-ttu-id="6524c-132">NuGet 通过调用到 [DTE](/dotnet/api/envdte.dte)（Visual Studio 的顶级自动化接口），使项目系统添加引用、内容项和 MSBuild 导入。</span><span class="sxs-lookup"><span data-stu-id="6524c-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="6524c-133">DTE 是一组可能已经实现的 COM 接口。</span><span class="sxs-lookup"><span data-stu-id="6524c-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="6524c-134">如果项目类型基于 CPS，则已实现 DTE。</span><span class="sxs-lookup"><span data-stu-id="6524c-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
