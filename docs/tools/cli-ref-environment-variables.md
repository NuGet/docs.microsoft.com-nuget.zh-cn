---
title: NuGet CLI 环境变量
description: Nuget.exe 环境变量的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9f26f75a70a996cad158fd125e86d98e10c3dac1
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610638"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 环境变量

Nuget.exe CLI 的行为可以通过许多环境变量，这会影响计算机范围的用户的 nuget.exe 或处理级别配置。 环境变量始终重写中的任何设置`NuGet.Config`文件，从而使生成服务器，而无需修改任何文件更改相应设置。

一般情况下，直接在命令行上或在 NuGet 配置文件中指定的选项具有优先级，但如有少数例外情况之外*FORCE_NUGET_EXE_INTERACTIVE*。 如果您发现该 nuget.exe 以不同的方式不同的计算机之间的行为，环境变量可能是原因。 例如，具有 （部署过程中使用） 的 Azure Web 应用 Kudu *NUGET_XMLDOC_MODE*设置为*跳过*包还原的性能提高的速度和节省磁盘空间。

NuGet CLI 使用 MSBuild 来读取项目文件。 所有环境变量都都可用作[属性](/visualstudio/msbuild/msbuild-command-line-reference)MSBuild 评估期间。
说明中的属性列表[NuGet 包和作为 MSBuild 目标还原](../reference/msbuild-targets.md#restore-properties)也可设置为环境变量。

| 变量 | 描述 | 备注 |
| --- | --- | --- |
| http_proxy | 用于 NuGet HTTP 操作的 http 代理。 | 这会指定为`http://<username>:<password>@proxy.com`。 |
| no_proxy | 配置从使用代理服务器绕过的域。 | 指定为逗号 （，） 分隔的域。 |
| EnableNuGetPackageRestore | 如果 NuGet 应隐式授予同意的情况下，如果所需在还原包标记的。 | 指定的标志将被视为 *，则返回 true*或*1*，未设置任何其他值视为标志。 |
| NUGET_EXE_NO_PROMPT | 可以防止会提示输入凭据的 exe。 | 除了 null 或空字符串将被视为任何值这样的标记集/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 若要强制交互模式下的全局环境变量。 | 除了 null 或空字符串将被视为任何值这样的标记集/true。 |
| NUGET_PACKAGES | 要用于路径*全局包*文件夹中，如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定为绝对路径。 |
| NUGET_FALLBACK_PACKAGES | 回退的全局包文件夹。 | 以分号 （;） 分隔的绝对文件夹路径。 |
| NUGET_HTTP_CACHE_PATH | 要用于路径*http 缓存*文件夹中，如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定为绝对路径。 |
| NUGET_PERSIST_DG | 标志，用于指示是否应保留 dg 文件 （通过 MSBuild 收集的数据）。 | 指定作为 *，则返回 true*或*false* （默认值），如果未设置 NUGET_PERSIST_DG_PATH 将存储到临时目录 （NuGetScratch 文件夹当前环境的临时目录中）。 |
| NUGET_PERSIST_DG_PATH | 若要持久保存 dg 文件的路径。 | 指定为绝对路径，此选项是时，才使用*NUGET_PERSIST_DG*设置为 true。 |
| NUGET_RESTORE_MSBUILD_ARGS | 设置其他 MSBuild 参数。 | 将参数传递到如何你会将其传递给 msbuild.exe 完全相同。 从命令行的 Foo 的项目属性设置为值栏的一个示例是 /p:Foo = 栏 |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 设置 MSBuild 日志详细信息。 | 默认值是*安静*("/ v: q")。 可能的值*q [uiet]*， *m [inimal]*， *n [ormal]*， *d [etailed]*，并*diag [nostic]*。 |
| NUGET_SHOW_STACK | 确定是否应该向用户显示完整的异常 （包括堆栈跟踪）。 | 指定作为 *，则返回 true*或*false* （默认值）。 |
| NUGET_XMLDOC_MODE | 确定应如何处理程序集 XML 文档文件解压缩。 | 支持的模式包括*跳过*（不提取 XML 文档文件），请*压缩*（作为 zip 存档中存储 XML 文档文件） 或*none* （默认值，将 XML 文档文件视为常规文件）。 |
| NUGET_CERT_REVOCATION_MODE | 确定用于对包进行签名的证书的吊销状态检查的方式，将已签名的包安装或还原时执行。 未设置时，默认为`online`。| 可能的值*在线*（默认值），*脱机*。  与相关[NU3028](../reference/errors-and-warnings/NU3028.md) |

