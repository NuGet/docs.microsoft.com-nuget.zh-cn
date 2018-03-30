---
title: 创建 NuGet 包的概述和工作流 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 概述创建和发布 NuGet 包的流程，其中提供该流程其他特定部分的链接。
keywords: NuGet 包创建, NuGet 创建概述, NuGet 创建工作流, 宝创建工作流, 包创建概述.
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: df08e15c2632a88ea7cc3333d64f4844c78c278d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="package-creation-workflow"></a>包创建工作流

通过公共 nuget.org 库或组织内部的私有库，创建你要进行打包并与他人共享的、以编译代码（通常为 .NET 程序集）开头的包。 此包还可以包含其他文件（如安装包时显示的自述文件）以及特定项目文件的转换文件。

包还可仅用于拉入任意数量的其他依赖项，但不包含其自己的任何代码。 利用这种包可以轻松传递由多个独立包组成的 SDK。 在其他情况下，包可能仅包含用于协助调试的符号 (`.pdb`) 文件。

> [!Note]
> 如果要创建供其他开发人员使用的包，则务必了解他们将依赖于你的工作成果。 因此，创建并发布包也表示你将修复 bug 和提供其他更新，或者至少应以开源形式提供包，以便他人可帮助维护包。

在任何情况下，创建包首先需要确定要打包的程序集及其他文件。 然后创建称为 `.nuspec` 的清单文件，用于描述包的内容及其标识符、版本号、版权信息、MSBuild 属性和目标以及其他诸多内容。

在相应文件夹中准备好所有必要文件并创建 `.nuspec` 文件后，应使用 `nuget pack` 命令（或 [MSBuild pack target](../reference/msbuild-targets.md)）将所有内容一起放入 `.nupkg` 文件。 此时便可将包部署到可供其他开发人员使用的任何主机。

> [!Tip]
> 具有 `.nupkg` 扩展名的 NuGet 包只是一个 zip 文件。 若要轻松查看任何包的内容，只需将扩展名更改为 `.zip` 并按常规方法展开内容。 尝试将包上传到主机前，请务必将扩展名改回 `.nupkg`。

若想了解并掌握创建流程，请首先参阅[创建包](../create-packages/creating-a-package.md)，其中针对适用于所有包的核心流程提供了完整说明。

接下来，你可以考虑对包应用其他多种选项：

- [支持多目标框架](../create-packages/supporting-multiple-target-frameworks.md)，说明如何创建具有面向不同 .NET Framework 的多个变体的包。
- [创建本地化包](../create-packages/creating-localized-packages.md)，说明如何构建具有多个语言资源的包以及如何使用独立的本地化附属包。
- [预发行包](../create-packages/prerelease-packages.md)，演示如何向感兴趣的客户发布 alpha、beta 和 rc 版本的包。
- [源和配置文件转换](../create-packages/source-and-config-file-transformations.md)，说明如何在已添加到项目的文件中执行两种单向令牌替换，以及如何修改 `web.config` 和 `app.config`（卸载包时还将舍弃这两者的设置）。
- [符号包](../create-packages/symbol-packages.md)，说明如何为库提供符号以允许使用者在调试期间单步执行代码。
- [包版本控制](../reference/package-versioning.md)，说明如何识别依赖项（通过你的包所使用的其他包）所需的确切版本。
- [本机包](../create-packages/native-packages.md)，说明面向 C++ 使用者创建包的流程。
- [签名包](../create-packages/sign-a-package.md)，说明向包添加数字签名的流程。

当准备好将包发布到 nuget.org 时，请按照[发布包](../create-packages/publish-a-package.md)中的简单流程执行操作。

如果希望使用私有源而非 nuget.org，请参阅[托管包概述](../hosting-packages/overview.md)
