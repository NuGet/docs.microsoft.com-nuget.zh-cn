---
title: NuGet CLI 环境变量
description: Nuget.exe 环境变量的引用
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: adeacd917fd775c6eed431df9c0f74e591ad793e
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 环境变量

可以通过许多环境变量，这会影响计算机级用户 nuget.exe 或处理级别配置 nuget.exe CLI 的行为。 环境变量始终重写中的任何设置`NuGet.Config`文件，从而使生成服务器而无需修改任何文件更改相应的设置。

一般情况下，直接在命令行上或 NuGet 配置文件中指定的选项具有优先级，但如有少数例外情况之外*FORCE_NUGET_EXE_INTERACTIVE*。 如果您发现该 nuget.exe 不同计算机之间的行为方式不同，环境变量可能是可能的原因。 例如，Azure Web 应用 Kudu （在部署期间使用） 具有*NUGET_XMLDOC_MODE*设置为*跳过*加快包还原性能并节省磁盘空间。

| 变量 | 描述 | 备注 |
| --- | --- | --- |
| http_proxy | 用于 NuGet HTTP 操作的 http 代理。 | 这将指定为`http://<username>:<password>@proxy.com`。 |
| no_proxy | 配置从使用代理跳过的域。 | 指定为用逗号 （，） 分隔的域。 |
| EnableNuGetPackageRestore | 如果 NuGet 应隐式授予同意的情况下，如果需要在还原包用于的标志。 | 指定的标志将被视为*true*或*1*，未设置视为标志的任何其他值。 |
| NUGET_EXE_NO_PROMPT | 会使该 exe 用于提示输入凭据。 | 任何值，除了 null 或空字符串将被视为此标记集/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 要强制交互模式的全局环境变量。 | 任何值，除了 null 或空字符串将被视为此标记集/true。 |
| NUGET_PACKAGES | 路径以用于*全局包*文件夹上所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定为绝对路径。 |
| NUGET_FALLBACK_PACKAGES | 全局回退包文件夹。 | 用分号 （;） 分隔的绝对文件夹路径。 |
| NUGET_HTTP_CACHE_PATH | 路径以用于*http 缓存*文件夹上所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定为绝对路径。 |
| NUGET_PERSIST_DG | 标志指示是否应保持 dg 文件 （MSBuild 中收集的数据）。 | 指定为*true*或*false* （默认），如果 NUGET_PERSIST_DG_PATH 未设置将存储到临时目录 （NuGetScratch 文件夹当前环境临时目录中）。 |
| NUGET_PERSIST_DG_PATH | 若要保留 dg 文件的路径。 | 指定为绝对路径，此选项是时才使用*NUGET_PERSIST_DG*设置为 true。 |
| NUGET_RESTORE_MSBUILD_ARGS | 设置其他 MSBuild 自变量。 | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 设置 MSBuild 日志详细信息。 | 默认值是*quiet* ("/ v: q")。 可能的值*q [uiet]*， *m [最低]*， *n [ormal]*， *d [etailed]*，和*diag [nostic]*。 |
| NUGET_SHOW_STACK | 确定是否应该向用户显示完整的异常 （包括堆栈跟踪）。 | 指定为*true*或*false* （默认值）。 |
| NUGET_XMLDOC_MODE | 确定应如何处理程序集 XML 文档文件提取。 | 支持的模式为*跳过*（不提取 XML 文档文件），*压缩*（作为 zip 存档中存储 XML 文档文件） 或*无*（默认值为，将 XML 文档文件视为常规文件）。 |
