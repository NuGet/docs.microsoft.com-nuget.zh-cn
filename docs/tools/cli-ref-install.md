---
title: NuGet CLI 安装命令
description: Nuget.exe install 命令的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549131"
---
# <a name="install-command-nuget-cli"></a>install 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**支持的版本：** 所有

下载并安装到项目后，默认设置为当前文件夹中，使用指定的包源的包。

> [!Tip]
> 若要下载的包直接在项目的上下文以外，访问包的页面上[nuget.org](https://www.nuget.org) ，然后选择**下载**链接。

如果指定了不到源，那些在全局配置文件中，列出`%appdata%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。 请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)有关其他详细信息。

如果未不指定任何特定的包，`install`安装在项目中列出的所有包`packages.config`文件，使它类似于[ `restore` ](cli-ref-restore.md)。

`install`命令不会修改项目文件或`packages.config`; 在这种方式是类似于`restore`它仅将包添加到磁盘而不会更改项目的依赖项。

若要添加依赖项，请在 Visual Studio 中，添加一个包通过包管理器 UI 或控制台或修改`packages.config`，然后运行任一`install`或`restore`。

## <a name="usage"></a>用法

```cli
nuget install <packageID | configFilePath> [options]
```

其中`<packageID>`名称的包安装 （使用最新版本），或`<configFilePath>`标识`packages.config`文件，其中列出要安装的包。 您可以指示与特定版本`-Version`选项。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| DependencyVersion | *（4.4 +)* 版本的依赖项包使用，可以是以下值之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</li><li>*最高*： 最高版本</li></ul> |
| DisableParallelProcessing | 禁用并行安装多个包。 |
| ExcludeVersion | 将包安装到仅包名称而不是版本数字与名为的文件夹。 |
| FallbackSource | *（3.2 +)* 要用作回退，如果主数据库中找不到包的包源的列表或默认源。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 框架 | *（4.4 +)* 用于选择依赖关系的目标框架。 默认值为 Any 如果未指定。 |
| 帮助 | 显示的帮助命令的信息。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定在其中安装包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 |
| PackageSaveMode | 指定要将包安装完成后保存的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| 预发行版 | 允许要安装的预发行包。 还原包时，此标志不是必需`packages.config`。 |
| RequireConsent | 验证下载和安装包之前已启用还原包。 有关详细信息，请参阅[包还原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要为其还原包解决方案的根文件夹。 |
| 源 | 指定包源的列表 （作为 Url) 来使用。 如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |
| 版本 | 指定要安装的包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
