---
title: NuGet 3.2 发行说明
description: NuGet 3.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780298"
---
# <a name="nuget-32-release-notes"></a><span data-ttu-id="c3d6d-103">NuGet 3.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="c3d6d-103">NuGet 3.2 Release Notes</span></span>

<span data-ttu-id="c3d6d-104">[NuGet 3.2-RC 发行说明](../release-notes/nuget-3.2-RC.md)  | [NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-104">[NuGet 3.2-RC Release Notes](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md)</span></span>

<span data-ttu-id="c3d6d-105">NuGet 3.2 于9月16日发布2015，作为3.1.1 版本的改进和修补程序的集合，可从 [dist.nuget.org](http://dist.nuget.org/index.html) 和 [Visual Studio 库](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)中获得。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-105">NuGet 3.2 was released September 16, 2015 as a collection of improvements and fixes for the 3.1.1 release and is available from both [dist.nuget.org](http://dist.nuget.org/index.html) and the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).</span></span>

## <a name="new-features"></a><span data-ttu-id="c3d6d-106">新功能</span><span class="sxs-lookup"><span data-stu-id="c3d6d-106">New Features</span></span>

* <span data-ttu-id="c3d6d-107">位于同一文件夹中的项目现在可以 `project.json` 在该文件夹中具有特定于每个项目的不同文件。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-107">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="c3d6d-108">对于每个项目，将文件命名为， `project.json` `{ProjectName}.project.json` NuGet 将相应地为每个项目的配置提供首选项。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-108">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will give preference to that configuration for each project appropriately.</span></span>  <span data-ttu-id="c3d6d-109">仅安装了 Windows 10 Tools v1.1- [1102](https://github.com/NuGet/Home/issues/1102)支持此项</span><span class="sxs-lookup"><span data-stu-id="c3d6d-109">This is only supported with Windows 10 Tools v1.1 installed -  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="c3d6d-110">NuGet 客户端支持指定全局 NUGET_PACKAGES 环境变量，以指定使用 `project.json` Windows 10 工具 v1.1 的托管项目中使用的共享全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-110">NuGet clients support specifying a global NUGET_PACKAGES environment variable to specify the location of the shared global packages folder used in `project.json` managed projects with Windows 10 tools v1.1.</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="c3d6d-111">命令行更新</span><span class="sxs-lookup"><span data-stu-id="c3d6d-111">Command-line updates</span></span>

<span data-ttu-id="c3d6d-112">这是 nuget.exe 客户端的第一个版本，它支持 NuGet v3 服务器，并为使用文件管理的项目还原包 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-112">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

<span data-ttu-id="c3d6d-113">在此版本中解决了许多经过身份验证的源问题，以改善与客户端的交互。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-113">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="c3d6d-114">安装/还原交互仅向经过身份验证的源的初始请求提交凭据- [1300](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-114">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="c3d6d-115">Push 命令不能解析配置中的凭据- [1248](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-115">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="c3d6d-116">用户代理和标头现在已提交到 NuGet 存储库以帮助进行统计跟踪- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-116">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

<span data-ttu-id="c3d6d-117">我们进行了大量改进，以便在尝试使用远程 NuGet 存储库时更好地处理网络故障：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-117">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="c3d6d-118">改善了无法连接到远程源时的错误消息- [1238](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-118">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="c3d6d-119">更正了 NuGet restore 命令，以便在出现错误情况时正确返回 1- [1186](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-119">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="c3d6d-120">现在，重试每个200毫秒的网络连接，在出现 HTTP 5xx 失败时最多执行5次尝试- [1120](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-120">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="c3d6d-121">改进了推送命令期间服务器重定向响应的处理- [1051](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-121">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="c3d6d-122">`nuget install -source` 现在支持作为参数的 Nuget.Config 中的 URL 或存储库名称- [1046](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-122">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="c3d6d-123">还原期间缺少存储库中的程序包现在会报告为错误，而不是警告 [1038](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-123">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="c3d6d-124">更正了针对 Unix/Linux 方案的 \r\n multipartwebrequest 处理- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-124">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

<span data-ttu-id="c3d6d-125">有多个针对各种命令的问题的修补程序：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-125">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="c3d6d-126">在针对包源进行 PUT 之前，推送命令不再执行 GET- [1237](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-126">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="c3d6d-127">List 命令不再重复版本号- [1185](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-127">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="c3d6d-128">带有-build 参数的 Pack 现在正确支持 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-128">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="c3d6d-129">更正了尝试打包使用 Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)生成的 F # 项目的问题</span><span class="sxs-lookup"><span data-stu-id="c3d6d-129">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="c3d6d-130">如果包已存在，则立即还原为非 ops- [1040](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-130">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="c3d6d-131">文件格式错误时改进的错误消息 `packages.config` - [1034](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-131">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="c3d6d-132">使用-SolutionDirectory 开关更正了 restore 命令，以便使用相对路径- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-132">Corrected restore command with -SolutionDirectory switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="c3d6d-133">改进了更新的命令来支持解决方案范围的更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-133">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="c3d6d-134">此版本中解决的问题的完整列表可在 NuGet GitHub [命令行里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)中找到。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-134">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="c3d6d-135">Visual Studio 扩展更新</span><span class="sxs-lookup"><span data-stu-id="c3d6d-135">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="c3d6d-136">Visual Studio 中的新功能</span><span class="sxs-lookup"><span data-stu-id="c3d6d-136">New Features in Visual Studio</span></span>

* <span data-ttu-id="c3d6d-137">已将新的上下文菜单项添加到 "解决方案" 节点上的解决方案资源管理器，这允许在不生成解决方案 ([1274](https://github.com/NuGet/Home/issues/1274)) 的情况下还原包。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-137">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新的 "还原包" 上下文菜单项](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="c3d6d-139">Visual Studio 中的更新和修补程序</span><span class="sxs-lookup"><span data-stu-id="c3d6d-139">Updates and Fixes in Visual Studio</span></span>

<span data-ttu-id="c3d6d-140">经过身份验证的源的修补程序也会在扩展中汇总和寻址。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-140">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="c3d6d-141">以下身份验证项目也在扩展中进行了说明：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-141">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="c3d6d-142">现在正确地正确对待 NuGet v3 身份验证源，而不是作为 v2 身份验证源- [1216](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-142">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="c3d6d-143">更正 `project.json` 了使用和与 v2 源通信的项目中身份验证凭据的请求- [1082](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-143">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

<span data-ttu-id="c3d6d-144">网络连接已影响 Visual Studio 中的用户界面，我们通过以下修补程序解决了这一问题：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-144">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="c3d6d-145">提高了包版本（ [1096](https://github.com/NuGet/Home/issues/1096) ）的本地缓存的维护</span><span class="sxs-lookup"><span data-stu-id="c3d6d-145">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="c3d6d-146">在连接到 v3 源时更改了失败行为，不再尝试将其视为 v2 源- [1253](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-146">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="c3d6d-147">现在，在安装包含多个包源的包时阻止安装失败- [1183](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-147">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="c3d6d-148">改进了对生成操作的交互处理：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-148">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="c3d6d-149">如果为单个项目还原包失败，现在继续生成项目- [1169](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-149">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="c3d6d-150">将包安装到由解决方案中其他项目依赖的项目中会强制解决方案重新生成- [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-150">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="c3d6d-151">更正了已失败的包安装以正确回滚对项目的更改- [1265](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-151">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="c3d6d-152">更正了 `developmentDependency` `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)中对包的属性的意外删除</span><span class="sxs-lookup"><span data-stu-id="c3d6d-152">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="c3d6d-153">对的调用 `install.ps1` 现在传递了正确的 `$package.AssemblyReferences` 对象- [1245](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-153">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="c3d6d-154">当项目处于错误状态时，不再阻止卸载 UWP 项目中的包- [1128](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-154">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="c3d6d-155">`packages.config`现在可正确生成包含和项目组合的解决方案， `project.json` 而无需进行第二次生成操作- [1122](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-155">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="c3d6d-156">如果文件已链接或位于其他文件夹中，则正确查找 app.config 文件- [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-156">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="c3d6d-157">UWP 项目现在可以安装未列出的包- [1109](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-157">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="c3d6d-158">当解决方案未处于保存状态时，现在允许使用包还原- [1081](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-158">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>

<span data-ttu-id="c3d6d-159">已更正处理配置文件的更新：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-159">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="c3d6d-160">不再从托管项目的后续版本中删除包中提供的目标文件 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-160">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="c3d6d-161">ASP.NET 5 解决方案版本期间不再修改 Nuget.Config 文件- [1201](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-161">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="c3d6d-162">在包更新期间不再更改允许的版本约束- [1130](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-162">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="c3d6d-163">锁定文件现在在生成期间保持锁定状态- [1127](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-163">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="c3d6d-164">现在 `packages.config` ，在更新过程中修改和不重写此项- [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-164">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>

<span data-ttu-id="c3d6d-165">与 TFS 源代码管理的交互经过改进：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-165">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="c3d6d-166">对于绑定到 TFS- [1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)的包，不会再安装失败。</span><span class="sxs-lookup"><span data-stu-id="c3d6d-166">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="c3d6d-167">更正了 NuGet 用户界面以允许 TFS 2013 集成- [1071](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-167">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="c3d6d-168">更正了对从包文件夹中正确还原的包的引用- [1004](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-168">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="c3d6d-169">最后，我们还改进了以下各项：</span><span class="sxs-lookup"><span data-stu-id="c3d6d-169">Finally, we also improved these items:</span></span>

* <span data-ttu-id="c3d6d-170">针对托管项目减少的日志消息详细级别 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-170">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="c3d6d-171">现在正确地在用户界面中显示包的安装版本- [1061](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-171">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>
* <span data-ttu-id="c3d6d-172">具有在 nuspec 中指定的依赖关系范围的包现在具有为稳定包版本安装的这些依赖项的预发布版本- [1304](https://github.com/NuGet/Home/issues/1304)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-172">Packages with dependency ranges specified in their nuspec now have pre-release versions of those dependencies installed for a stable package version - [1304](https://github.com/NuGet/Home/issues/1304)</span></span>

<span data-ttu-id="c3d6d-173">有关 Visual Studio 扩展的问题的完整列表，请参阅 NuGet GitHub [3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-173">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="c3d6d-174">已知问题</span><span class="sxs-lookup"><span data-stu-id="c3d6d-174">Known Issues</span></span>

<span data-ttu-id="c3d6d-175">我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c3d6d-175">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>