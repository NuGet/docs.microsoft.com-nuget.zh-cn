---
title: 配置 NuGet 的行为
description: NuGet.Config 文件同时以全局方式和基于每个项目的方式控制 NuGet 的行为，并且这些文件可使用 nuget config 命令进行修改。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c8cc78be1bd48adc603b9447282a6c4bef7f942f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="configuring-nuget-behavior"></a>配置 NuGet 行为

NuGet 的行为由一个或多个 `NuGet.Config` (XML) 文件（可存在于项目范围、用户范围和计算机范围的级别）中的累积设置驱动。 还可以使用全局 `NuGetDefaults.Config` 文件专门配置包源。 这些设置应用于 CLI、包管理器控制台和包管理器 UI 中发出的所有命令。

## <a name="config-file-locations-and-uses"></a>配置文件的位置和使用

| 范围 | NuGet.Config 文件的位置 | 描述 |
| --- | --- | --- |
| 项目 | 当前文件夹（aka 项目文件夹）或上至驱动器根目录的任何文件夹。| 在项目文件夹中，设置仅应用于该项目。 在包含多个项目子文件夹的父文件夹中，设置应用于这些子文件夹中的所有项目。 |
| “用户” | Windows：`%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux：`~/.config/NuGet/NuGet.Config` 或 `~/.nuget/NuGet/NuGet.Config`（因 OS 版本而异） | 设置应用于所有操作，但可被任何项目级的设置替代。 |
| 计算机 | Windows：`%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux：`$XDG_DATA_HOME`。 如果 `$XDG_DATA_HOME` 的值是 null 或为空，将使用 `~/.local/share` 或 `/usr/local/share`（因 OS 版本而异）  | 设置虽然适用于计算机上的所有操作，但会被任何用户级或项目级设置覆盖。 |

针对早期版本的 NuGet 的说明：
- NuGet 3.3 及更早版本使用 `.nuget` 文件夹作为解决方案范围的设置。 NuGet 3.4+ 中不使用此文件。
- 对于 NuGet 2.6 到 3.x 版本，Windows 上的计算机级配置文件位于 %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config，其中，{IDE} 可能为 VisualStudio，{Version} 为 Visual Studio 的版本（如 14.0），{SKU} 可能为 Community、Pro 或 Enterprise。 若要将设置迁移到 NuGet 4.0+，只需将配置文件复制到 %ProgramFiles(x86)%\NuGet\Config 即可。在 Linux 上，此位置以前为 /etc/opt；在 Mac 上为 /Library/Application Support。

## <a name="changing-config-settings"></a>更改配置设置

`NuGet.Config` 文件是包含键/值对的简单 XML 文本文件，请参阅 [NuGet 配置设置](../reference/nuget-config-file.md)主题。

设置通过 NuGet CLI [config 命令](../tools/cli-ref-config.md)进行管理：
- 默认情况下需更改用户级配置文件。
- 若要更改其他文件中的设置，请使用 `-configFile` 开关。 在此情况下，文件可以使用任何文件名。
- 键始终需要区分大小写。
- 更改计算机级设置文件中的设置需要提升权限。

> [!Warning]
> 尽管可以修改任何文本编辑器中的文件，但如果配置文件中包含格式不正确的 XML（不匹配的标记、无效引号等），NuGet（v3.4.3 及更高版本）将以无提示方式忽略整个配置文件。 因此推荐使用 `nuget config` 管理设置。

### <a name="setting-a-value"></a>设置值

Windows：

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

Mac/Linux：

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
> 在 NuGet 3.4 及更高版本中，可以在任何值中使用环境变量，与在 `repositoryPath=%PACKAGEHOME%` (Windows) 和 `repositoryPath=%PACKAGEHOME` (Mac/Linux) 中类似。

### <a name="removing-a-value"></a>删除值

若要删除值，请指定具有空值的键。

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>创建新配置文件

将下方的模板复制到新文件中，然后使用 `nuget config -configFile <filename>` 设置值：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>如何应用设置

可使用多个 `NuGet.Config` 文件在不同位置存储设置，以便设置可应用于单个项目、一组项目或所有项目。 这些设置共同应用于从命令行或 Visual Studio 调用的任何 NuGet 操作，并且优先应用“最靠近”项目或当前文件夹的设置。

具体而言，NuGet 将按照以下顺序从不同配置文件加载设置：

1. [NuGetDefaults.Config 文件](#nuget-defaults-file)，仅包含与包源相关的设置。
1. 计算机级文件。
1. 用户级文件。
1. 用 `-configFile` 指定的文件。
1. 按照从驱动器根目录到当前文件夹（在此文件夹中调用 nuget.exe 或此文件夹包含 Visual Studio 项目）的路径，在其中的每个文件夹中找到的文件。 例如，如果在 c:\A\B\C 中调用命令，NuGet 将先后查找并加载 c:\,、c:\A、c:\A\B 和 c:\A\B\C 中的配置文件。

NuGet 在这些文件中找到设置时，设置将按如下方式应用：

1. 对于单项元素，NuGet 将替换以前找到的具有相同键的值。 也就是说，“最靠近”当前文件夹或项目的设置将替代之前找到的任何其他设置。 例如，如果 `NuGetDefaults.Config` 中的 `defaultPushSource` 设置存在于任何其他配置文件中，则此设置将被替代。

1. 对于集合元素（如 `<packageSources>`），NuGet 会将所有配置文件中的值合并到一个集合中。

1. 当给定节点中存在 `<clear />` 时，NuGet 将忽略之前为该节点定义的配置值。

### <a name="settings-walkthrough"></a>设置演练

假设两个独立的驱动器上具有以下文件夹结构：

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

随后以下位置上将有 4 个具有给定内容的 `NuGet.Config` 文件。 （此示例不包括计算机级文件，但其与用户级文件具有相似行为。）

文件 A. 用户级文件（Windows 上为 `%appdata%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.config/NuGet/NuGet.Config`）：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

文件 B. disk_drive_2/NuGet.Config：

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

文件 C. disk_drive_2/Project1/NuGet.Config：

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

文件 D. disk_drive_2/Project2/NuGet.Config：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

接下来，NuGet 将按如下方式加载和应用设置，具体取决于调用设置的位置：

- **从 disk_drive_1/users 调用**：仅使用用户级配置文件 (A) 中列出的默认存储库，因为这是在 disk_drive_1 中找到的唯一文件。

- **从 disk_drive_2/ 或 disk_drive_/tmp 调用**：首先加载用户级文件 (A)，然后 NuGet 转到 disk_drive_2 的根目录并查找文件 (B)。 NuGet 还将在 /tmp 中查找配置文件，但不会找到此类文件。 因此，此时将使用 nuget.org 上的默认存储库、启用包还原并在 disk_drive_2/tmp 中展开包。

- **从 disk_drive_2/Project1 或 disk_drive_2/Project1/Source 调用**：首先加载用户级文件 (A)，然后 NuGet 依次加载 disk_drive_2 根目录中的文件 (B) 和文件 (C)。 (C) 中的设置会替代 (B) 和 (A) 中的设置，因此安装包的 `repositoryPath` 将为 disk_drive_2/Project1/External/Packages，而非 disk_drive_2/tmp。 此外，由于 (C) 清除了 `<packageSources>`，因此 nuget.org 将不再可用作源，并仅留下 `https://MyPrivateRepo/ES/nuget`。

- **从 disk_drive_2/Project2 或 disk_drive_2/Project2/Source 调用**：首先加载用户级文件 (A)，然后依次加载文件 (B) 和文件 (D)。 由于未清除 `packageSources`，因此 `nuget.org` 和 `https://MyPrivateRepo/DQ/nuget` 都可用作源。 按 (B) 中的指定，包将在 disk_drive_2/tmp 中展开。

## <a name="nuget-defaults-file"></a>NuGet 默认文件

`NuGetDefaults.Config` 文件用于指定通过其安装和更新包的包源，以及控制使用 `nuget push` 发布包的默认目标。 管理员可以轻松向开发人员和生成计算机部署一致的 `NuGetDefaults.Config` 文件（例如使用组策略），因此他们可以确保组织中的每位用户使用正确的包源，而不是 nuget.org。

> [!Important]
> `NuGetDefaults.Config` 文件绝不会导致开发人员 NuGet 配置中的包源被删除。 也就是说，如果开发人员已使用 NuGet，即意味着已注册 nuget.org 包源，创建 `NuGetDefaults.Config` 文件后将不会删除此包源。
>
> 此外，NuGet 中的 `NuGetDefaults.Config` 或任何其他机制都不会阻止访问 nuget.org 等包源。如果组织希望阻止此类访问，则必须通过其他方式（如防火墙）实现。

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config 的位置

下表根据目标操作系统描述 `NuGetDefaults.Config` 文件应存储的位置：

| 操作系统平台  | NuGetDefaults.Config 的位置 |
| --- | --- |
| Windows      | **Visual Studio 2017 或 NuGet 4.x+：**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 及更低版本或 NuGet 3.x 及更低版本：**`%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME`（通常为 `~/.local/share` 或 `/usr/local/share`，具体视 OS 版本而定）|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config 的设置

- `packageSources`：此集合与常规配置文件中的 `packageSources` 具有相同含义，并可指定默认源。 在使用 `packages.config` 管理格式的项目中安装或更新包时，NuGet 会按顺序使用源。 对于使用 PackageReference 格式的项目，NuGet 会先使用本地源，再使用网络共享上的源，最后使用 HTTP 源，而不管配置文件中的顺序如何。 NuGet 会始终忽略还原操作的源顺序。

- `disabledPackageSources`：此集合还与在 `NuGet.Config` 文件中时具有相同含义，集合中将列出每个受影响源的名称，并用 true/false 值指示源是否已禁用。 这可使源名称和 URL 保留在 `packageSources` 中，但不会将其默认打开。 开发人员随后可在其他 `NuGet.Config` 文件中将源的值设置为 false，以便重新启用源，而无需再次寻找正确的 URL。 开发人员还可通过此方法获取组织的内部源 URL 完整列表，同时仅默认启用一个团队的源。

- `defaultPushSource`：指定 `nuget push` 操作的默认目标，同时替代 nuget.org 的内置默认值。管理员可部署此设置以避免误将内部包发布到公共 nuget.org，因为开发人员专门负责使用 `nuget push -Source` 向 nuget.org 发布。

### <a name="example-nugetdefaultsconfig-and-application"></a>示例 NuGetDefaults.Config 和应用程序

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
