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
# <a name="packagesconfig-reference"></a>packages.config 引用

某些项目类型中使用 `packages.config` 文件维护项目引用的包的列表。 这样，当项目要传输到不同的计算机（例如生成服务器）时，NuGet 就可以轻松地还原项目的依赖项，而无需所有这些包。

如果使用， `packages.config` 通常位于项目根目录中。 它在第一个 NuGet 操作运行时自动创建，但也可以在运行任何命令之前手动创建，如 `nuget restore` 。

使用 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 的项目不使用 `packages.config` 。

## <a name="schema"></a>架构

架构十分简单：以下标准 XML 标头是一个 `<packages>` 节点，包含一个或多个 `<package>` 元素，每个元素用于一个引用。 每个 `<package>` 元素可具有以下属性：

| 属性 | 必需 | 说明 |
| --- | --- | --- |
| id | 是 | 包的标识符，如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。 | 
| 版本 | 是 | 要安装的包的确切版本，如 3.1.1 或 4.2.5.11-beta。 版本字符串必须至少具有三个数字，可以选择性添加第四个数字作为预发布后缀。 不允许使用范围。 | 
| targetFramework | 否 | 安装包时应用的[目标框架名字对象 (TFM)](target-frameworks.md)。 安装包时，此内容最初设置为项目目标。 因此，不同的 `<package>` 元素可具有不同的 TFM。 例如，如果创建面向 .NET 4.5.2 的项目，此时安装的包将使用 net452 的 TFM。 如果稍后将项目重定向到 .NET 4.6 并添加更多包，这些包将使用 net46 的 TFM。 项目目标和 `targetFramework` 属性之间的不匹配会生成警告，在此情况下，可以重新安装受影响的包。 | 
| allowedVersions | 否 | 在包更新期间允许对此包应用的一系列版本（请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)）。 这不影响安装或还原操作期间安装的包。 有关语法的信息，请参阅[包版本控制](../concepts/package-versioning.md#version-ranges)。 PackageManager UI 还禁用允许范围之外的所有版本。 | 
| developmentDependency | 否 | 如果使用项目本身创建 NuGet 包，针对依赖项将其设置为 `true`，可防止在创建使用包时添加该包。 默认值为 `false`。 | 

## <a name="examples"></a>示例

以下 `packages.config` 指的是两个依赖项：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

以下 `packages.config` 指的是九个包，但由于 `developmentDependency` 属性，生成使用包时不会包括 `Microsoft.Net.Compilers`。 对 Newtonsoft.Json 的引用还将更新限制为仅 8.x 和 9.x 版本。

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
