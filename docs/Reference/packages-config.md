---
title: NuGet packages.config 文件引用 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 在某些项目类型中，packages.config 维护项目中使用的 NuGet 包的列表。
keywords: NuGet packages.config 文件, NuGet 包引用, NuGet 依赖项
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="1b7cf-104">packages.config 引用</span><span class="sxs-lookup"><span data-stu-id="1b7cf-104">packages.config reference</span></span>

<span data-ttu-id="1b7cf-105">某些项目类型中使用 `packages.config` 文件维护项目引用的包的列表。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="1b7cf-106">这允许 NuGet 在项目要传输到其他计算机（如生成服务器）上时轻松还原项目的依赖项，而无需所有这些包。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="1b7cf-107">架构</span><span class="sxs-lookup"><span data-stu-id="1b7cf-107">Schema</span></span>

<span data-ttu-id="1b7cf-108">架构十分简单：以下标准 XML 标头是一个 `<packages>` 节点，包含一个或多个 `<package>` 元素，每个元素用于一个引用。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="1b7cf-109">每个 `<package>` 元素可具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="1b7cf-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="1b7cf-110">特性</span><span class="sxs-lookup"><span data-stu-id="1b7cf-110">Attribute</span></span> | <span data-ttu-id="1b7cf-111">必需</span><span class="sxs-lookup"><span data-stu-id="1b7cf-111">Required</span></span> | <span data-ttu-id="1b7cf-112">描述</span><span class="sxs-lookup"><span data-stu-id="1b7cf-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b7cf-113">id</span><span class="sxs-lookup"><span data-stu-id="1b7cf-113">id</span></span> | <span data-ttu-id="1b7cf-114">是</span><span class="sxs-lookup"><span data-stu-id="1b7cf-114">Yes</span></span> | <span data-ttu-id="1b7cf-115">包的标识符，如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="1b7cf-116">version</span><span class="sxs-lookup"><span data-stu-id="1b7cf-116">version</span></span> | <span data-ttu-id="1b7cf-117">是</span><span class="sxs-lookup"><span data-stu-id="1b7cf-117">Yes</span></span> | <span data-ttu-id="1b7cf-118">要安装的包的确切版本，如 3.1.1 或 4.2.5.11-beta。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="1b7cf-119">版本字符串必须至少具有三个数字，可以选择性添加第四个数字作为预发布后缀。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="1b7cf-120">不允许使用范围。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="1b7cf-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="1b7cf-121">targetFramework</span></span> | <span data-ttu-id="1b7cf-122">否</span><span class="sxs-lookup"><span data-stu-id="1b7cf-122">No</span></span> | <span data-ttu-id="1b7cf-123">安装包时应用的[目标框架名字对象 (TFM)](target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-123">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="1b7cf-124">安装包时，此内容最初设置为项目目标。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="1b7cf-125">因此，不同的 `<package>` 元素可具有不同的 TFM。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="1b7cf-126">例如，如果创建面向 .NET 4.5.2 的项目，此时安装的包将使用 net452 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="1b7cf-127">如果稍后将项目重定向到 .NET 4.6 并添加更多包，这些包将使用 net46 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="1b7cf-128">项目目标和 `targetFramework` 属性之间的不匹配会生成警告，在此情况下，可以重新安装受影响的包。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="1b7cf-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="1b7cf-129">allowedVersions</span></span> | <span data-ttu-id="1b7cf-130">否</span><span class="sxs-lookup"><span data-stu-id="1b7cf-130">No</span></span> | <span data-ttu-id="1b7cf-131">在包更新期间允许对此包应用的一系列版本（请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)）。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="1b7cf-132">这不影响安装或还原操作期间安装的包。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="1b7cf-133">有关语法的信息，请参阅[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="1b7cf-134">PackageManager UI 还禁用允许范围之外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="1b7cf-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="1b7cf-135">developmentDependency</span></span> | <span data-ttu-id="1b7cf-136">否</span><span class="sxs-lookup"><span data-stu-id="1b7cf-136">No</span></span> | <span data-ttu-id="1b7cf-137">如果使用项目本身创建 NuGet 包，针对依赖项将其设置为 `true`，可防止在创建使用包时添加该包。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="1b7cf-138">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="1b7cf-139">示例</span><span class="sxs-lookup"><span data-stu-id="1b7cf-139">Examples</span></span>

<span data-ttu-id="1b7cf-140">以下 `packages.config` 指的是两个依赖项：</span><span class="sxs-lookup"><span data-stu-id="1b7cf-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="1b7cf-141">以下 `packages.config` 指的是九个包，但由于 `developmentDependency` 属性，生成使用包时不会包括 `Microsoft.Net.Compilers`。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="1b7cf-142">对 Newtonsoft.Json 的引用还将更新限制为仅 8.x 和 9.x 版本。</span><span class="sxs-lookup"><span data-stu-id="1b7cf-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
