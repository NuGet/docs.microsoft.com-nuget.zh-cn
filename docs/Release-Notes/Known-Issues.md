---
title: "NuGet 已知问题 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 的已知问题，包括身份验证、包安装和工具。"
keywords: "NuGet 已知问题, NuGet 问题"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b9190c058215d9e63894de45c0c55c8ddae0e0f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="29694-104">NuGet 的已知问题</span><span class="sxs-lookup"><span data-stu-id="29694-104">Known Issues with NuGet</span></span>

<span data-ttu-id="29694-105">这些是反复报告的 NuGet 最常见已知问题。</span><span class="sxs-lookup"><span data-stu-id="29694-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="29694-106">如果在安装 NuGet 或管理包时遇到问题，请查看这些已知问题及其解决方案。</span><span class="sxs-lookup"><span data-stu-id="29694-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="29694-107">从 NuGet 4.0 开始，各版本的发行说明中均包含已知问题。</span><span class="sxs-lookup"><span data-stu-id="29694-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="29694-108">在 nuget.exe v3.4.3 中，向 VSTS 中的 NuGet 源进行身份验证的问题</span><span class="sxs-lookup"><span data-stu-id="29694-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="29694-109">**问题：**</span><span class="sxs-lookup"><span data-stu-id="29694-109">**Problem:**</span></span>

<span data-ttu-id="29694-110">当我们使用以下命令来存储凭据时，我们最终会对个人访问令牌双重加密。</span><span class="sxs-lookup"><span data-stu-id="29694-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="29694-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="29694-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="29694-112">**临时解决方法：**</span><span class="sxs-lookup"><span data-stu-id="29694-112">**Workaround:**</span></span>

<span data-ttu-id="29694-113">使用 [-StorePasswordInClearText](../tools/cli-ref-sources.md) 选项以明文形式存储密码。</span><span class="sxs-lookup"><span data-stu-id="29694-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="29694-114">在 NuGet 3.4、3.4.1 中安装包时出现出错</span><span class="sxs-lookup"><span data-stu-id="29694-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="29694-115">**问题：**</span><span class="sxs-lookup"><span data-stu-id="29694-115">**Problem:**</span></span>

<span data-ttu-id="29694-116">在 NuGet 3.4 和 3.4.1 中，使用 NuGet 加载项时，没有源报告为可用，且无法在配置窗口添加新源。</span><span class="sxs-lookup"><span data-stu-id="29694-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="29694-117">结果与下图类似：</span><span class="sxs-lookup"><span data-stu-id="29694-117">The result is similar to the image below:</span></span>

![没有源的 NuGet 配置](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="29694-119">`%AppData%\NuGet\` 文件夹中的 `NuGet.Config` 文件意外被清空。</span><span class="sxs-lookup"><span data-stu-id="29694-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="29694-120">若要解决此问题，请执行以下步骤：关闭 Visual Studio 2015，删除 `%AppData%\NuGet\` 文件夹中的 `NuGet.Config` 文件，然后重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="29694-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="29694-121">将生成新的 `NuGet.Config` 文件，并且你能够继续操作。</span><span class="sxs-lookup"><span data-stu-id="29694-121">A new `NuGet.Config` file will be generated and you are able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="29694-122">在 NuGet 2.7 中安装包时出现错误</span><span class="sxs-lookup"><span data-stu-id="29694-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="29694-123">**问题：**</span><span class="sxs-lookup"><span data-stu-id="29694-123">**Problem:**</span></span>

<span data-ttu-id="29694-124">在 NuGet 2.7 或更高版本中，尝试安装包含程序集引用的任何包时，可能会收到错误消息“输入字符串的格式不正确。”，如下所示：</span><span class="sxs-lookup"><span data-stu-id="29694-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="29694-125">这是由于未在系统上注册 `VSLangProj.dll` COM 组件的类型库引起的。</span><span class="sxs-lookup"><span data-stu-id="29694-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="29694-126">这在以下情况下可能发生，例如：并行安装两个版本的 Visual Studio，然后卸载旧版本。</span><span class="sxs-lookup"><span data-stu-id="29694-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="29694-127">此操作可能会无意中取消注册上述 COM 库。</span><span class="sxs-lookup"><span data-stu-id="29694-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="29694-128">**解决方案：**:</span><span class="sxs-lookup"><span data-stu-id="29694-128">**Solution:**:</span></span>

<span data-ttu-id="29694-129">从提升的提示符运行此命令，重新注册 `VSLangProj.dll` 的类型库</span><span class="sxs-lookup"><span data-stu-id="29694-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="29694-130">如果该命令失败，请检查文件是否存在于该位置。</span><span class="sxs-lookup"><span data-stu-id="29694-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="29694-131">有关此错误的详细信息，请参阅此[工作项](https://nuget.codeplex.com/workitem/3609 "工作项 3609")。</span><span class="sxs-lookup"><span data-stu-id="29694-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="29694-132">在 VS 2012 中更新包之后生成失败</span><span class="sxs-lookup"><span data-stu-id="29694-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="29694-133">问题：使用 VS 2012 RTM。</span><span class="sxs-lookup"><span data-stu-id="29694-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="29694-134">更新 NuGet 包时，出现此消息：“无法完全卸载一个或多个包。”，</span><span class="sxs-lookup"><span data-stu-id="29694-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="29694-135">并提示你重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="29694-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="29694-136">VS 重启后，收到奇怪的生成错误。</span><span class="sxs-lookup"><span data-stu-id="29694-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="29694-137">原因是旧包中的某些文件被后台 MSBuild 进程锁定。</span><span class="sxs-lookup"><span data-stu-id="29694-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="29694-138">即使 VS 重启，后台 MSBuild 进程仍在使用旧包中的文件，导致生成失败。</span><span class="sxs-lookup"><span data-stu-id="29694-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="29694-139">解决方法是安装 VS 2012 Update，例如 VS 2012 Update 2。</span><span class="sxs-lookup"><span data-stu-id="29694-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="29694-140">从旧版升级到最新版 NuGet 时出现签名验证错误</span><span class="sxs-lookup"><span data-stu-id="29694-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="29694-141">由于安装了旧版本，尝试升级 NuGet 时，如果运行 VS 2010 SP1，可能遇到以下错误消息。</span><span class="sxs-lookup"><span data-stu-id="29694-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio 扩展安装程序](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="29694-143">查看日志时，可能会看到提到 `SignatureMismatchException`。</span><span class="sxs-lookup"><span data-stu-id="29694-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="29694-144">若要防止此情况发生，可安装 [Visual Studio 2010 SP1 修补程序](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="29694-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="29694-145">或者，解决方法是简单地卸载 NuGet（以管理员身份运行 Visual Studio 时），然后从 VS 扩展库安装。</span><span class="sxs-lookup"><span data-stu-id="29694-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="29694-146">有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="29694-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="29694-147">当安装了 Reflector Visual Studio 加载项时，包管理器控制台也会引发异常。</span><span class="sxs-lookup"><span data-stu-id="29694-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="29694-148">在运行包管理器控制台时，如果安装了 Reflector VS 加载项，则可能会遇到以下异常消息。</span><span class="sxs-lookup"><span data-stu-id="29694-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="29694-149">或</span><span class="sxs-lookup"><span data-stu-id="29694-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="29694-150">我们已联系了加载项的创建者，希望能够制定一个解决方案。</span><span class="sxs-lookup"><span data-stu-id="29694-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="29694-151">更新：我们已验证了最新版本的 Reflector（6.5 版）不再在控制台中导致此异常。</span><span class="sxs-lookup"><span data-stu-id="29694-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="29694-152">打开包管理器控制台失败，出现 ObjectSecurity 异常</span><span class="sxs-lookup"><span data-stu-id="29694-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="29694-153">尝试打开包管理器控制台时，可能会看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="29694-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="29694-154">如果看到此错误，请按照 [StackOverflow 上讨论的解决方案](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)来修复错误。</span><span class="sxs-lookup"><span data-stu-id="29694-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="29694-155">如果解决方案包含 InstallShield Limited Edition 项目，则“添加包库引用”对话框会引发异常</span><span class="sxs-lookup"><span data-stu-id="29694-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="29694-156">我们发现，如果解决方案包含一个或多个 InstallShield Limited Edition 项目，打开时，“添加包库引用”对话框将引发异常。</span><span class="sxs-lookup"><span data-stu-id="29694-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="29694-157">除了删除或卸载 InstallShield 项目，目前尚无解决方法。</span><span class="sxs-lookup"><span data-stu-id="29694-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="29694-158">“卸载”按钮变灰？</span><span class="sxs-lookup"><span data-stu-id="29694-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="29694-159">需要管理权限才能安装/卸载 NuGet</span><span class="sxs-lookup"><span data-stu-id="29694-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="29694-160">如果尝试通过 Visual Studio Extension Manager 卸载 NuGet，可能会注意到“卸载”按钮被禁用。</span><span class="sxs-lookup"><span data-stu-id="29694-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="29694-161">需要管理员访问权限才能安装和卸载 NuGet。</span><span class="sxs-lookup"><span data-stu-id="29694-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="29694-162">以管理员身份重启 Visual Studio，卸载扩展。</span><span class="sxs-lookup"><span data-stu-id="29694-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="29694-163">NuGet 不需要管理员访问权限即可使用。</span><span class="sxs-lookup"><span data-stu-id="29694-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="29694-164">在 Windows XP 中打开包管理器控制台时崩溃。</span><span class="sxs-lookup"><span data-stu-id="29694-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="29694-165">为什么会这样？</span><span class="sxs-lookup"><span data-stu-id="29694-165">What's wrong?</span></span>

<span data-ttu-id="29694-166">NuGet 需要 Powershell 2.0 运行时。</span><span class="sxs-lookup"><span data-stu-id="29694-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="29694-167">默认情况下，Windows XP 没有 Powershell 2.0。</span><span class="sxs-lookup"><span data-stu-id="29694-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="29694-168">可从 [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) 下载 Powershell 2.0 运行时。</span><span class="sxs-lookup"><span data-stu-id="29694-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="29694-169">安装后，重启 Visual Studio ，应该就能打开包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="29694-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="29694-170">如果包管理器控制台处于打开状态，Visual Studio 2010 SP1 Beta 在退出时崩溃。</span><span class="sxs-lookup"><span data-stu-id="29694-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="29694-171">如果已安装了 Visual Studio 2010 SP1 Beta 版，可能会注意到，当打开包管理器控制台并关闭 Visual Studio 时，它会崩溃。</span><span class="sxs-lookup"><span data-stu-id="29694-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="29694-172">这是 Visual Studio 的一个已知问题，将在 SP1 RTM 版本中修复。</span><span class="sxs-lookup"><span data-stu-id="29694-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="29694-173">临时解决方法是直接忽略崩溃或卸载 SP1 Beta 版（如果可以）。</span><span class="sxs-lookup"><span data-stu-id="29694-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="29694-174">元素“元数据”...发生无效的子元素异常</span><span class="sxs-lookup"><span data-stu-id="29694-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="29694-175">如果安装了使用 NuGet 预发布版本生成的包，当对该项目运行 RTM 版本的 NuGet 时，可能会遇到错误消息“命名空间‘schemas.microsoft.com/packaging/2010/07/nuspec.xsd’中的元素‘元数据’具有无效的子元素”。</span><span class="sxs-lookup"><span data-stu-id="29694-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="29694-176">将需要使用 RTM 版本的 NuGet 卸载并重新安装每个包。</span><span class="sxs-lookup"><span data-stu-id="29694-176">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="29694-177">尝试安装或卸载导致错误“文件已存在时，无法创建该文件。”</span><span class="sxs-lookup"><span data-stu-id="29694-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="29694-178">出于某种原因，Visual Studio 扩展呈现奇怪的状态，即已卸载了 VSIX 扩展，但遗留了一些文件。</span><span class="sxs-lookup"><span data-stu-id="29694-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="29694-179">解决此问题：</span><span class="sxs-lookup"><span data-stu-id="29694-179">To work around this issue:</span></span>

1. <span data-ttu-id="29694-180">退出 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29694-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="29694-181">打开以下文件夹（可能位于计算机上的其他驱动器上）</span><span class="sxs-lookup"><span data-stu-id="29694-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="29694-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="29694-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="29694-183">删除带有 .deleteme 扩展名的所有文件。</span><span class="sxs-lookup"><span data-stu-id="29694-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="29694-184">重新打开 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29694-184">Re-open Visual Studio</span></span>

<span data-ttu-id="29694-185">执行这些步骤后，继续操作。</span><span class="sxs-lookup"><span data-stu-id="29694-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="29694-186">在极少数情况下，当代码分析处于开启状态时，编译会导致错误。</span><span class="sxs-lookup"><span data-stu-id="29694-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="29694-187">如果使用包管理器控制台安装 FluentNHibernate，然后在代码分析处于开启状态时编译项目，可能会收到以下错误。</span><span class="sxs-lookup"><span data-stu-id="29694-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="29694-188">默认情况下，FluentNHibernate 需要 NHibernate 3.0.0.2001。</span><span class="sxs-lookup"><span data-stu-id="29694-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="29694-189">但是，NuGet 会故意在项目中安装 NHibernate 3.0.0.4000 ，并添加相应的绑定重定向，使其工作。</span><span class="sxs-lookup"><span data-stu-id="29694-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="29694-190">如果没有开启代码分析，项目将正常编译。</span><span class="sxs-lookup"><span data-stu-id="29694-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="29694-191">与编译器不同，代码分析工具不正确地遵循绑定重定向来使用 3.0.0.4000 而非 3.0.0.2001。</span><span class="sxs-lookup"><span data-stu-id="29694-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="29694-192">可通过安装 NHibernate 3.0.0.2001 或者通过执行以下操作，指示代码分析工具与编译器行为相同，来解决这个问题：</span><span class="sxs-lookup"><span data-stu-id="29694-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="29694-193">转到 %PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop</span><span class="sxs-lookup"><span data-stu-id="29694-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="29694-194">打开 FxCopCmd.exe.config 并将 `AssemblyReferenceResolveMode` 从 `StrongName` 更改为 `StrongNameIgnoringVersion`。</span><span class="sxs-lookup"><span data-stu-id="29694-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="29694-195">保存更改并重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="29694-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="29694-196">Write-Error 命令在 install.ps1/uninstall.ps1/init.ps1 中不起作用</span><span class="sxs-lookup"><span data-stu-id="29694-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="29694-197">这是一个已知问题。</span><span class="sxs-lookup"><span data-stu-id="29694-197">This is a known issue.</span></span> <span data-ttu-id="29694-198">请调用 throw，而非调用 Write-Error。</span><span class="sxs-lookup"><span data-stu-id="29694-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="29694-199">在 Windows 2003 上安装具有受限访问权限的 NuGet 可能会导致 Visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="29694-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="29694-200">尝试使用 Visual Studio Extension Manager 安装 NuGet 并且未以管理员身份运行时，将显示“运行方式”对话框，并且默认选中对话框中标记为“以受限访问运行此程序”的复选框。</span><span class="sxs-lookup"><span data-stu-id="29694-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![“以受限方式运行”对话框](./media/RunAsRestricted.png)

<span data-ttu-id="29694-202">选中该复选框后，单击“确定”会导致 Visual Studio 崩溃。</span><span class="sxs-lookup"><span data-stu-id="29694-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="29694-203">确保先取消选中该选项，然后再安装 NuGet。</span><span class="sxs-lookup"><span data-stu-id="29694-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="29694-204">无法卸载适用于 Windows Phone 工具的 NuGet</span><span class="sxs-lookup"><span data-stu-id="29694-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="29694-205">Windows Phone 工具不支持 Visual Studio Extension Manager。</span><span class="sxs-lookup"><span data-stu-id="29694-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="29694-206">若要卸载 NuGet，请运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="29694-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="29694-207">更改 NuGet 包 ID 的大写会中断包还原</span><span class="sxs-lookup"><span data-stu-id="29694-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="29694-208">正如在[此 GitHub 问题](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)上详细讨论的，可通过 NuGet 支持来完成 NuGet 包的大写更改，但对于在本地包缓存中现有不同包的用户来说，包还原期间会导致复杂情况。</span><span class="sxs-lookup"><span data-stu-id="29694-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="29694-209">建议仅在有办法与包的现有用户交流生成时包还原可能发生的中断情况时，才请求更改事例。</span><span class="sxs-lookup"><span data-stu-id="29694-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="29694-210">报告问题</span><span class="sxs-lookup"><span data-stu-id="29694-210">Reporting issues</span></span>

<span data-ttu-id="29694-211">若要报告 NuGet 问题，请访问 [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)。</span><span class="sxs-lookup"><span data-stu-id="29694-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
