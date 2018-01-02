---
title: "配置 NuGet 行为 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "NuGet.Config 文件同时以全局方式和基于每个项目的方式控制 NuGet 的行为，并且这些文件可使用 nuget config 命令进行修改。"
keywords: "NuGet 配置文件, NuGet 配置, NuGet 行为设置, NuGet 设置, Nuget.Config, NuGetDefaults.Config, 默认"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="69dfb-104">配置 NuGet 行为</span><span class="sxs-lookup"><span data-stu-id="69dfb-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="69dfb-105">NuGet 的行为由一个或多个 `NuGet.Config` (XML) 文件（可存在于项目范围、用户范围和计算机范围的级别）中的累积设置驱动。</span><span class="sxs-lookup"><span data-stu-id="69dfb-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="69dfb-106">还可以使用全局 `NuGetDefaults.Config` 文件 (2.7+) 专门用于配置包源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="69dfb-107">这些设置应用于 CLI、包管理器控制台和包管理器 UI 中发出的所有命令。</span><span class="sxs-lookup"><span data-stu-id="69dfb-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="69dfb-108">在本主题中：</span><span class="sxs-lookup"><span data-stu-id="69dfb-108">In this topic:</span></span>

- [<span data-ttu-id="69dfb-109">NuGet.Config 文件的位置和使用</span><span class="sxs-lookup"><span data-stu-id="69dfb-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="69dfb-110">更改设置</span><span class="sxs-lookup"><span data-stu-id="69dfb-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="69dfb-111">如何应用设置</span><span class="sxs-lookup"><span data-stu-id="69dfb-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="69dfb-112">NuGetDefaults.Config 文件</span><span class="sxs-lookup"><span data-stu-id="69dfb-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="69dfb-113">配置文件的位置和使用</span><span class="sxs-lookup"><span data-stu-id="69dfb-113">Config file locations and uses</span></span>

| <span data-ttu-id="69dfb-114">范围</span><span class="sxs-lookup"><span data-stu-id="69dfb-114">Scope</span></span> | <span data-ttu-id="69dfb-115">NuGet.Config 文件的位置</span><span class="sxs-lookup"><span data-stu-id="69dfb-115">NuGet.Config file location</span></span> | <span data-ttu-id="69dfb-116">描述</span><span class="sxs-lookup"><span data-stu-id="69dfb-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69dfb-117">Project</span><span class="sxs-lookup"><span data-stu-id="69dfb-117">Project</span></span> | <span data-ttu-id="69dfb-118">项目文件夹或上至驱动器根目录的任何文件夹</span><span class="sxs-lookup"><span data-stu-id="69dfb-118">Project folder or any folder up to the drive root</span></span> | <span data-ttu-id="69dfb-119">在项目文件夹中，设置仅应用于该项目。</span><span class="sxs-lookup"><span data-stu-id="69dfb-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="69dfb-120">在包含多个项目子文件夹的父文件夹中，设置应用于这些子文件夹中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="69dfb-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="69dfb-121">用户</span><span class="sxs-lookup"><span data-stu-id="69dfb-121">User</span></span> | <span data-ttu-id="69dfb-122">Windows：%APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="69dfb-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="69dfb-123">Mac/Linux：~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="69dfb-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="69dfb-124">设置应用于所有操作，但可被任何项目级的设置替代。</span><span class="sxs-lookup"><span data-stu-id="69dfb-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> <span data-ttu-id="69dfb-125">使用 CLI 命令时，可以使用 `-configFile` 开关来指定其他配置文件，以忽略默认用户级文件中的任何设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-125">When using CLI commands, you can specify a different config file using the `-configFile` switch to ignore any settings in the default user-level file.</span></span> |
| <span data-ttu-id="69dfb-126">计算机</span><span class="sxs-lookup"><span data-stu-id="69dfb-126">Computer</span></span> | <span data-ttu-id="69dfb-127">Windows：%ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="69dfb-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="69dfb-128">Mac/Linux：$XDG_DATA_HOME（通常为 ~/.local/share）</span><span class="sxs-lookup"><span data-stu-id="69dfb-128">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="69dfb-129">设置应用于计算机上的所有操作，但可被任何用户级或项目级的设置替代。</span><span class="sxs-lookup"><span data-stu-id="69dfb-129">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="69dfb-130">针对早期版本的 NuGet 的说明：</span><span class="sxs-lookup"><span data-stu-id="69dfb-130">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="69dfb-131">NuGet 3.3 及更早版本使用 `.nuget` 文件夹作为解决方案范围的设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-131">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="69dfb-132">NuGet 3.4+ 中不使用此文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-132">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="69dfb-133">对于 NuGet 2.6 到 3.x 版本，Windows 上的计算机级配置文件位于 %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config，其中，{IDE} 可能为 VisualStudio，{Version} 为 Visual Studio 的版本（如 14.0），{SKU} 可能为 Community、Pro 或 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="69dfb-133">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="69dfb-134">若要将设置迁移到 NuGet 4.0+，只需将配置文件复制到 %ProgramFiles(x86)%\NuGet\Config 即可。在 Linux 上，此位置以前为 /etc/opt；在 Mac 上为 /Library/Application Support。</span><span class="sxs-lookup"><span data-stu-id="69dfb-134">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linus, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="69dfb-135">更改配置设置</span><span class="sxs-lookup"><span data-stu-id="69dfb-135">Changing config settings</span></span>

<span data-ttu-id="69dfb-136">`NuGet.Config` 文件是包含键/值对的简单 XML 文本文件，请参阅 [NuGet 配置设置](../Schema/nuget-config-file.md)主题。</span><span class="sxs-lookup"><span data-stu-id="69dfb-136">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="69dfb-137">设置通过 NuGet CLI [config 命令](../tools/cli-ref-config.md)进行管理：</span><span class="sxs-lookup"><span data-stu-id="69dfb-137">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="69dfb-138">默认情况下需更改用户级配置文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-138">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="69dfb-139">若要更改其他文件中的设置，请使用 `-configFile` 开关。</span><span class="sxs-lookup"><span data-stu-id="69dfb-139">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="69dfb-140">在此情况下，文件可以使用任何文件名。</span><span class="sxs-lookup"><span data-stu-id="69dfb-140">In this case files can use any filename.</span></span>
- <span data-ttu-id="69dfb-141">键始终需要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="69dfb-141">Keys are always case sensitive.</span></span>
- <span data-ttu-id="69dfb-142">更改计算机级设置文件中的设置需要提升权限。</span><span class="sxs-lookup"><span data-stu-id="69dfb-142">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="69dfb-143">尽管可以修改任何文本编辑器中的文件，但如果配置文件中包含格式不正确的 XML（不匹配的标记、无效引号等），NuGet（v3.4.3 及更高版本）将以无提示方式忽略整个配置文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-143">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="69dfb-144">因此推荐使用 `nuget config` 管理设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-144">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="69dfb-145">设置值</span><span class="sxs-lookup"><span data-stu-id="69dfb-145">Setting a value</span></span>

<span data-ttu-id="69dfb-146">Windows：</span><span class="sxs-lookup"><span data-stu-id="69dfb-146">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="69dfb-147">Mac/Linux：</span><span class="sxs-lookup"><span data-stu-id="69dfb-147">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="69dfb-148">在 NuGet 3.4 及更高版本中，可以在任何值中使用环境变量，与在 `repositoryPath=%PACKAGEHOME%` (Windows) 和 `repositoryPath=%PACKAGEHOME` (Mac/Linux) 中类似。</span><span class="sxs-lookup"><span data-stu-id="69dfb-148">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="69dfb-149">删除值</span><span class="sxs-lookup"><span data-stu-id="69dfb-149">Removing a value</span></span>

<span data-ttu-id="69dfb-150">若要删除值，请指定具有空值的键。</span><span class="sxs-lookup"><span data-stu-id="69dfb-150">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="69dfb-151">创建新配置文件</span><span class="sxs-lookup"><span data-stu-id="69dfb-151">Creating a new config file</span></span>

<span data-ttu-id="69dfb-152">将下方的模板复制到新文件中，然后使用 `nuget config --configFile <filename>` 设置值：</span><span class="sxs-lookup"><span data-stu-id="69dfb-152">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="69dfb-153">如何应用设置</span><span class="sxs-lookup"><span data-stu-id="69dfb-153">How settings are applied</span></span>

<span data-ttu-id="69dfb-154">可使用多个 `NuGet.Config` 文件在不同位置存储设置，以便设置可应用于单个项目、一组项目或所有项目。</span><span class="sxs-lookup"><span data-stu-id="69dfb-154">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="69dfb-155">这些设置共同应用于从命令行或 Visual Studio 调用的任何 NuGet 操作，并且优先应用“最靠近”项目或当前文件夹的设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-155">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="69dfb-156">具体而言，NuGet 将按照以下顺序从不同配置文件加载设置：</span><span class="sxs-lookup"><span data-stu-id="69dfb-156">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="69dfb-157">[NuGetDefaults.Config 文件](#nuget-defaults-file)，仅包含与包源相关的设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-157">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="69dfb-158">计算机级文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-158">The computer-level file.</span></span>
1. <span data-ttu-id="69dfb-159">用户级文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-159">The user-level file.</span></span>
1. <span data-ttu-id="69dfb-160">用 `-configFile` 指定的文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-160">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="69dfb-161">按照从驱动器根目录到当前文件夹（在此文件夹中调用 nuget.exe 或此文件夹包含 Visual Studio 项目）的路径，在其中的每个文件夹中找到的文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-161">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="69dfb-162">例如，如果在 c:\A\B\C 中调用命令，NuGet 将先后查找并加载 c:\,、c:\A、c:\A\B 和 c:\A\B\C 中的配置文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-162">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="69dfb-163">NuGet 在这些文件中找到设置时，设置将按如下方式应用：</span><span class="sxs-lookup"><span data-stu-id="69dfb-163">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="69dfb-164">对于单项元素，NuGet 将替换以前找到的具有相同键的值。</span><span class="sxs-lookup"><span data-stu-id="69dfb-164">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="69dfb-165">也就是说，“最靠近”当前文件夹或项目的设置将替代之前找到的任何其他设置。</span><span class="sxs-lookup"><span data-stu-id="69dfb-165">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="69dfb-166">例如，如果 `NuGetDefaults.Config` 中的 `defaultPushSource` 设置存在于任何其他配置文件中，则此设置将被替代。</span><span class="sxs-lookup"><span data-stu-id="69dfb-166">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="69dfb-167">对于集合元素（如 `<packageSources>`），NuGet 会将所有配置文件中的值合并到一个集合中。</span><span class="sxs-lookup"><span data-stu-id="69dfb-167">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="69dfb-168">当给定节点中存在 `<clear />` 时，NuGet 将忽略之前为该节点定义的配置值。</span><span class="sxs-lookup"><span data-stu-id="69dfb-168">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="69dfb-169">设置演练</span><span class="sxs-lookup"><span data-stu-id="69dfb-169">Settings walkthrough</span></span>

<span data-ttu-id="69dfb-170">假设两个独立的驱动器上具有以下文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="69dfb-170">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="69dfb-171">随后以下位置上将有 4 个具有给定内容的 `NuGet.Config` 文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-171">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="69dfb-172">（此示例不包括计算机级文件，但其与用户级文件具有相似行为。）</span><span class="sxs-lookup"><span data-stu-id="69dfb-172">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="69dfb-173">文件 A. 用户级文件（在 Windows 上为 %APPDATA%\NuGet\NuGet.Config；在 Mac/Linux 上为 ~/.nuget/NuGet.Config）：</span><span class="sxs-lookup"><span data-stu-id="69dfb-173">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="69dfb-174">文件 B. disk_drive_2/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="69dfb-174">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>        
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="69dfb-175">文件 C. disk_drive_2/Project1/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="69dfb-175">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="69dfb-176">文件 D. disk_drive_2/Project2/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="69dfb-176">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="69dfb-177">接下来，NuGet 将按如下方式加载和应用设置，具体取决于调用设置的位置：</span><span class="sxs-lookup"><span data-stu-id="69dfb-177">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="69dfb-178">**从 disk_drive_1/users 调用**：仅使用用户级配置文件 (A) 中列出的默认存储库，因为这是在 disk_drive_1 中找到的唯一文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-178">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="69dfb-179">**从 disk_drive_2/ 或 disk_drive_/tmp 调用**：首先加载用户级文件 (A)，然后 NuGet 转到 disk_drive_2 的根目录并查找文件 (B)。</span><span class="sxs-lookup"><span data-stu-id="69dfb-179">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="69dfb-180">NuGet 还将在 /tmp 中查找配置文件，但不会找到此类文件。</span><span class="sxs-lookup"><span data-stu-id="69dfb-180">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="69dfb-181">因此，此时将使用 nuget.org 上的默认存储库、启用包还原并在 disk_drive_2/tmp 中展开包。</span><span class="sxs-lookup"><span data-stu-id="69dfb-181">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="69dfb-182">**从 disk_drive_2/Project1 或 disk_drive_2/Project1/Source 调用**：首先加载用户级文件 (A)，然后 NuGet 依次加载 disk_drive_2 根目录中的文件 (B) 和文件 (C)。</span><span class="sxs-lookup"><span data-stu-id="69dfb-182">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="69dfb-183">(C) 中的设置会替代 (B) 和 (A) 中的设置，因此安装包的 `repositoryPath` 将为 disk_drive_2/Project1/External/Packages，而非 disk_drive_2/tmp。</span><span class="sxs-lookup"><span data-stu-id="69dfb-183">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="69dfb-184">此外，由于 (C) 清除了 `<packageSources>`，因此 nuget.org 将不再可用作源，并仅留下 `https://MyPrivateRepo/ES/nuget`。</span><span class="sxs-lookup"><span data-stu-id="69dfb-184">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="69dfb-185">**从 disk_drive_2/Project2 或 disk_drive_2/Project2/Source 调用**：首先加载用户级文件 (A)，然后依次加载文件 (B) 和文件 (D)。</span><span class="sxs-lookup"><span data-stu-id="69dfb-185">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="69dfb-186">由于未清除 `packageSources`，因此 `nuget.org` 和 `https://MyPrivateRepo/DQ/nuget` 都可用作源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-186">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="69dfb-187">按 (B) 中的指定，包将在 disk_drive_2/tmp 中展开。</span><span class="sxs-lookup"><span data-stu-id="69dfb-187">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="69dfb-188">NuGet 默认文件</span><span class="sxs-lookup"><span data-stu-id="69dfb-188">NuGet defaults file</span></span>

<span data-ttu-id="69dfb-189">`NuGetDefaults.Config` 文件用于指定通过其安装和更新包的包源，以及控制使用 `nuget push` 发布包的默认目标。</span><span class="sxs-lookup"><span data-stu-id="69dfb-189">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="69dfb-190">管理员可以轻松向开发人员和生成计算机部署一致的 `NuGetDefaults.Config` 文件（例如使用组策略），因此他们可以确保组织中的每位用户使用正确的包源，而不是 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="69dfb-190">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="69dfb-191">`NuGetDefaults.Config` 文件绝不会导致开发人员 NuGet 配置中的包源被删除。</span><span class="sxs-lookup"><span data-stu-id="69dfb-191">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="69dfb-192">也就是说，如果开发人员已使用 NuGet，即意味着已注册 nuget.org 包源，创建 `NuGetDefaults.Config` 文件后将不会删除此包源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-192">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="69dfb-193">此外，NuGet 中的 `NuGetDefaults.Config` 或任何其他机制都不会阻止访问 nuget.org 等包源。如果组织希望阻止此类访问，则必须通过其他方式（如防火墙）实现。</span><span class="sxs-lookup"><span data-stu-id="69dfb-193">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="69dfb-194">NuGetDefaults.Config 的位置</span><span class="sxs-lookup"><span data-stu-id="69dfb-194">NuGetDefaults.Config location</span></span>

<span data-ttu-id="69dfb-195">Windows：%ProgramFiles(x86)%\NuGet\Config（NuGet 2.7 到 NuGet 3.x：%PROGRAMDATA%\NuGet\NuGetDefaults.Config） Mac/Linux：$XDG_DATA_HOME（通常为 ~/.local/share）</span><span class="sxs-lookup"><span data-stu-id="69dfb-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="69dfb-196">NuGetDefaults.Config 的设置</span><span class="sxs-lookup"><span data-stu-id="69dfb-196">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="69dfb-197">`packageSources`：此集合与常规配置文件中的 `packageSources` 具有相同含义，可按其首选顺序指定默认源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-197">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="69dfb-198">如果 `NuGetDefaults.Config` 中存在此设置，NuGet 将不会使用 nuget.org 作为默认包源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-198">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="69dfb-199">这样，管理员便可以确保使用此文件的每位用户都使用相同源，避免按照个人意愿使用 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="69dfb-199">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="69dfb-200">`disabledPackageSources`：此集合还与在 `NuGet.Config` 文件中时具有相同含义，集合中将列出每个受影响源的名称，并用 true/false 值指示源是否已禁用。</span><span class="sxs-lookup"><span data-stu-id="69dfb-200">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="69dfb-201">这可使源名称和 URL 保留在 `packageSources` 中，但不会将其默认打开。</span><span class="sxs-lookup"><span data-stu-id="69dfb-201">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="69dfb-202">开发人员随后可在其他 `NuGet.Config` 文件中将源的值设置为 false，以便重新启用源，而无需再次寻找正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="69dfb-202">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="69dfb-203">开发人员还可通过此方法获取组织的内部源 URL 完整列表，同时仅默认启用一个团队的源。</span><span class="sxs-lookup"><span data-stu-id="69dfb-203">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="69dfb-204">`defaultPushSource`：指定 `nuget push` 操作的默认目标，同时替代 nuget.org 的内置默认值。管理员可部署此设置以避免误将内部包发布到公共 nuget.org，因为开发人员专门负责使用 `nuget push -Source` 向 nuget.org 发布。</span><span class="sxs-lookup"><span data-stu-id="69dfb-204">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="69dfb-205">示例 NuGetDefaults.Config 和应用程序</span><span class="sxs-lookup"><span data-stu-id="69dfb-205">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
