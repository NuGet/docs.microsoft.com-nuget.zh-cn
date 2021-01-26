---
title: NuGet CLI 环境变量
description: nuget.exe 环境变量的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779381"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 环境变量

可以通过多个环境变量来配置 nuget.exe CLI 的行为，这会影响计算机范围、用户或进程级别 nuget.exe。 环境变量始终覆盖文件中的任何设置 `NuGet.Config` ，允许生成服务器更改适当的设置，而无需修改任何文件。

一般情况下，直接在命令行上或在 NuGet 配置文件中指定的选项优先，但有一些例外，如 *FORCE_NUGET_EXE_INTERACTIVE*。 如果发现 nuget.exe 在不同的计算机之间行为不同，则可能是环境变量。 例如，在部署期间使用的 Azure Web 应用 Kudu () *NUGET_XMLDOC_MODE* 设置为 " *跳过* " 以加快包还原性能并节省磁盘空间。

NuGet CLI 使用 MSBuild 读取项目文件。 在 MSBuild 计算期间，所有环境变量都作为 [属性](/visualstudio/msbuild/msbuild-command-line-reference) 提供。
[NuGet 包和还原为 MSBuild 目标](../msbuild-targets.md#restore-properties)中记录的属性列表也可以设置为环境变量。

| 变量 | 说明 | 备注 |
| --- | --- | --- |
| http_proxy | 用于 NuGet HTTP 操作的 Http 代理。 | 这将指定为 `http://<username>:<password>@proxy.com` 。 |
| no_proxy | 将使用代理的域配置为绕过。 | 指定为以逗号分隔的域 (，) 。 |
| EnableNuGetPackageRestore | 如果 NuGet 在还原时需要此权限，NuGet 应隐式授予同意。 | 指定标志被视为 *true* 或 *1*，其他任何值视为标志未设置。 |
| NUGET_EXE_NO_PROMPT | 阻止 exe 提示输入凭据。 | Null 或空字符串以外的任何值都将被视为此标志设置/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 强制交互模式的全局环境变量。 | Null 或空字符串以外的任何值都将被视为此标志设置/true。 |
| NUGET_PACKAGES | 用于 *全局包* 文件夹的路径，如 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。 | 指定为绝对路径。 |
| NUGET_FALLBACK_PACKAGES | 全局备用包文件夹。 | 用分号分隔的绝对文件夹路径 (; ) 。 |
| NUGET_HTTP_CACHE_PATH | 用于 *http 缓存* 文件夹的路径，如 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。 | 指定为绝对路径。 |
| NUGET_PERSIST_DG | 一个标志，用于指示是否应保留 (从 MSBuild) 收集的数据。 | 指定为 " *true* " 或 " *false* " (默认) ，如果 NUGET_PERSIST_DG_PATH 未设置，则将存储到当前) 环境中的临时目录 (NuGetScratch 文件夹中。 |
| NUGET_PERSIST_DG_PATH | 持久保存 dg 文件的路径。 | 指定为绝对路径，仅当 *NUGET_PERSIST_DG* 设置为 true 时才使用此选项。 |
| NUGET_RESTORE_MSBUILD_ARGS | 设置其他 MSBuild 参数。 | 传递参数的方式与将其传递到 msbuild.exe 的方式相同。 将项目属性 "Foo" 从命令行设置为值栏的示例如下所示： Foo = Bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 设置 MSBuild 日志详细级别。 | 默认值为 *quiet* ( "/v： q" ) 。 可能的值 *q [uiet]*、 *m [inimal]*、 *n [ormal]*、 *d [etailed]* 和 *诊断 [nostic]*。 |
| NUGET_SHOW_STACK | 确定是否应向用户显示 (包含 stack 跟踪) 的完整异常。 | 指定为 *true* 或 *false* (默认) 。 |
| NUGET_XMLDOC_MODE | 确定如何处理程序集 XML 文档文件提取。 | 支持的模式为 *skip* (不要提取 xml 文档文件) 、 *压缩* (将 xml 文档文件存储为 zip 存档) 或 *none* (默认情况下，将 xml 文档文件视为常规文件) 。 |
| NUGET_CERT_REVOCATION_MODE | 确定用于对包进行签名的证书的吊销状态检查如何在安装或还原已签名的包时执行。 如果未设置，则默认为 `online` 。| 可能的值 *联机* (默认) *脱机*。  与[NU3028](../errors-and-warnings/NU3028.md)相关 |

