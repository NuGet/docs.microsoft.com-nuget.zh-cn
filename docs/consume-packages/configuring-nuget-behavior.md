---
title: 常见的 NuGet 配置
description: NuGet.Config 文件同时以全局方式和基于每个项目的方式控制 NuGet 的行为，并且这些文件可使用 nuget config 命令进行修改。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 5309d94fafea9cdfc3699d443393be5d381dd145
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317734"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="7165f-103">常见的 NuGet 配置</span><span class="sxs-lookup"><span data-stu-id="7165f-103">Common NuGet configurations</span></span>

<span data-ttu-id="7165f-104">NuGet 的行为由一个或多个 `NuGet.Config` (XML) 文件（可存在于项目范围、用户范围和计算机范围的级别）中的累积设置驱动。</span><span class="sxs-lookup"><span data-stu-id="7165f-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="7165f-105">还可以使用全局 `NuGetDefaults.Config` 文件专门配置包源。</span><span class="sxs-lookup"><span data-stu-id="7165f-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="7165f-106">这些设置应用于 CLI、包管理器控制台和包管理器 UI 中发出的所有命令。</span><span class="sxs-lookup"><span data-stu-id="7165f-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="7165f-107">配置文件的位置和使用</span><span class="sxs-lookup"><span data-stu-id="7165f-107">Config file locations and uses</span></span>

| <span data-ttu-id="7165f-108">范围</span><span class="sxs-lookup"><span data-stu-id="7165f-108">Scope</span></span> | <span data-ttu-id="7165f-109">NuGet.Config 文件的位置</span><span class="sxs-lookup"><span data-stu-id="7165f-109">NuGet.Config file location</span></span> | <span data-ttu-id="7165f-110">说明</span><span class="sxs-lookup"><span data-stu-id="7165f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7165f-111">解决方案</span><span class="sxs-lookup"><span data-stu-id="7165f-111">Solution</span></span> | <span data-ttu-id="7165f-112">当前文件夹（又称解决方案文件夹）或上至驱动器根目录的任何文件夹。</span><span class="sxs-lookup"><span data-stu-id="7165f-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="7165f-113">在解决方案文件夹中，设置应用于子文件夹中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="7165f-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="7165f-114">请注意，如果配置文件位于项目文件夹中，则对该项目没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="7165f-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="7165f-115">用户</span><span class="sxs-lookup"><span data-stu-id="7165f-115">User</span></span> | <span data-ttu-id="7165f-116">Windows：`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="7165f-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="7165f-117">Mac/Linux：`~/.config/NuGet/NuGet.Config` 或 `~/.nuget/NuGet/NuGet.Config`（因 OS 版本而异）</span><span class="sxs-lookup"><span data-stu-id="7165f-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="7165f-118">设置应用于所有操作，但可被任何项目级的设置替代。</span><span class="sxs-lookup"><span data-stu-id="7165f-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="7165f-119">计算机</span><span class="sxs-lookup"><span data-stu-id="7165f-119">Computer</span></span> | <span data-ttu-id="7165f-120">Windows：`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="7165f-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="7165f-121">Mac/Linux：`$XDG_DATA_HOME`。</span><span class="sxs-lookup"><span data-stu-id="7165f-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="7165f-122">如果 `$XDG_DATA_HOME` 的值是 null 或为空，将使用 `~/.local/share` 或 `/usr/local/share`（因 OS 版本而异）</span><span class="sxs-lookup"><span data-stu-id="7165f-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="7165f-123">设置虽然适用于计算机上的所有操作，但会被任何用户级或项目级设置覆盖。</span><span class="sxs-lookup"><span data-stu-id="7165f-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="7165f-124">针对早期版本的 NuGet 的说明：</span><span class="sxs-lookup"><span data-stu-id="7165f-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="7165f-125">NuGet 3.3 及更早版本使用 `.nuget` 文件夹作为解决方案范围的设置。</span><span class="sxs-lookup"><span data-stu-id="7165f-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="7165f-126">NuGet 3.4+ 中不使用此文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="7165f-127">对于 NuGet 2.6 到 3.x 版本，Windows 上的计算机级配置文件位于 %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config，其中，{IDE} 可能为 VisualStudio，{Version} 为 Visual Studio 的版本（如 14.0），{SKU} 可能为 Community、Pro 或 Enterprise         。</span><span class="sxs-lookup"><span data-stu-id="7165f-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="7165f-128">若要将设置迁移到 NuGet 4.0+，只需将配置文件复制到 %ProgramFiles(x86)%\NuGet\Config 即可。在 Linux 上，此位置以前为 /etc/opt；在 Mac 上为 /Library/Application Support。</span><span class="sxs-lookup"><span data-stu-id="7165f-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="7165f-129">更改配置设置</span><span class="sxs-lookup"><span data-stu-id="7165f-129">Changing config settings</span></span>

<span data-ttu-id="7165f-130">`NuGet.Config` 文件是包含键/值对的简单 XML 文本文件，请参阅 [NuGet 配置设置](../reference/nuget-config-file.md)主题。</span><span class="sxs-lookup"><span data-stu-id="7165f-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="7165f-131">设置通过 NuGet CLI [config 命令](../reference/cli-reference/cli-ref-config.md)进行管理：</span><span class="sxs-lookup"><span data-stu-id="7165f-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="7165f-132">默认情况下需更改用户级配置文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="7165f-133">若要更改其他文件中的设置，请使用 `-configFile` 开关。</span><span class="sxs-lookup"><span data-stu-id="7165f-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="7165f-134">在此情况下，文件可以使用任何文件名。</span><span class="sxs-lookup"><span data-stu-id="7165f-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="7165f-135">键始终需要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="7165f-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="7165f-136">更改计算机级设置文件中的设置需要提升权限。</span><span class="sxs-lookup"><span data-stu-id="7165f-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="7165f-137">尽管可以修改任何文本编辑器中的文件，但如果配置文件中包含格式不正确的 XML（不匹配的标记、无效引号等），NuGet（v3.4.3 及更高版本）将以无提示方式忽略整个配置文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="7165f-138">因此推荐使用 `nuget config` 管理设置。</span><span class="sxs-lookup"><span data-stu-id="7165f-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="7165f-139">设置值</span><span class="sxs-lookup"><span data-stu-id="7165f-139">Setting a value</span></span>

<span data-ttu-id="7165f-140">Windows：</span><span class="sxs-lookup"><span data-stu-id="7165f-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="7165f-141">Mac/Linux：</span><span class="sxs-lookup"><span data-stu-id="7165f-141">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="7165f-142">在 NuGet 3.4 及更高版本中，可以在任何值中使用环境变量，与在 `repositoryPath=%PACKAGEHOME%` (Windows) 和 `repositoryPath=$PACKAGEHOME` (Mac/Linux) 中类似。</span><span class="sxs-lookup"><span data-stu-id="7165f-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="7165f-143">删除值</span><span class="sxs-lookup"><span data-stu-id="7165f-143">Removing a value</span></span>

<span data-ttu-id="7165f-144">若要删除值，请指定具有空值的键。</span><span class="sxs-lookup"><span data-stu-id="7165f-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="7165f-145">创建新配置文件</span><span class="sxs-lookup"><span data-stu-id="7165f-145">Creating a new config file</span></span>

<span data-ttu-id="7165f-146">将下方的模板复制到新文件中，然后使用 `nuget config -configFile <filename>` 设置值：</span><span class="sxs-lookup"><span data-stu-id="7165f-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="7165f-147">如何应用设置</span><span class="sxs-lookup"><span data-stu-id="7165f-147">How settings are applied</span></span>

<span data-ttu-id="7165f-148">可使用多个 `NuGet.Config` 文件在不同位置存储设置，以便设置可应用于单个项目、一组项目或所有项目。</span><span class="sxs-lookup"><span data-stu-id="7165f-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="7165f-149">这些设置共同应用于从命令行或 Visual Studio 调用的任何 NuGet 操作，并且优先应用“最靠近”项目或当前文件夹的设置。</span><span class="sxs-lookup"><span data-stu-id="7165f-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="7165f-150">具体而言，NuGet 将按照以下顺序从不同配置文件加载设置：</span><span class="sxs-lookup"><span data-stu-id="7165f-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="7165f-151">[NuGetDefaults.Config 文件](#nuget-defaults-file)，仅包含与包源相关的设置。</span><span class="sxs-lookup"><span data-stu-id="7165f-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="7165f-152">计算机级文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-152">The computer-level file.</span></span>
1. <span data-ttu-id="7165f-153">用户级文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-153">The user-level file.</span></span>
1. <span data-ttu-id="7165f-154">用 `-configFile` 指定的文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="7165f-155">按照从驱动器根目录到当前文件夹（在此文件夹中调用 nuget.exe 或此文件夹包含 Visual Studio 项目）的路径，在其中的每个文件夹中找到的文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="7165f-156">例如，如果在 c:\A\B\C 中调用命令，NuGet 将先后查找并加载 c:\,、c:\A、c:\A\B 和 c:\A\B\C 中的配置文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="7165f-157">NuGet 在这些文件中找到设置时，设置将按如下方式应用：</span><span class="sxs-lookup"><span data-stu-id="7165f-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="7165f-158">对于单项元素，NuGet 将替换以前找到的具有相同键的值。</span><span class="sxs-lookup"><span data-stu-id="7165f-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="7165f-159">也就是说，“最靠近”当前文件夹或项目的设置将替代之前找到的任何其他设置。</span><span class="sxs-lookup"><span data-stu-id="7165f-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="7165f-160">例如，如果 `NuGetDefaults.Config` 中的 `defaultPushSource` 设置存在于任何其他配置文件中，则此设置将被替代。</span><span class="sxs-lookup"><span data-stu-id="7165f-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="7165f-161">对于集合元素（如 `<packageSources>`），NuGet 会将所有配置文件中的值合并到一个集合中。</span><span class="sxs-lookup"><span data-stu-id="7165f-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="7165f-162">当给定节点中存在 `<clear />` 时，NuGet 将忽略之前为该节点定义的配置值。</span><span class="sxs-lookup"><span data-stu-id="7165f-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="7165f-163">设置演练</span><span class="sxs-lookup"><span data-stu-id="7165f-163">Settings walkthrough</span></span>

<span data-ttu-id="7165f-164">假设两个独立的驱动器上具有以下文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="7165f-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="7165f-165">随后以下位置上将有 4 个具有给定内容的 `NuGet.Config` 文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="7165f-166">（此示例不包括计算机级文件，但其与用户级文件具有相似行为。）</span><span class="sxs-lookup"><span data-stu-id="7165f-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="7165f-167">文件 A. 用户级文件（Windows 上为 `%appdata%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.config/NuGet/NuGet.Config`）：</span><span class="sxs-lookup"><span data-stu-id="7165f-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="7165f-168">文件 B. disk_drive_2/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="7165f-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="7165f-169">文件 C. disk_drive_2/Project1/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="7165f-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="7165f-170">文件 D. disk_drive_2/Project2/NuGet.Config：</span><span class="sxs-lookup"><span data-stu-id="7165f-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="7165f-171">接下来，NuGet 将按如下方式加载和应用设置，具体取决于调用设置的位置：</span><span class="sxs-lookup"><span data-stu-id="7165f-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="7165f-172">**从 disk_drive_1/users 调用**：仅使用用户级配置文件 (A) 中列出的默认存储库，因为这是 disk_drive_1 中的唯一文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="7165f-173">**从 disk_drive_2/ 或 disk_drive_/tmp 调用**：首先加载用户级文件 (A)，然后 NuGet 转到 disk_drive_2 的根目录并查找文件 (B)。</span><span class="sxs-lookup"><span data-stu-id="7165f-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="7165f-174">NuGet 还将在 /tmp 中查找配置文件，但不会找到此类文件。</span><span class="sxs-lookup"><span data-stu-id="7165f-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="7165f-175">因此，此时将使用 nuget.org 上的默认存储库、启用包还原并在 disk_drive_2/tmp 中展开包。</span><span class="sxs-lookup"><span data-stu-id="7165f-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="7165f-176">**从 disk_drive_2/Project1 或 disk_drive_2/Project1/Source 调用**：首先加载用户级文件 (A)，然后 NuGet 从 disk_drive_2 的根目录依次加载文件 (B) 和文件 (C)。</span><span class="sxs-lookup"><span data-stu-id="7165f-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="7165f-177">(C) 中的设置会替代 (B) 和 (A) 中的设置，因此安装包的 `repositoryPath` 将为 disk_drive_2/Project1/External/Packages，而非 disk_drive_2/tmp  。</span><span class="sxs-lookup"><span data-stu-id="7165f-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="7165f-178">此外，由于 (C) 清除了 `<packageSources>`，因此 nuget.org 将不再可用作源，并仅留下 `https://MyPrivateRepo/ES/nuget`。</span><span class="sxs-lookup"><span data-stu-id="7165f-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="7165f-179">**从 disk_drive_2/Project2 或 disk_drive_2/Project2/Source 调用**：首先加载用户级文件 (A)，然后依次加载文件 (B) 和文件 (D)。</span><span class="sxs-lookup"><span data-stu-id="7165f-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="7165f-180">由于未清除 `packageSources`，因此 `nuget.org` 和 `https://MyPrivateRepo/DQ/nuget` 都可用作源。</span><span class="sxs-lookup"><span data-stu-id="7165f-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="7165f-181">按 (B) 中的指定，包将在 disk_drive_2/tmp 中展开。</span><span class="sxs-lookup"><span data-stu-id="7165f-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="7165f-182">NuGet 默认文件</span><span class="sxs-lookup"><span data-stu-id="7165f-182">NuGet defaults file</span></span>

<span data-ttu-id="7165f-183">`NuGetDefaults.Config` 文件用于指定通过其安装和更新包的包源，以及控制使用 `nuget push` 发布包的默认目标。</span><span class="sxs-lookup"><span data-stu-id="7165f-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="7165f-184">由于管理员可以便捷地向开发人员和生成计算机部署一致的 `NuGetDefaults.Config` 文件（例如，使用组策略），因此他们可以确保组织中的每个人都在使用正确的包源，而不是 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="7165f-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="7165f-185">`NuGetDefaults.Config` 文件绝不会导致开发人员 NuGet 配置中的包源被删除。</span><span class="sxs-lookup"><span data-stu-id="7165f-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="7165f-186">也就是说，如果开发人员已使用 NuGet，即意味着已注册 nuget.org 包源，创建 `NuGetDefaults.Config` 文件后将不会删除此包源。</span><span class="sxs-lookup"><span data-stu-id="7165f-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="7165f-187">此外，NuGet 中的 `NuGetDefaults.Config` 或任何其他机制都不会阻止访问 nuget.org 等包源。如果组织希望阻止此类访问，则必须通过其他方式（如防火墙）实现。</span><span class="sxs-lookup"><span data-stu-id="7165f-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="7165f-188">NuGetDefaults.Config 的位置</span><span class="sxs-lookup"><span data-stu-id="7165f-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="7165f-189">下表根据目标操作系统描述 `NuGetDefaults.Config` 文件应存储的位置：</span><span class="sxs-lookup"><span data-stu-id="7165f-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="7165f-190">操作系统平台</span><span class="sxs-lookup"><span data-stu-id="7165f-190">OS Platform</span></span>  | <span data-ttu-id="7165f-191">NuGetDefaults.Config 的位置</span><span class="sxs-lookup"><span data-stu-id="7165f-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="7165f-192">Windows</span><span class="sxs-lookup"><span data-stu-id="7165f-192">Windows</span></span>      | <span data-ttu-id="7165f-193">**Visual Studio 2017 或 NuGet 4.x+：** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="7165f-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="7165f-194">**Visual Studio 2015 及更低版本或 NuGet 3.x 及更低版本：** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="7165f-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="7165f-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7165f-195">Mac/Linux</span></span>    | <span data-ttu-id="7165f-196">`$XDG_DATA_HOME`（通常为 `~/.local/share` 或 `/usr/local/share`，具体视 OS 版本而定）</span><span class="sxs-lookup"><span data-stu-id="7165f-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="7165f-197">NuGetDefaults.Config 的设置</span><span class="sxs-lookup"><span data-stu-id="7165f-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="7165f-198">`packageSources`：此集合与常规配置文件中的 `packageSources` 具有相同含义，并可指定默认源。</span><span class="sxs-lookup"><span data-stu-id="7165f-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="7165f-199">在使用 `packages.config` 管理格式的项目中安装或更新包时，NuGet 会按顺序使用源。</span><span class="sxs-lookup"><span data-stu-id="7165f-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="7165f-200">对于使用 PackageReference 格式的项目，NuGet 会先使用本地源，再使用网络共享上的源，最后使用 HTTP 源，而不管配置文件中的顺序如何。</span><span class="sxs-lookup"><span data-stu-id="7165f-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="7165f-201">NuGet 会始终忽略还原操作的源顺序。</span><span class="sxs-lookup"><span data-stu-id="7165f-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="7165f-202">`disabledPackageSources`：此集合还与在 `NuGet.Config` 文件中时具有相同含义，集合中将列出每个受影响源的名称，并用 true/false 值指示源是否已禁用。</span><span class="sxs-lookup"><span data-stu-id="7165f-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="7165f-203">这可使源名称和 URL 保留在 `packageSources` 中，但不会将其默认打开。</span><span class="sxs-lookup"><span data-stu-id="7165f-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="7165f-204">开发人员随后可在其他 `NuGet.Config` 文件中将源的值设置为 false，以便重新启用源，而无需再次寻找正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="7165f-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="7165f-205">开发人员还可通过此方法获取组织的内部源 URL 完整列表，同时仅默认启用一个团队的源。</span><span class="sxs-lookup"><span data-stu-id="7165f-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="7165f-206">`defaultPushSource`：指定 `nuget push` 操作的默认目标，同时替代 nuget.org 的内置默认值。管理员可部署此设置以避免误将内部包发布到公共 nuget.org，因为开发人员专门负责使用 `nuget push -Source` 向 nuget.org 发布。</span><span class="sxs-lookup"><span data-stu-id="7165f-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="7165f-207">示例 NuGetDefaults.Config 和应用程序</span><span class="sxs-lookup"><span data-stu-id="7165f-207">Example NuGetDefaults.Config and application</span></span>

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
