---
title: NuGet 5.0 预览版发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 预览版的发行说明。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196195"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 预览版发行说明

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 预览版本

* 2010 年 2 月 27 日- [NuGet 5.0 预览版 4](#summary-whats-new-in-50-preview-4)
* 2019 年 2 月 13 日- [NuGet 5.0 预览版 3](#summary-whats-new-in-50-preview-3)
* 2019 年 1 月 23 日- [NuGet 5.0 预览版 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-4"></a>摘要:什么是 NuGet 5.0 预览版 4 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug:**

* NuGet.VisualStudio.IVsPackageInstaller-调用上使用的任何包的项目引用始终使用 packages.config，即使默认值设置为 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC:更新包从列表去除包上重新安装失败 （"找不到包"）。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* 在我们的存储库和 VSIX 中-添加第三方通知[#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage 应安装最新版本时提供的任何版本[#7493](https://github.com/NuGet/Home/issues/7493)

* -dotnet nuget push 交互式支持- [#7519](https://github.com/NuGet/Home/issues/7519)

* 当还原锁定文件时，不应引发 NU1603 警告。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet 应使用最小日志记录-还原期间无法打印项目路径[#7647](https://github.com/NuGet/Home/issues/7647)

* -适用于 dotnet 的交互支持中删除程序包- [#7727](https://github.com/NuGet/Home/issues/7727)

* 添加与 TypeForwardedTo attrs-备份 NuGet.Packaging.Core [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 需要较短的路径来有效工作的[#7770](https://github.com/NuGet/Home/issues/7770)

* 如果用户未请求特定的 msbuild 版本-则更喜欢 msbuild 发现路径[#7786](https://github.com/NuGet/Home/issues/7786)

**Dcr:**

* 限制每个源通过 NuGet.Config 的 http 请求数目[#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet 应针对 Net472 （以帮助清理 16.0 生成的 VSIX）- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC:删除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 请 NetCoreApp 3.0 映射到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 将 netstandard2.0 支持添加到 NuGet.* 包- [#6516](https://github.com/NuGet/Home/issues/6516)


## <a name="summary-whats-new-in-nuget-50-preview-3"></a>摘要:什么是 NuGet 5.0 预览版 3 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题 

**Bug:**

* nuget.exe /? 应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5)： 错误：找不到部分路径 / tmp/NuGetScratch-mono-上[#7793](https://github.com/NuGet/Home/issues/7793)

* 还原不必要地枚举在计算机缓存中的引用包的所有版本的内容[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild 自动检测后安装与 2019年预览-始终选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* 一种解决方案上的 dotnet 列表包输出的框架的重复条目[#7607](https://github.com/NuGet/Home/issues/7607)

* 异常"空路径名称不是合法的"时调用 IVsPackageInstaller.InstallPackage 上旧项目和包文件夹不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore 最低详细级别应为更少的[#4695](https://github.com/NuGet/Home/issues/4695)

**Dcr:**

* 允许程序包作者可定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)

* 启用在 VS 成功如果项目不是解决方案的一部分或未加载，但以前已还原的还原[#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>摘要:什么是 5.0 预览版 2 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug:**

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

**Dcr:**

* NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)

* 从 NuGet.Packaging NuGetLicenseData 应为公共类型。 更新许可证元数据从 spdx 引入。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)

[在此版本 5.0.0-preview2 中修复所有问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>已知问题

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。 - [#7414](https://github.com/NuGet/Home/issues/7414)
**问题**使用 dotnet.exe 时 2.x 以还原项目的多重目标 netcoreapp 1.x 和 netcoreapp 2.x，回退文件夹视为文件源。 也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。
**解决方法**通过设置来禁用回退文件夹的使用情况`RestoreAdditionalProjectSources`为 nothing。 请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。
