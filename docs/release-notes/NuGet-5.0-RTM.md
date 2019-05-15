---
title: NuGet 5.0 RTM 发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610663"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>随 Visual Studio 2019 一起安装.NET Core 工作负载 

<sup>2</sup>作为可选安装随.NET Core 工作负载的 Visual Studio 2019

## <a name="summary-whats-new-in-50"></a>摘要:什么是 5.0 中的新增功能

* 对还原的支持[筛选解决方案](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` 文件夹允许包来间接地参与到宿主项目中的目标/属性[#6091](https://github.com/NuGet/Home/issues/6091)
* 更好地支持 NuGet Iv Api-中的 PackageReference 方案[#7005](https://github.com/NuGet/Home/issues/7005)， [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 已弃用- [#7928](https://github.com/NuGet/Home/issues/7928)
* 第 1 代凭据提供程序插件已被[第 2 代](https://aka.ms/nuget-cross-platform-authentication-plugin)并且将很快被弃用的[#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 执行操作时 NoOp 还原，避免 *。 在 obj 目录-dgspec.json 写[#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget 内创建的文件的权限是太打开- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 不使用需要身份验证-源[#7605](https://github.com/NuGet/Home/issues/7605)

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

* `nuget.exe /?` 应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5)： 错误：找不到部分路径 / tmp/NuGetScratch-mono-上[#7793](https://github.com/NuGet/Home/issues/7793)

* 还原不必要地枚举在计算机缓存中的引用包的所有版本的内容[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild 自动检测后安装与 2019年预览-始终选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* 一种解决方案上的 dotnet 列表包输出的框架的重复条目[#7607](https://github.com/NuGet/Home/issues/7607)

* 异常"空路径名称不是合法的"时调用 IVsPackageInstaller.InstallPackage 上旧项目和包文件夹不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore 最低详细级别应为更少的[#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 的 NuGet UI 具有不可读的选项卡颜色问题-由于[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core 和 NuGet.Clients License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)

* 还原不必要地枚举全局包文件夹中尝试确定类型- [#7596](https://github.com/NuGet/Home/issues/7596)

* 从锁定文件强制错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修复 NuGet.Configuration 问题- [#7326](https://github.com/NuGet/Home/issues/7326)

* 适应 MSBuild 更新其安装位置- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 应该是开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)

* 添加包扩展点包括调试符号的[#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 应保留在创建 nupkg 的依赖项版本范围 （即使使用浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` 失败时用户级配置还具有源-已经过身份验证的源上[#7209](https://github.com/NuGet/Home/issues/7209)

* 包不应限制的内容文件-BuildActions 套[#7155](https://github.com/NuGet/Home/issues/7155)

* 使用 ProjectReference，这要求 AssetTargetFallback 成功，应发出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 由于线程问题到 CPS (CommonProjectSystem) 的调用时的死锁[#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 不会从全局配置的凭据用于在本地配置-中指定的源[#6935](https://github.com/NuGet/Home/issues/6935)

* 使用 MEF 上异步调用的线程问题的代码路径- [#6771](https://github.com/NuGet/Home/issues/6771)

* 签名： 报告两次，而无需调用堆栈的错误[#6455](https://github.com/NuGet/Home/issues/6455)

* 使用不受信任的签名证书安装已签名的包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet 还原不正确 Noop 当 2 个项目共享 obj 目录- [#6114](https://github.com/NuGet/Home/issues/6114)

* 不能使用与 PAT `dotnet restore` Linux 上的使用经过身份验证源-中的包[#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 还原由于已禁用计算机范围源-而失败[#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* 未来"dotnet 包 project.json"的删除，则发出警告[#7928](https://github.com/NuGet/Home/issues/7928)
 
* 添加对 Gen1 凭据插件-的弃用警告[#7819](https://github.com/NuGet/Home/issues/7819)
 
* 签名：已启用存储库，需要为存储库的客户端验证的每个包签名--通过 RepositorySignatures/5.0.0 资源- [#7759](https://github.com/NuGet/Home/issues/7759)

* 限制每个源通过 NuGet.Config 的 http 请求数目[#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet 应针对 Net472 （以帮助清理 16.0 生成的 VSIX）- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC:删除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 请 NetCoreApp 3.0 映射到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 将 netstandard2.0 支持添加到 NuGet.* 包- [#6516](https://github.com/NuGet/Home/issues/6516)

* 允许程序包作者可定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)

* 支持 VS 2019 解决方案筛选器功能。 此外支持项目不在解决方案中或已卸载的项目。 需要首先还原完整的解决方案 （通过 CLI 或 VS） [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)

* 从 NuGet.Packaging NuGetLicenseData 应为公共类型。 更新许可证元数据从 spdx 引入。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)

**[在此版本中-5.0 RTM 中已解决所有问题的列表](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>摘要:什么是 5.0.2 版中的新增功能

* （当通过 dotnet.exe 或 mono.exe 运行） 的安全性-应使用正确的权限创建 obj 文件夹[#7908](https://github.com/NuGet/Home/issues/7908)

* 在 mono/MacOS 上的 nuget.exe 还原失败，并自定义 nuget.config 并`PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>已知问题

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>问题
使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。 也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。<br>
#### <a name="workaround"></a>解决方法
通过设置来禁用回退文件夹的使用情况`RestoreAdditionalProjectSources`为 nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

因为现在会从 NuGet.org 下载包将从回退文件夹中还原，请谨慎使用此。
