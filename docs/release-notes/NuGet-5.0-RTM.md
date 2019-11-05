---
title: NuGet 5.0 RTM 发行说明
description: NuGet 5.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611337"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本16。0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 版本16.0。4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装 

<sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装

## <a name="summary-whats-new-in-50"></a>摘要：5.0 中的新增功能

* 支持在 Visual Studio 2019 中还原[筛选的解决方案](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019)- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` 文件夹使包能够以可传递的目标/属性到主机项目- [#6091](https://github.com/NuGet/Home/issues/6091)
* 更好地支持 NuGet IVs Api 中的 PackageReference 方案- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 已弃用- [#7928](https://github.com/NuGet/Home/issues/7928)
* 第1代凭据提供程序插件已被[gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)取代，即将弃用- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 执行 NoOp 还原时，请避免在 obj 目录中写入 dgspec [#7854](https://github.com/NuGet/Home/issues/7854)

* 在 ~/.nuget 中创建的文件的权限过于打开- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 不适用于需要身份验证[#7605](https://github.com/NuGet/Home/issues/7605)的源

* VisualStudio。 IVsPackageInstaller-对没有包引用的项目调用始终使用 package，即使默认设置为 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC：更新包重新安装在 delisted 包上失败（"找不到包"）。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* 在我们的存储库和 VSIX 中添加第三方通知- [#7409](https://github.com/NuGet/Home/issues/7409)

* 如果未指定版本，则 VisualStudio 应安装最新版本[#7493](https://github.com/NuGet/Home/issues/7493)

* --交互式支持 dotnet nuget 推送[#7519](https://github.com/NuGet/Home/issues/7519)

* 当还原时，不应引发 NU1603 警告。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* 在还原过程中 NuGet 不应打印项目路径[#7647](https://github.com/NuGet/Home/issues/7647)

* --交互式支持 dotnet 删除包- [#7727](https://github.com/NuGet/Home/issues/7727)

* 添加 back Nuget.exe with TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 需要更短的路径才能正常工作[#7770](https://github.com/NuGet/Home/issues/7770)

* 如果用户没有请求特定的 msbuild 版本，则首选 msbuild 发现的路径- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet （498，5）：错误：找不到路径 "/tmp/NuGetScratch" 的一部分[#7793](https://github.com/NuGet/Home/issues/7793)

* 还原不必要地枚举计算机缓存中引用包的所有版本的内容- [#7639](https://github.com/NuGet/Home/issues/7639)

* 在安装 VS 2019 Preview 后，MSBuild 自动检测始终会选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* 解决方案中的 dotnet 列表包输出框架[#7607](https://github.com/NuGet/Home/issues/7607)的重复条目

* 在旧项目和包文件夹中调用 IVsPackageInstaller 时，异常 "空路径名称不合法"。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild/t：还原最少详细级别应该更小- [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 的 NuGet UI 由于颜色问题而无法读取选项卡- [#7735](https://github.com/NuGet/Home/issues/7735)

* Nuget.exe & NuGet。客户端许可证 .txt 说明- [#7629](https://github.com/NuGet/Home/issues/7629)

* 还原不必要地枚举全局包文件夹，尝试确定类型[#7596](https://github.com/NuGet/Home/issues/7596)

* 锁定文件强制执行的错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修复 NuGet。配置问题- [#7326](https://github.com/NuGet/Home/issues/7326)

* 适应 MSBuild 更新其安装位置- [#7325](https://github.com/NuGet/Home/issues/7325)

* Nuget.exe 应为开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)

* 添加包扩展点以包括调试符号- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 应保留创建的 nupkg 中的依赖项版本范围（即使使用了浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* 当用户级配置还具有源[#7209](https://github.com/NuGet/Home/issues/7209)时，对通过身份验证的源的 `dotnet restore` 失败

* 包不应限制内容文件的 BuildActions 集- [#7155](https://github.com/NuGet/Home/issues/7155)

* 使用需要 AssetTargetFallback 成功的 ProjectReference 会发出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 由于调用 CPS （CommonProjectSystem）时线程问题导致死锁- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 不会对本地配置中指定的源使用来自全局配置的凭据- [#6935](https://github.com/NuGet/Home/issues/6935)

* 在异步代码路径上调用 MEF 的线程问题- [#6771](https://github.com/NuGet/Home/issues/6771)

* 签名：错误报告了两次，没有调用堆栈- [#6455](https://github.com/NuGet/Home/issues/6455)

* 安装带有不受信任签名证书的签名包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)

* 当2个项目共享 obj 目录时，NuGet 还原 Noop 错误- [#6114](https://github.com/NuGet/Home/issues/6114)

* 在 Linux 上，不能将 PAT `dotnet restore` 与来自已验证源的包结合使用- [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore 因禁用了计算机范围的源而失败- [#5410](https://github.com/NuGet/Home/issues/5410)

**Dcr**

* 以后删除 "dotnet pack" 时警告- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* 为 Gen1 credential 插件添加弃用警告- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 签名：启用的存储库需要将每个包的客户端验证为签名[#7759](https://github.com/NuGet/Home/issues/7759)的存储库

* 通过 NuGet 限制每个源的 http 请求数- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet 应面向 Net472 （以帮助清理 VSIX 的16.0 版本）- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC：删除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 将 NetCoreApp 3.0 映射到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 将 netstandard 2.0 支持添加到 NuGet。 * 包- [#6516](https://github.com/NuGet/Home/issues/6516)

* 允许包作者定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)

* 支持 VS 2019 解决方案筛选器功能。 还支持不在解决方案中的项目或已卸载的项目。 需要首先还原完整解决方案（通过 CLI 或 VS） [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0 程序集需要 .NET 4.7.2 （通过 TFM 更改）- [#7510](https://github.com/NuGet/Home/issues/7510)

* 从 NuGet NuGetLicenseData。打包应为公共类型。 从 spdx 更新许可证元数据引入。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 删除过时的设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 具有1个 cpu [#6742](https://github.com/NuGet/Home/issues/6742)的系统上的解决方法还原超时

* NuGet 首选 NTLM 身份验证，即使在 NuGet 中有凭据-添加配置选项来筛选凭据的身份验证类型- [#5286](https://github.com/NuGet/Home/issues/5286)

* 启用用于 PackageReference 的 EmbedInteropTypes （匹配的包 .Config 功能）- [#2365](https://github.com/NuGet/Home/issues/2365)

**[此版本中已修复的所有问题的列表-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>摘要：5.0.2 中的新增功能

* 安全（当通过 dotnet 或 cscript.exe 运行时）-应创建具有正确权限的 obj 文件夹[#7908](https://github.com/NuGet/Home/issues/7908)

* mono/MacOS 上的 nuget.exe 还原失败，并出现自定义 nuget .config 和 `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>已知问题

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>问题
使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。 也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。<br>
#### <a name="workaround"></a>解决方法
通过将 `RestoreAdditionalProjectSources` 设置为 "无"，禁用回退文件夹的使用：

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

请谨慎使用这一点，因为现在将从 NuGet.org 下载从回退文件夹还原的包。
