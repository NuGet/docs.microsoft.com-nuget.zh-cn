---
title: NuGet 5.0 预览版发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 预览版的发行说明。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084933"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 预览版发行说明

## <a name="summary-whats-new-in-50-preview-2"></a>摘要:什么是 5.0 预览版 2 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

#### <a name="bugs"></a>Bug:

* VS 16.0 的 NuGet UI 具有不可读的选项卡颜色问题-由于[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core 和 NuGet.Clients License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)

* 还原不必要地枚举全局包文件夹中尝试确定类型- [#7596](https://github.com/NuGet/Home/issues/7596)

* 从锁定文件强制错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修复 NuGet.Configuration 问题- [#7326](https://github.com/NuGet/Home/issues/7326)

* 适应 MSBuild 更新的安装位置。  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 应该是开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)

* 添加包扩展点包括调试符号的[#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet 包应保留在创建 nupkg 的依赖项版本范围。 （即使使用浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* 用户级配置还具有源-已经过身份验证源失败 dotnet 还原[#7209](https://github.com/NuGet/Home/issues/7209)

* 包不应限制的内容文件-BuildActions 套[#7155](https://github.com/NuGet/Home/issues/7155)

* 使用 projectreference，这要求 AssetTargetFallback 成功，应发出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 由于线程问题到 CPS (CommonProjectSystem) 的调用时的死锁[#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet 添加包不会用于本地配置-中指定的源的凭据从全局配置[#6935](https://github.com/NuGet/Home/issues/6935)

* 线程处理问题与 MEF 正在调用异步代码- [#6771](https://github.com/NuGet/Home/issues/6771)

* 签名： 报告两次，而无需调用堆栈的错误[#6455](https://github.com/NuGet/Home/issues/6455)

* 使用不受信任的签名证书安装已签名的包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet 还原不正确 Noop 当 2 个项目共享 obj 目录- [#6114](https://github.com/NuGet/Home/issues/6114)

* 使用 Linux 上使用已经过身份验证源-中的包的 dotnet 还原不能使用 PAT [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 还原由于已禁用计算机范围源-而失败[#5410](https://github.com/NuGet/Home/issues/5410)

#### <a name="dcrs"></a>DCR

* NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)

* 从 NuGet.Packaging NuGetLicenseData 应为公共类型。 更新许可证元数据从 spdx 引入。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)

[在此版本 5.0.0-preview2 中修复所有问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a>已知问题

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive 在 Mac 上抛出错误。 - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>问题
`--interactive` 参数无法由 dotnet cli 转发，因此导致错误 `error: Missing value for option 'interactive'` 出现

#### <a name="workaround"></a>解决方法
将 interactive 选项与其他任何 dotnet 命令一起运行（如 `dotnet restore --interactive`），并进行身份验证。 凭据提供程序可能会缓存身份验证。 然后，运行 `dotnet nuget push`。

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。 - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>问题
使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。 也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。

#### <a name="workaround"></a>解决方法
通过将 `RestoreAdditionalProjectSources` 设置为无，禁用回退文件夹。 请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。
