---
title: NuGet CLI 环境变量
description: 针对 nuget.exe 环境变量的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327824"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 环境变量

可以通过多个环境变量来配置 nuget.exe CLI 的行为, 这会影响计算机范围、用户或进程级别上的 nuget.exe。 环境变量始终覆盖文件中`NuGet.Config`的任何设置, 允许生成服务器更改适当的设置, 而无需修改任何文件。

一般情况下, 直接在命令行上或在 NuGet 配置文件中指定的选项优先, 但有一些例外, 如*FORCE_NUGET_EXE_INTERACTIVE*。 如果在不同的计算机之间发现 nuget.exe 的行为不同, 则可能是环境变量。 例如, 在部署期间使用的 Azure Web Apps Kudu 将*NUGET_XMLDOC_MODE*设置为 "*跳过*", 以加快包还原性能并节省磁盘空间。

NuGet CLI 使用 MSBuild 读取项目文件。 在 MSBuild 计算期间, 所有环境变量都作为[属性](/visualstudio/msbuild/msbuild-command-line-reference)提供。
[NuGet 包和还原为 MSBuild 目标](../msbuild-targets.md#restore-properties)中记录的属性列表也可以设置为环境变量。

| 变量 | 描述 | 备注 |
| --- | --- | --- |
| http_proxy | 用于 NuGet HTTP 操作的 Http 代理。 | 这将指定为`http://<username>:<password>@proxy.com`。 |
| no_proxy | 将使用代理的域配置为绕过。 | 指定为以逗号 (,) 分隔的域。 |
| EnableNuGetPackageRestore | 如果 NuGet 在还原时需要此权限, NuGet 应隐式授予同意。 | 指定标志被视为*true*或*1*, 其他任何值视为标志未设置。 |
| NUGET_EXE_NO_PROMPT | 阻止 exe 提示输入凭据。 | Null 或空字符串以外的任何值都将被视为此标志设置/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 强制交互模式的全局环境变量。 | Null 或空字符串以外的任何值都将被视为此标志设置/true。 |
| NUGET_PACKAGES | 用于*全局包*文件夹的路径, 如[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。 | 指定为绝对路径。 |
| NUGET_FALLBACK_PACKAGES | 全局备用包文件夹。 | 绝对文件夹路径, 用分号 (;) 分隔。 |
| NUGET_HTTP_CACHE_PATH | 用于*http 缓存*文件夹的路径, 如[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。 | 指定为绝对路径。 |
| NUGET_PERSIST_DG | 指示是否应持久保存 dg 文件 (从 MSBuild 收集的数据) 的标志。 | 指定为*true*或*false* (默认值), 如果未设置 NUGET_PERSIST_DG_PATH, 则将存储到临时目录 (当前环境 Temp 目录中的 NuGetScratch 文件夹)。 |
| NUGET_PERSIST_DG_PATH | 持久保存 dg 文件的路径。 | 指定为绝对路径, 仅当*NUGET_PERSIST_DG*设置为 true 时才使用此选项。 |
| NUGET_RESTORE_MSBUILD_ARGS | 设置其他 MSBuild 参数。 | 传递参数的方式与将它们传递给 msbuild.exe 的方式相同。 将项目属性 "Foo" 从命令行设置为值栏的示例如下所示: Foo = Bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 设置 MSBuild 日志详细级别。 | 默认值为*quiet* ("/v: q")。 可能的值*q [uiet]* 、 *m [inimal]* 、 *n [ormal]* 、 *d [etailed]* 和*诊断 [nostic]* 。 |
| NUGET_SHOW_STACK | 确定是否应向用户显示完全异常 (包括堆栈跟踪)。 | 指定为*true*或*false* (默认值)。 |
| NUGET_XMLDOC_MODE | 确定如何处理程序集 XML 文档文件提取。 | 支持的模式为*skip* (不提取 xml 文档文件),*压缩*(将 xml 文档文件存储为 zip 存档) 或*none* (默认情况下, 将 xml 文档文件视为常规文件)。 |
| NUGET_CERT_REVOCATION_MODE | 确定用于对包进行签名的证书的吊销状态检查如何在安装或还原已签名的包时执行。 如果未设置, 则默认`online`为。| 可能的值*联机*(默认值),*脱机*。  与[NU3028](../errors-and-warnings/NU3028.md)相关 |

