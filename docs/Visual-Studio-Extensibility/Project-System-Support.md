---
title: "NuGet 对 Visual Studio 项目系统的支持 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "将 NuGet 集成到第三方项目类型的 Visual Studio 项目系统中。"
keywords: "Visual Studio 中的 NuGet, 自定义项目类型, Visual Studio 项目"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39212361e7cb2c214c3e83cef604d40cd057fd7e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="76410-104">NuGet 对 Visual Studio 项目系统的支持</span><span class="sxs-lookup"><span data-stu-id="76410-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="76410-105">为在 Visual Studio 中支持第三方项目类型，NuGet 3.x+ 支持[公共项目系统 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)，且 NuGet 3.2+ 也支持非 CPS 项目系统。</span><span class="sxs-lookup"><span data-stu-id="76410-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="76410-106">若要与 NuGet 集成，项目系统必须播发自己对本主题中介绍的所有项目功能的支持。</span><span class="sxs-lookup"><span data-stu-id="76410-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="76410-107">请勿为了在项目中安装包，而声明项目中实际没有的功能。</span><span class="sxs-lookup"><span data-stu-id="76410-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="76410-108">除 NuGet 客户端之外，Visual Studio 的许多功能和其他扩展还依赖于项目功能。</span><span class="sxs-lookup"><span data-stu-id="76410-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="76410-109">项目的错误播发功能会导致这些组件出现故障，同时对用户体验产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="76410-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="76410-110">播发项目功能</span><span class="sxs-lookup"><span data-stu-id="76410-110">Advertise project capabilities</span></span>

<span data-ttu-id="76410-111">NuGet 客户端基于[项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)确定与项目类型兼容的包，如下表所述。</span><span class="sxs-lookup"><span data-stu-id="76410-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="76410-112">功能</span><span class="sxs-lookup"><span data-stu-id="76410-112">Capability</span></span>|<span data-ttu-id="76410-113">描述</span><span class="sxs-lookup"><span data-stu-id="76410-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="76410-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="76410-114">AssemblyReferences</span></span>|<span data-ttu-id="76410-115">指示项目支持程序集引用（与 WinRTReferences 不同）</span><span class="sxs-lookup"><span data-stu-id="76410-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="76410-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="76410-116">DeclaredSourceItems</span></span>|<span data-ttu-id="76410-117">指示项目是典型的 MSBuild 项目（而不是 DNX），因为它声明项目本身的源项目（而不是 `project.json` 文件，该文件假定文件夹中的所有文件均为编译的一部分）。</span><span class="sxs-lookup"><span data-stu-id="76410-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="76410-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="76410-118">UserSourceItems</span></span>|<span data-ttu-id="76410-119">指示允许用户向其项目添加任意文件。</span><span class="sxs-lookup"><span data-stu-id="76410-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="76410-120">有关基于 CPS 的项目系统，本节剩余部分中介绍了项目功能的实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="76410-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="76410-121">请参阅[声明 CPS 项目中的项目功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)。</span><span class="sxs-lookup"><span data-stu-id="76410-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="76410-122">实现 VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="76410-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="76410-123">`VsProjectCapabilitiesPresenceChecker` 类必须实现 `IVsBooleanSymbolPresenceChecker` 接口，定义如下：</span><span class="sxs-lookup"><span data-stu-id="76410-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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


<span data-ttu-id="76410-124">此接口的示例实现是：</span><span class="sxs-lookup"><span data-stu-id="76410-124">A sample implementation of this interface would then be:</span></span>
    
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

<span data-ttu-id="76410-125">请记住，基于项目系统实际支持的内容添加/删除 `ActualProjectCapabilities` 集的功能。</span><span class="sxs-lookup"><span data-stu-id="76410-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="76410-126">若要了解完整说明，请参阅[项目功能文档](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="76410-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="76410-127">对查询作出响应</span><span class="sxs-lookup"><span data-stu-id="76410-127">Responding to queries</span></span>

<span data-ttu-id="76410-128">项目通过 `IVsHierarchy::GetProperty` 支持 `VSHPROPID_ProjectCapabilitiesChecker` 属性来声明此功能。</span><span class="sxs-lookup"><span data-stu-id="76410-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="76410-129">它应返回 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` 的实例，`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 程序集中对其进行了定义。</span><span class="sxs-lookup"><span data-stu-id="76410-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="76410-130">通过安装[相应的 NuGet 包](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)引用此程序集。</span><span class="sxs-lookup"><span data-stu-id="76410-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="76410-131">例如，可将以下 `case` 语句添加到 `IVsHierarchy::GetProperty` 方法的 `switch` 语句中：</span><span class="sxs-lookup"><span data-stu-id="76410-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```


## <a name="dte-support"></a><span data-ttu-id="76410-132">DTE 支持</span><span class="sxs-lookup"><span data-stu-id="76410-132">DTE Support</span></span>

<span data-ttu-id="76410-133">NuGet 通过调用到 [DTE](https://msdn.microsoft.com/library/mt452175.aspx)（Visual Studio 的顶级自动化接口），使项目系统添加引用、内容项和 MSBuild 导入。</span><span class="sxs-lookup"><span data-stu-id="76410-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](https://msdn.microsoft.com/library/mt452175.aspx), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="76410-134">DTE 是一组可能已经实现的 COM 接口。</span><span class="sxs-lookup"><span data-stu-id="76410-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="76410-135">如果项目类型基于 CPS，则已实现 DTE。</span><span class="sxs-lookup"><span data-stu-id="76410-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
