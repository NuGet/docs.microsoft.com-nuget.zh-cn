---
title: NuGet packages.config 文件引用
description: 在某些项目类型中，packages.config 维护项目中使用的 NuGet 包的列表。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: da682197d4a156f9dff8ce169aab449a5392ef41
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "99260298"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="e892e-103">packages.config 引用</span><span class="sxs-lookup"><span data-stu-id="e892e-103">packages.config reference</span></span>

<span data-ttu-id="e892e-104">某些项目类型中使用 `packages.config` 文件维护项目引用的包的列表。</span><span class="sxs-lookup"><span data-stu-id="e892e-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="e892e-105">这样，当项目要传输到不同的计算机（例如生成服务器）时，NuGet 就可以轻松地还原项目的依赖项，而无需所有这些包。</span><span class="sxs-lookup"><span data-stu-id="e892e-105">This allows NuGet to easily restore the project's dependencies when the project is to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="e892e-106">如果使用， `packages.config` 通常位于项目根目录中。</span><span class="sxs-lookup"><span data-stu-id="e892e-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="e892e-107">它在第一个 NuGet 操作运行时自动创建，但也可以在运行任何命令之前手动创建，如 `nuget restore` 。</span><span class="sxs-lookup"><span data-stu-id="e892e-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="e892e-108">使用 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 的项目不使用 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="e892e-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="e892e-109">架构</span><span class="sxs-lookup"><span data-stu-id="e892e-109">Schema</span></span>

<span data-ttu-id="e892e-110">架构十分简单：以下标准 XML 标头是一个 `<packages>` 节点，包含一个或多个 `<package>` 元素，每个元素用于一个引用。</span><span class="sxs-lookup"><span data-stu-id="e892e-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="e892e-111">每个 `<package>` 元素可具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="e892e-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="e892e-112">属性</span><span class="sxs-lookup"><span data-stu-id="e892e-112">Attribute</span></span> | <span data-ttu-id="e892e-113">必需</span><span class="sxs-lookup"><span data-stu-id="e892e-113">Required</span></span> | <span data-ttu-id="e892e-114">说明</span><span class="sxs-lookup"><span data-stu-id="e892e-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e892e-115">id</span><span class="sxs-lookup"><span data-stu-id="e892e-115">id</span></span> | <span data-ttu-id="e892e-116">是</span><span class="sxs-lookup"><span data-stu-id="e892e-116">Yes</span></span> | <span data-ttu-id="e892e-117">包的标识符，如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。</span><span class="sxs-lookup"><span data-stu-id="e892e-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="e892e-118">版本</span><span class="sxs-lookup"><span data-stu-id="e892e-118">version</span></span> | <span data-ttu-id="e892e-119">是</span><span class="sxs-lookup"><span data-stu-id="e892e-119">Yes</span></span> | <span data-ttu-id="e892e-120">要安装的包的确切版本，如 3.1.1 或 4.2.5.11-beta。</span><span class="sxs-lookup"><span data-stu-id="e892e-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="e892e-121">版本字符串必须至少具有三个数字，可以选择性添加第四个数字作为预发布后缀。</span><span class="sxs-lookup"><span data-stu-id="e892e-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="e892e-122">不允许使用范围。</span><span class="sxs-lookup"><span data-stu-id="e892e-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="e892e-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="e892e-123">targetFramework</span></span> | <span data-ttu-id="e892e-124">否</span><span class="sxs-lookup"><span data-stu-id="e892e-124">No</span></span> | <span data-ttu-id="e892e-125">安装包时应用的[目标框架名字对象 (TFM)](target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="e892e-126">安装包时，此内容最初设置为项目目标。</span><span class="sxs-lookup"><span data-stu-id="e892e-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="e892e-127">因此，不同的 `<package>` 元素可具有不同的 TFM。</span><span class="sxs-lookup"><span data-stu-id="e892e-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="e892e-128">例如，如果创建面向 .NET 4.5.2 的项目，此时安装的包将使用 net452 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="e892e-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="e892e-129">如果稍后将项目重定向到 .NET 4.6 并添加更多包，这些包将使用 net46 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="e892e-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="e892e-130">项目目标和 `targetFramework` 属性之间的不匹配会生成警告，在此情况下，可以重新安装受影响的包。</span><span class="sxs-lookup"><span data-stu-id="e892e-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="e892e-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="e892e-131">allowedVersions</span></span> | <span data-ttu-id="e892e-132">否</span><span class="sxs-lookup"><span data-stu-id="e892e-132">No</span></span> | <span data-ttu-id="e892e-133">在包更新期间允许对此包应用的一系列版本（请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)）。</span><span class="sxs-lookup"><span data-stu-id="e892e-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="e892e-134">这不影响安装或还原操作期间安装的包。</span><span class="sxs-lookup"><span data-stu-id="e892e-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="e892e-135">有关语法的信息，请参阅[包版本控制](../concepts/package-versioning.md#version-ranges)。</span><span class="sxs-lookup"><span data-stu-id="e892e-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="e892e-136">PackageManager UI 还禁用允许范围之外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="e892e-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="e892e-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="e892e-137">developmentDependency</span></span> | <span data-ttu-id="e892e-138">否</span><span class="sxs-lookup"><span data-stu-id="e892e-138">No</span></span> | <span data-ttu-id="e892e-139">如果使用项目本身创建 NuGet 包，针对依赖项将其设置为 `true`，可防止在创建使用包时添加该包。</span><span class="sxs-lookup"><span data-stu-id="e892e-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="e892e-140">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="e892e-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="e892e-141">示例</span><span class="sxs-lookup"><span data-stu-id="e892e-141">Examples</span></span>

<span data-ttu-id="e892e-142">以下 `packages.config` 指的是两个依赖项：</span><span class="sxs-lookup"><span data-stu-id="e892e-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="e892e-143">以下 `packages.config` 指的是九个包，但由于 `developmentDependency` 属性，生成使用包时不会包括 `Microsoft.Net.Compilers`。</span><span class="sxs-lookup"><span data-stu-id="e892e-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="e892e-144">对 Newtonsoft.Json 的引用还将更新限制为仅 8.x 和 9.x 版本。</span><span class="sxs-lookup"><span data-stu-id="e892e-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
