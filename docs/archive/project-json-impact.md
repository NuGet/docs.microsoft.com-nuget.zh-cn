---
title: project.json 对 NuGet 包作者的影响
description: 详细介绍 NuGet 3.x 中的 project.json 实现如何影响包作者，如不支持的功能、内容和包格式。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545568"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>创建包时 project.json 产生的影响

> [!Important]
> 此内容已弃用。 项目应使用 `packages.config` 或 PackageReference 格式。

NuGet 3+ 中使用的 `project.json` 系统通过多种方式影响包作者，这些内容将在后续部分介绍。

## <a name="changes-affecting-existing-packages-usage"></a>影响现有包使用的更改

传统的 NuGet 包支持一系列不会传送到可传递体系的功能。

### <a name="install-and-uninstall-scripts-are-ignored"></a>忽略了安装和卸载脚本

[依赖项解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中介绍的可传递还原模型不具有“包安装时间”概念。 包的状态为存在或不存在，但安装包后不会出现一致的进程。

此外，仅 Visual Studio 支持安装脚本。 其他 IDE 必须模拟 Visual Studio 扩展性 API 以尝试支持此类脚本，且在常见编辑器和命令行工具中不提供支持。

### <a name="content-transforms-are-not-supported"></a>不支持转换内容。

与安装脚本相似，转换在包安装上运行，且通常不是幂等的。 由于不再存在安装时间，XDT 转换和类似功能不受支持，并且如果在可传递方案中使用了此类包，则会忽略前述转换和功能。

### <a name="content"></a>内容

传统的 NuGet 包传送源代码和配置文件之类的内容文件。 通常用于以下两个方案：

1. 将初始文件放置到项目中，以便用户稍后进行编辑。 常见示例是默认配置文件。

1. 将内容文件用作项目中所安装程序集的辅助文件。 示例是程序集使用的徽标图像。

目前禁用了对内容的支持，其原因与不支持脚本和转换的原因相似，但我们正在设计对内容的支持。

内容文件仍可以在包中进行传送，且此类文件目前被忽略，但是最终用户仍可以将其复制到适当的位置。

可在此处查看恢复内容文件的其中一项建议并跟踪其进度：[https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)。

## <a name="impact-for-package-authors"></a>对包作者的影响

使用上述功能的包必须使用不同的机制。 对此最常用的有用机制是继续受到完全支持的 MSBuild 目标/属性。 生成系统可以选择在包中选取其他约定。 这样便可实现 MSBuild 目标和 Roslyn 分析器支持。 可以生成支持适用于 `packages.config` 和 `project.json` 方案的目标和分析器的包。

尝试修改项目以简化启动的包通常用于一组非常有限的方案，且应改为提供自述文件或包的使用方法指南。

大多数现有包都无需使用下文介绍的包格式。

格式使得本机内容作为优先方案。 这意味着，托管程序集依赖近硬件实现基于目标平台随托管程序集提供二进制实现。 例如，System.IO.Compression 包便是利用此技术。 [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

总之，如果上述功能不是绝对必要，我们建议继续使用现有的包格式，因为仅 NuGet 3.x+ 支持此处介绍的格式。

可通过填充生成适用于 `packages.config` 和 `project.json` 方案的包，但以传统方式组织包的结构通常会更简单，无需上述弃用的功能。

## <a name="3x-package-format"></a>3.x 包格式

3.x 包格式允许使用 NuGet 2.x 之外的其他几项功能：

1. 定义一个引用程序集和一组实现程序集，前者用于编译，后者用于不同平台/设备上的运行时。 这样，你就可以利用平台特定的 API，同时为使用者提供常见的外围应用。 具体而言，这有助于更轻松地编写中间可移植库。

1. 允许包在操作系统或 CPU 体系结构等平台上透视。

1. 允许将平台特定的实现分离到辅助包中。

1. 支持本机依赖项作为优先选项。
