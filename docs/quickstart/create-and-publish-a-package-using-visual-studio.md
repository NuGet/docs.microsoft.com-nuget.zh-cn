---
title: 在 Windows 上使用 Visual Studio 创建和发布 .NET Standard 包
description: 在 Windows 上使用 Visual Studio 2017 创建和发布 .NET Standard NuGet 包的演练教程。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: e97773d79b22db1f08d868190895a9417b12c924
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963082"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>快速入门：使用 Visual Studio 创建和发布 NuGet 包（仅限 .NET Standard 和 Windows）

从 Windows 上 Visual Studio 中的 .NET Standard 类库创建 NuGet 包，然后使用 CLI 工具将其发布到 nuget.org，这是一个很简单的过程。

> [!Note]
> 本快速入门教程仅适用于 Visual Studio 2017 for Windows。 Visual Studio for Mac 不包括此处所述的功能。 改为使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。

## <a name="prerequisites"></a>系统必备

1. 通过任何与 .NET 相关的工作负载从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2017。 安装 .NET 工作负载时，Visual Studio 2017 会自动包含 NuGet 功能。

1. 要安装 `nuget.exe` CLI，从 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下载它，将 `.exe` 文件保存到合适的文件夹，然后将该文件夹添加到 PATH 环境变量中。

    或者，如果安装了 [.NET Core SDK](https://www.microsoft.com/net/download/)，则可以使用 `dotnet` CLI。

1. 如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)。 创建新帐户会发送确认电子邮件。 必须先确认该帐户，才能上传包。

## <a name="create-a-class-library-project"></a>创建类库项目

可以使用现有的 .NET Standard 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C# > .NET Standard”节点，选择“类库 (.NET Standard)”模板，将项目命名为“AppLogger”，然后单击“确定”。

1. 右键单击生成的项目文件并选择“生成”，确保已正确创建项目。 DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。

当然，在实际的 NuGet 包中，可实现许多有用的功能，让其他人可通过这些功能生成应用程序。 但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。 但是，如果你需要此程序包的某个功能代码，请使用以下命令：

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> 除非你有其他选择理由，否则 .NET Standard 是 NuGet 包的首选目标，因为它提供了与最广泛的使用项目的兼容性。

## <a name="configure-package-properties"></a>配置包属性

1. 选择“项目”>“属性”菜单命令，然后选择“包”选项卡。（“包”选项卡仅出现在 .NET Standard 类库项目中；如果要面向 .NET Framework，请参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)。 如果未出现在 .NET Standard 项目中，可能需要将 Visual Studio 2017 更新到最新版本。）

    ![Visual Studio 项目中的 NuGet 包属性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > 对于面向公共使用而生成的包，请特别注意 **Tags** 属性，因为这些标记可帮助其他人查找包并了解其用途。

1. 为包提供一个唯一标识符，并填写任何其他所需的属性。 有关不同属性的说明，请参阅 [.nuspec 文件引用](../reference/nuspec.md)。 这里的所有属性都列入 Visual Studio 为项目创建的 `.nuspec` 清单。

    > [!Important]
    > 你必须为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。 对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。
    >
    > 如果你尝试发布名称已存在的包，则会看到一个错误。

1. 可选：若要直接查看项目文件中的属性，请右击“解决方案资源管理器”中的“项目”，然后选择“编辑 AppLogger.csproj”。

## <a name="run-the-pack-command"></a>运行 pack 命令

1. 将此配置设置为“发布”。

1. 请在“解决方案资源管理器”中右键单击该项目，然后选择“Pack”命令：

    ![Visual Studio 项目上下文菜单上的 NuGet pack 命令](media/qs_create-vs-02-pack-command.png)

1. Visual Studio 构建项目并创建 `.nupkg` 文件。 检查“输出”窗口以查看详细信息（类似于以下内容），其中包含包文件的路径。 另请注意，生成的程序集位于适合 .NET Standard 2.0 目标的 `bin\Release\netstandard2.0` 中。

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>备用选项：使用 MSBuild 打包

作为使用“打包”菜单命令的备选项，当项目包含必要的包数据时，NuGet 4.x+ 和 MSBuild 15.1+ 支持 `pack` 目标。 打开命令提示符，导航到项目文件夹并运行以下命令。 （用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置。）

```cli
msbuild /t:pack /p:Configuration=Release
```

然后可在 `bin\Release` 文件夹中找到此包。

有关 `msbuild /t:pack` 的其他选项，请参阅 [NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md#pack-target)。

## <a name="publish-the-package"></a>发布包

有了 `.nupkg` 文件后，可以使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>获取 API 密钥

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>用 nuget push 发布

该步骤是使用 `dotnet.exe` 的替代方法。

1. 更改到包含 `.nupkg` 文件的文件夹。

1. 运行以下命令，指定包名称并使用你的 API 密钥替换密钥值：

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe 会显示发布过程的结果：

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

请参阅 [nuget push](../tools/cli-ref-push.md)。

### <a name="publish-with-dotnet-nuget-push"></a>用 dotnet nuget push 发布

该步骤是使用 `nuget.exe` 的替代方法。

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>发布错误

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已发布的包

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>相关主题

- [创建包](../create-packages/creating-a-package.md)
- [发布包](../create-packages/publish-a-package.md)
- [预发行包](../create-packages/Prerelease-Packages.md)
- [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)
- [包版本控制](../reference/package-versioning.md)
- [创建本地化包](../create-packages/creating-localized-packages.md)
- [.NET Standard 库文档](/dotnet/articles/standard/library)
- [从 .NET Framework 移植到 .NET Core](/dotnet/articles/core/porting/index)
