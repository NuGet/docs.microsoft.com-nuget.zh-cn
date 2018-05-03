---
title: NuGet packages.config 文件引用
description: 在某些项目类型中，packages.config 维护项目中使用的 NuGet 包的列表。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 73234f79cb9eb30327c4e206a5bc51c5bc1c6f1d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="3911d-103">packages.config 引用</span><span class="sxs-lookup"><span data-stu-id="3911d-103">packages.config reference</span></span>

<span data-ttu-id="3911d-104">某些项目类型中使用 `packages.config` 文件维护项目引用的包的列表。</span><span class="sxs-lookup"><span data-stu-id="3911d-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="3911d-105">这允许 NuGet 在项目要传输到其他计算机（如生成服务器）上时轻松还原项目的依赖项，而无需所有这些包。</span><span class="sxs-lookup"><span data-stu-id="3911d-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="3911d-106">架构</span><span class="sxs-lookup"><span data-stu-id="3911d-106">Schema</span></span>

<span data-ttu-id="3911d-107">架构十分简单：以下标准 XML 标头是一个 `<packages>` 节点，包含一个或多个 `<package>` 元素，每个元素用于一个引用。</span><span class="sxs-lookup"><span data-stu-id="3911d-107">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="3911d-108">每个 `<package>` 元素可具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="3911d-108">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="3911d-109">特性</span><span class="sxs-lookup"><span data-stu-id="3911d-109">Attribute</span></span> | <span data-ttu-id="3911d-110">必需</span><span class="sxs-lookup"><span data-stu-id="3911d-110">Required</span></span> | <span data-ttu-id="3911d-111">描述</span><span class="sxs-lookup"><span data-stu-id="3911d-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3911d-112">id</span><span class="sxs-lookup"><span data-stu-id="3911d-112">id</span></span> | <span data-ttu-id="3911d-113">是</span><span class="sxs-lookup"><span data-stu-id="3911d-113">Yes</span></span> | <span data-ttu-id="3911d-114">包的标识符，如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。</span><span class="sxs-lookup"><span data-stu-id="3911d-114">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="3911d-115">version</span><span class="sxs-lookup"><span data-stu-id="3911d-115">version</span></span> | <span data-ttu-id="3911d-116">是</span><span class="sxs-lookup"><span data-stu-id="3911d-116">Yes</span></span> | <span data-ttu-id="3911d-117">要安装的包的确切版本，如 3.1.1 或 4.2.5.11-beta。</span><span class="sxs-lookup"><span data-stu-id="3911d-117">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="3911d-118">版本字符串必须至少具有三个数字，可以选择性添加第四个数字作为预发布后缀。</span><span class="sxs-lookup"><span data-stu-id="3911d-118">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="3911d-119">不允许使用范围。</span><span class="sxs-lookup"><span data-stu-id="3911d-119">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="3911d-120">targetFramework</span><span class="sxs-lookup"><span data-stu-id="3911d-120">targetFramework</span></span> | <span data-ttu-id="3911d-121">否</span><span class="sxs-lookup"><span data-stu-id="3911d-121">No</span></span> | <span data-ttu-id="3911d-122">安装包时应用的[目标框架名字对象 (TFM)](target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="3911d-122">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="3911d-123">安装包时，此内容最初设置为项目目标。</span><span class="sxs-lookup"><span data-stu-id="3911d-123">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="3911d-124">因此，不同的 `<package>` 元素可具有不同的 TFM。</span><span class="sxs-lookup"><span data-stu-id="3911d-124">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="3911d-125">例如，如果创建面向 .NET 4.5.2 的项目，此时安装的包将使用 net452 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="3911d-125">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="3911d-126">如果稍后将项目重定向到 .NET 4.6 并添加更多包，这些包将使用 net46 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="3911d-126">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="3911d-127">项目目标和 `targetFramework` 属性之间的不匹配会生成警告，在此情况下，可以重新安装受影响的包。</span><span class="sxs-lookup"><span data-stu-id="3911d-127">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="3911d-128">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="3911d-128">allowedVersions</span></span> | <span data-ttu-id="3911d-129">否</span><span class="sxs-lookup"><span data-stu-id="3911d-129">No</span></span> | <span data-ttu-id="3911d-130">在包更新期间允许对此包应用的一系列版本（请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)）。</span><span class="sxs-lookup"><span data-stu-id="3911d-130">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="3911d-131">这不影响安装或还原操作期间安装的包。</span><span class="sxs-lookup"><span data-stu-id="3911d-131">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="3911d-132">有关语法的信息，请参阅[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="3911d-132">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="3911d-133">PackageManager UI 还禁用允许范围之外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="3911d-133">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="3911d-134">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="3911d-134">developmentDependency</span></span> | <span data-ttu-id="3911d-135">否</span><span class="sxs-lookup"><span data-stu-id="3911d-135">No</span></span> | <span data-ttu-id="3911d-136">如果使用项目本身创建 NuGet 包，针对依赖项将其设置为 `true`，可防止在创建使用包时添加该包。</span><span class="sxs-lookup"><span data-stu-id="3911d-136">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="3911d-137">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="3911d-137">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="3911d-138">示例</span><span class="sxs-lookup"><span data-stu-id="3911d-138">Examples</span></span>

<span data-ttu-id="3911d-139">以下 `packages.config` 指的是两个依赖项：</span><span class="sxs-lookup"><span data-stu-id="3911d-139">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="3911d-140">以下 `packages.config` 指的是九个包，但由于 `developmentDependency` 属性，生成使用包时不会包括 `Microsoft.Net.Compilers`。</span><span class="sxs-lookup"><span data-stu-id="3911d-140">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="3911d-141">对 Newtonsoft.Json 的引用还将更新限制为仅 8.x 和 9.x 版本。</span><span class="sxs-lookup"><span data-stu-id="3911d-141">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
