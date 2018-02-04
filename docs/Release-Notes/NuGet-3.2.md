---
title: "NuGet 3.2 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.2 的发行说明。"
keywords: "NuGet 3.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1728a5c0d83be84686e7ab1394cfc4f8f809987c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-32-release-notes"></a><span data-ttu-id="e1117-104">NuGet 3.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="e1117-104">NuGet 3.2 Release Notes</span></span>

<span data-ttu-id="e1117-105">[NuGet 3.2 RC 发行说明](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="e1117-105">[NuGet 3.2-RC Release Notes](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md)</span></span>

<span data-ttu-id="e1117-106">发布 NuGet 3.2 2015 年 9 月 16 日的改进和修补程序 3.1.1 集合释放并从这两个可用[dist.nuget.org](http://dist.nuget.org/index.html)和[Visual Studio 库](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)。</span><span class="sxs-lookup"><span data-stu-id="e1117-106">NuGet 3.2 was released September 16, 2015 as a collection of improvements and fixes for the 3.1.1 release and is available from both [dist.nuget.org](http://dist.nuget.org/index.html) and the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).</span></span>

## <a name="new-features"></a><span data-ttu-id="e1117-107">新增功能</span><span class="sxs-lookup"><span data-stu-id="e1117-107">New Features</span></span>

* <span data-ttu-id="e1117-108">实时所在的文件夹中的项目现在可以具有不同`project.json`该特定于每个项目的文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="e1117-108">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="e1117-109">对于每个项目，将`project.json`文件`{ProjectName}.project.json`，NuGet 会相应地提供对该配置的每个项目的首选项。</span><span class="sxs-lookup"><span data-stu-id="e1117-109">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will give preference to that configuration for each project appropriately.</span></span>  <span data-ttu-id="e1117-110">这唯一支持与 Windows 10 工具 1.1 版安装- [1102年](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="e1117-110">This is only supported with Windows 10 Tools v1.1 installed -  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="e1117-111">NuGet 客户端支持指定全局 NUGET_PACKAGES 环境变量指定的位置中使用的共享全局包文件夹`project.json`托管与 Windows 10 工具 1.1 版的项目。</span><span class="sxs-lookup"><span data-stu-id="e1117-111">NuGet clients support specifying a global NUGET_PACKAGES environment variable to specify the location of the shared global packages folder used in `project.json` managed projects with Windows 10 tools v1.1.</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="e1117-112">命令行的更新</span><span class="sxs-lookup"><span data-stu-id="e1117-112">Command-line updates</span></span>

<span data-ttu-id="e1117-113">这是支持的 NuGet v3 服务器的 nuget.exe 客户端的第一个版本，并且还原项目包使用托管`project.json`文件。</span><span class="sxs-lookup"><span data-stu-id="e1117-113">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

<span data-ttu-id="e1117-114">没有大量的经过身份验证的源问题已解决在此版本中以提高与客户端交互。</span><span class="sxs-lookup"><span data-stu-id="e1117-114">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="e1117-115">安装 / 还原交互仅提交到经过身份验证数据源的初始请求凭据[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="e1117-115">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="e1117-116">推送命令不能解决从配置的凭据[1248年](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="e1117-116">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="e1117-117">用户代理和标头现在提交到 NuGet 存储库有助于统计信息跟踪- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="e1117-117">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

<span data-ttu-id="e1117-118">我们做了大量改进，可尝试使用远程的 NuGet 存储库时更好地处理网络故障：</span><span class="sxs-lookup"><span data-stu-id="e1117-118">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="e1117-119">改进错误消息时无法连接到远程源- [1238年](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="e1117-119">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="e1117-120">更正了 NuGet 还原命令时出现错误条件的正确返回 1 [1186年](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="e1117-120">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="e1117-121">现在重试网络连接最多 5 次尝试 HTTP 5xx 失败-对于每个 200ms年[1120年](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="e1117-121">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="e1117-122">改进的服务器重定向响应处理期间推送命令- [1051年](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="e1117-122">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="e1117-123">`nuget install -source`现在支持从作为自变量-Nuget.Config 的 URL 或存储库名称[1046年](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="e1117-123">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="e1117-124">缺少的程序包在还原过程中不存储库位于现在报告为错误而不是警告[1038年](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="e1117-124">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="e1117-125">更正的 Unix/Linux 方案-\r\n multipartwebrequest 处理[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="e1117-125">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

<span data-ttu-id="e1117-126">有大量的各种命令出现问题的修复：</span><span class="sxs-lookup"><span data-stu-id="e1117-126">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="e1117-127">推送命令不会再之前对包源-PUT GET [1237年](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="e1117-127">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="e1117-128">列表命令不再重复版本号- [1185年](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="e1117-128">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="e1117-129">包使用的生成参数现在正确支持 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="e1117-129">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="e1117-130">已更正的问题，尝试包 F # 项目生成使用 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)</span><span class="sxs-lookup"><span data-stu-id="e1117-130">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="e1117-131">当包已经存在-还原现在否 ops [1040年](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="e1117-131">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="e1117-132">改进的错误消息时`packages.config`文件格式不正确- [1034年](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="e1117-132">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="e1117-133">更正带-SolutionDirectory 交换机还原命令，可以使用相对路径- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="e1117-133">Corrected restore command with -SolutionDirectory switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="e1117-134">改进的更新命令，以支持解决方案范围更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="e1117-134">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="e1117-135">在 NuGet GitHub 中找不到在此版本中解决的问题的完整列表[命令行里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。</span><span class="sxs-lookup"><span data-stu-id="e1117-135">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="e1117-136">Visual Studio 扩展更新</span><span class="sxs-lookup"><span data-stu-id="e1117-136">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="e1117-137">Visual Studio 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e1117-137">New Features in Visual Studio</span></span>

* <span data-ttu-id="e1117-138">新的上下文菜单项已添加到解决方案资源管理器使包得以还原而不生成解决方案的解决方案节点上 ([1274年](https://github.com/NuGet/Home/issues/1274))。</span><span class="sxs-lookup"><span data-stu-id="e1117-138">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新还原包上下文菜单项](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="e1117-140">更新和修补在 Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="e1117-140">Updates and Fixes in Visual Studio</span></span>

<span data-ttu-id="e1117-141">经过身份验证的源的修补程序汇总中的扩展以及解决。</span><span class="sxs-lookup"><span data-stu-id="e1117-141">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="e1117-142">以下身份验证项还已扩展中得到解决:</span><span class="sxs-lookup"><span data-stu-id="e1117-142">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="e1117-143">现在正确将 NuGet v3 正确，身份验证源而不是 v2 已经过身份验证源- [1216年](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="e1117-143">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="e1117-144">在项目中使用的身份验证凭据的已更正的请求`project.json`以及与 v2 馈送-通信[1082年](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="e1117-144">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

<span data-ttu-id="e1117-145">网络连接有影响的用户界面在 Visual Studio 中，并且我们使用了下列修补程序来解决此：</span><span class="sxs-lookup"><span data-stu-id="e1117-145">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="e1117-146">改进的包版本的本地缓存维护[1096年](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="e1117-146">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="e1117-147">连接到源不再尝试将其视为 v2 源-v3 时更改失败行为[1253年](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="e1117-147">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="e1117-148">现在阻止安装失败时使用多个包源的安装包[1183年](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="e1117-148">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="e1117-149">我们改进与生成操作的交互的处理：</span><span class="sxs-lookup"><span data-stu-id="e1117-149">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="e1117-150">现在继续生成项目，如果为单个项目失败-还原包[1169年](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="e1117-150">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="e1117-151">将包安装到解决方案中的另一个项目依赖于项目强制解决方案重新生成的[981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="e1117-151">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="e1117-152">更正失败的包安装到项目的正确回滚更改[1265年](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="e1117-152">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="e1117-153">更正无意中的删除`developmentDependency`属性中的包`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)</span><span class="sxs-lookup"><span data-stu-id="e1117-153">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="e1117-154">调用`install.ps1`现在拥有适当的`$package.AssemblyReferences`传递的对象[1245年](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="e1117-154">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="e1117-155">处于错误状态的项目时的 UWP 项目中的包不再阻止卸载[1128年](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="e1117-155">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="e1117-156">包含多种解决方案`packages.config`和`project.json`而无需第二个现在正确生成项目生成操作- [1122年](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="e1117-156">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="e1117-157">如果链接或位于不同的文件夹的正确定位 app.config 文件[1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="e1117-157">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="e1117-158">UWP 项目现在可以安装未列出的包- [1109年](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="e1117-158">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="e1117-159">虽然解决方案并不处于保存状态的程序包还原现在允许[1081年](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="e1117-159">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>

<span data-ttu-id="e1117-160">处理对配置文件已更正的更新：</span><span class="sxs-lookup"><span data-stu-id="e1117-160">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="e1117-161">从上的后续版本的包不能再删除的目标文件传递`project.json`托管的项目- [1288年](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="e1117-161">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="e1117-162">无法再在 ASP.NET 5 解决方案生成的期间修改 Nuget.Config 文件[1201年](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="e1117-162">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="e1117-163">允许包更新的过程中无法再更改版本约束[1130年](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="e1117-163">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="e1117-164">锁定文件现在继续处于锁定状态生成的期间[1127年](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="e1117-164">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="e1117-165">正在修改`packages.config`和不在更新的过程中重写该[585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="e1117-165">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>

<span data-ttu-id="e1117-166">与 TFS 源代码管理的交互将有所改进：</span><span class="sxs-lookup"><span data-stu-id="e1117-166">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="e1117-167">不再失败的包的绑定到 TFS 的安装[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)</span><span class="sxs-lookup"><span data-stu-id="e1117-167">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="e1117-168">已更正的 NuGet 用户界面，以允许 TFS 2013 集成- [1071年](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="e1117-168">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="e1117-169">更正对包还原正确来自的包文件夹的引用[1004年](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="e1117-169">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="e1117-170">最后，我们还改进这些项：</span><span class="sxs-lookup"><span data-stu-id="e1117-170">Finally, we also improved these items:</span></span>

* <span data-ttu-id="e1117-171">针对日志消息的详细程度减小`project.json`托管项目的[1163年](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="e1117-171">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="e1117-172">现在在用户界面中的正确显示安装的包版本[1061年](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="e1117-172">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>
* <span data-ttu-id="e1117-173">依赖项范围中其 nuspec 现在指定的包具有的稳定的包版本的安装这些依赖项预发行版本[1304年](https://github.com/NuGet/Home/issues/1304)</span><span class="sxs-lookup"><span data-stu-id="e1117-173">Packages with dependency ranges specified in their nuspec now have pre-release versions of those dependencies installed for a stable package version - [1304](https://github.com/NuGet/Home/issues/1304)</span></span>

<span data-ttu-id="e1117-174">问题解决有关在 NuGet GitHub 中找不到 Visual Studio 扩展的完整列表[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="e1117-174">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="e1117-175">已知问题</span><span class="sxs-lookup"><span data-stu-id="e1117-175">Known Issues</span></span>

<span data-ttu-id="e1117-176">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="e1117-176">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>