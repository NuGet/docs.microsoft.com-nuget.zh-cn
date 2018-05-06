---
title: 已知问题
description: NuGet 的已知问题，包括身份验证、包安装和工具。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f170f377a3394694e953a794f2c814388656c21
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="known-issues-with-nuget"></a>NuGet 的已知问题

这些是反复报告的 NuGet 最常见已知问题。 如果在安装 NuGet 或管理包时遇到问题，请查看这些已知问题及其解决方案。

> [!Note]
> 从 NuGet 4.0 开始，各版本的发行说明中均包含已知问题。

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>在 nuget.exe v3.4.3 中，向 VSTS 中的 NuGet 源进行身份验证的问题

**问题：**

当我们使用以下命令来存储凭据时，我们最终会对个人访问令牌双重加密。

$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**临时解决方法：**

使用 [-StorePasswordInClearText](../tools/cli-ref-sources.md) 选项以明文形式存储密码。

## <a name="error-installing-packages-with-nuget-34-341"></a>在 NuGet 3.4、3.4.1 中安装包时出现出错

**问题：**

在 NuGet 3.4 和 3.4.1 中，使用 NuGet 加载项时，没有源报告为可用，且无法在配置窗口添加新源。 结果与下图类似：

![没有源的 NuGet 配置](./media/knownIssue-34-NoSources.PNG)

`%AppData%\NuGet\` (Windows) 或 `~/.nuget/` (Mac/Linux) 文件夹中的 `NuGet.Config` 文件意外被清空。 若要解决此问题，请执行以下操作：关闭 Visual Studio（适用于 Windows），删除 `NuGet.Config` 文件，然后再次尝试操作。 NuGet 生成了新的 `NuGet.Config` 文件，你应该可以继续操作。

## <a name="error-installing-packages-with-nuget-27"></a>在 NuGet 2.7 中安装包时出现错误

**问题：**

在 NuGet 2.7 或更高版本中，尝试安装包含程序集引用的任何包时，可能会收到错误消息“输入字符串的格式不正确。”，如下所示：

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

这是由于未在系统上注册 `VSLangProj.dll` COM 组件的类型库引起的。 这在以下情况下可能发生，例如：并行安装两个版本的 Visual Studio，然后卸载旧版本。 此操作可能会无意中取消注册上述 COM 库。

**解决方案：**:

从提升的提示符运行此命令，重新注册 `VSLangProj.dll` 的类型库

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

如果该命令失败，请检查文件是否存在于该位置。

有关此错误的详细信息，请参阅此[工作项](https://nuget.codeplex.com/workitem/3609 "工作项 3609")。

## <a name="build-failure-after-package-update-in-vs-2012"></a>在 VS 2012 中更新包之后生成失败

问题：使用 VS 2012 RTM。 更新 NuGet 包时，出现此消息：“无法完全卸载一个或多个包。”， 并提示你重启 Visual Studio。 VS 重启后，收到奇怪的生成错误。

原因是旧包中的某些文件被后台 MSBuild 进程锁定。 即使 VS 重启，后台 MSBuild 进程仍在使用旧包中的文件，导致生成失败。

解决方法是安装 VS 2012 Update，例如 VS 2012 Update 2。

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>从旧版升级到最新版 NuGet 时出现签名验证错误

由于安装了旧版本，尝试升级 NuGet 时，如果运行 VS 2010 SP1，可能遇到以下错误消息。

![Visual Studio 扩展安装程序](./media/Visual-Studio-Extension-Installer.png)

查看日志时，可能会看到提到 `SignatureMismatchException`。

若要防止此情况发生，可安装 [Visual Studio 2010 SP1 修补程序](http://bit.ly/vsixcertfix)。
或者，解决方法是简单地卸载 NuGet（以管理员身份运行 Visual Studio 时），然后从 VS 扩展库安装。  有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>当安装了 Reflector Visual Studio 加载项时，包管理器控制台也会引发异常。

在运行包管理器控制台时，如果安装了 Reflector VS 加载项，则可能会遇到以下异常消息。

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

或

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

我们已联系了加载项的创建者，希望能够制定一个解决方案。

<p class="info">更新：我们已验证了最新版本的 Reflector（6.5 版）不再在控制台中导致此异常。</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>打开包管理器控制台失败，出现 ObjectSecurity 异常

尝试打开包管理器控制台时，可能会看到以下错误：

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

如果看到此错误，请按照 [StackOverflow 上讨论的解决方案](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)来修复错误。

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>如果解决方案包含 InstallShield Limited Edition 项目，则“添加包库引用”对话框会引发异常

我们发现，如果解决方案包含一个或多个 InstallShield Limited Edition 项目，打开时，“添加包库引用”对话框将引发异常。 除了删除或卸载 InstallShield 项目，目前尚无解决方法。

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>“卸载”按钮变灰？ 需要管理权限才能安装/卸载 NuGet

如果尝试通过 Visual Studio Extension Manager 卸载 NuGet，可能会注意到“卸载”按钮被禁用。 需要管理员访问权限才能安装和卸载 NuGet。 以管理员身份重启 Visual Studio，卸载扩展。 NuGet 不需要管理员访问权限即可使用。

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>在 Windows XP 中打开包管理器控制台时崩溃。 为什么会这样？

NuGet 需要 Powershell 2.0 运行时。 默认情况下，Windows XP 没有 Powershell 2.0。 可从 [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) 下载 Powershell 2.0 运行时。 安装后，重启 Visual Studio ，应该就能打开包管理器控制台。

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>如果包管理器控制台处于打开状态，Visual Studio 2010 SP1 Beta 在退出时崩溃。

如果已安装了 Visual Studio 2010 SP1 Beta 版，可能会注意到，当打开包管理器控制台并关闭 Visual Studio 时，它会崩溃。 这是 Visual Studio 的一个已知问题，将在 SP1 RTM 版本中修复。 临时解决方法是直接忽略崩溃或卸载 SP1 Beta 版（如果可以）。

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>元素“元数据”...发生无效的子元素异常

如果安装了使用 NuGet 预发布版本生成的包，当对该项目运行 RTM 版本的 NuGet 时，可能会遇到错误消息“命名空间‘schemas.microsoft.com/packaging/2010/07/nuspec.xsd’中的元素‘元数据’具有无效的子元素”。 将需要使用 RTM 版本的 NuGet 卸载并重新安装每个包。

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>尝试安装或卸载导致错误“文件已存在时，无法创建该文件。”

出于某种原因，Visual Studio 扩展呈现奇怪的状态，即已卸载了 VSIX 扩展，但遗留了一些文件。 解决此问题：

1. 退出 Visual Studio
1. 打开以下文件夹（可能位于计算机上的其他驱动器上）

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. 删除带有 .deleteme 扩展名的所有文件。
1. 重新打开 Visual Studio

执行这些步骤后，继续操作。

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>在极少数情况下，当代码分析处于开启状态时，编译会导致错误。

如果使用包管理器控制台安装 FluentNHibernate，然后在代码分析处于开启状态时编译项目，可能会收到以下错误。

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

默认情况下，FluentNHibernate 需要 NHibernate 3.0.0.2001。 但是，NuGet 会故意在项目中安装 NHibernate 3.0.0.4000 ，并添加相应的绑定重定向，使其工作。 如果没有开启代码分析，项目将正常编译。 与编译器不同，代码分析工具不正确地遵循绑定重定向来使用 3.0.0.4000 而非 3.0.0.2001。 可通过安装 NHibernate 3.0.0.2001 或者通过执行以下操作，指示代码分析工具与编译器行为相同，来解决这个问题：

1. 转到 %PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop
1. 打开 FxCopCmd.exe.config 并将 `AssemblyReferenceResolveMode` 从 `StrongName` 更改为 `StrongNameIgnoringVersion`。
1. 保存更改并重新生成项目。

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Write-Error 命令在 install.ps1/uninstall.ps1/init.ps1 中不起作用

这是一个已知问题。 请调用 throw，而非调用 Write-Error。

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>在 Windows 2003 上安装具有受限访问权限的 NuGet 可能会导致 Visual Studio 崩溃

尝试使用 Visual Studio Extension Manager 安装 NuGet 并且未以管理员身份运行时，将显示“运行方式”对话框，并且默认选中对话框中标记为“以受限访问运行此程序”的复选框。

![“以受限方式运行”对话框](./media/RunAsRestricted.png)

选中该复选框后，单击“确定”会导致 Visual Studio 崩溃。 确保先取消选中该选项，然后再安装 NuGet。

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>无法卸载适用于 Windows Phone 工具的 NuGet

Windows Phone 工具不支持 Visual Studio Extension Manager。 若要卸载 NuGet，请运行以下命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>更改 NuGet 包 ID 的大写会中断包还原

正如在[此 GitHub 问题](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)上详细讨论的，可通过 NuGet 支持来完成 NuGet 包的大写更改，但对于在 global-packages 文件夹中现有不同包的用户来说，包还原期间会导致复杂情况。 建议仅在有办法与包的现有用户交流生成时包还原可能发生的中断情况时，才请求更改事例。

## <a name="reporting-issues"></a>报告问题

若要报告 NuGet 问题，请访问 [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)。
