---
title: 在 Windows 上使用 Visual Studio 创建和发布 .NET Standard NuGet 包
description: 在 Windows 上使用 Visual Studio 创建和发布 .NET Standard NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419923"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="c99e2-103">快速入门：使用 Visual Studio 创建和发布 NuGet 包（仅限 .NET Standard 和 Windows）</span><span class="sxs-lookup"><span data-stu-id="c99e2-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="c99e2-104">从 Windows 上 Visual Studio 中的 .NET Standard 类库创建 NuGet 包，然后使用 CLI 工具将其发布到 nuget.org，这是一个很简单的过程。</span><span class="sxs-lookup"><span data-stu-id="c99e2-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="c99e2-105">如果使用的是 Visual Studio for Mac，请参阅有关创建 NuGet 包的[以下信息](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)或使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c99e2-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c99e2-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="c99e2-106">Prerequisites</span></span>

1. <span data-ttu-id="c99e2-107">通过与 .NET Core 相关的工作负载从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2017 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="c99e2-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="c99e2-108">如果尚未安装，则安装 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="c99e2-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="c99e2-109">对于 `dotnet` CLI，从 Visual Studio 2017 开始，`dotnet` CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="c99e2-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="c99e2-110">否则，请安装 [.NET Core SDK](https://www.microsoft.com/net/download/) 以获取 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="c99e2-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="c99e2-111">`dotnet` CLI 是使用 [SDK 样式格式](../resources/check-project-format.md)（SDK 属性）的 .NET Standard 项目所必需的。</span><span class="sxs-lookup"><span data-stu-id="c99e2-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="c99e2-112">Visual Studio 2017 及更高版本中的默认类库模板（本文所用模板）使用 SDK 属性。</span><span class="sxs-lookup"><span data-stu-id="c99e2-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="c99e2-113">对于本文，建议使用 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="c99e2-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="c99e2-114">虽然可以使用 `nuget.exe` CLI 发布任何 NuGet 包，但本文中的某些步骤特定于 SDK 样式的项目和 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="c99e2-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="c99e2-115">nuget.exe CLI 用于[非 SDK 样式的项目](../resources/check-project-format.md)（通常为 .NET Framework）。</span><span class="sxs-lookup"><span data-stu-id="c99e2-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="c99e2-116">如果使用的是非 SDK 样式的项目，请按照[创建和发布 .NET Framework 包 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) 中的过程来创建和发布包。</span><span class="sxs-lookup"><span data-stu-id="c99e2-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="c99e2-117">如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account)。</span><span class="sxs-lookup"><span data-stu-id="c99e2-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="c99e2-118">创建新帐户会发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c99e2-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c99e2-119">必须先确认该帐户，才能上传包。</span><span class="sxs-lookup"><span data-stu-id="c99e2-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c99e2-120">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="c99e2-120">Create a class library project</span></span>

<span data-ttu-id="c99e2-121">可以使用现有的 .NET Standard 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c99e2-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c99e2-122">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C# > .NET Standard”节点，选择“类库 (.NET Standard)”模板，将项目命名为“AppLogger”，然后单击“确定”。   </span><span class="sxs-lookup"><span data-stu-id="c99e2-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="c99e2-123">右键单击生成的项目文件并选择“生成”，确保已正确创建项目。 </span><span class="sxs-lookup"><span data-stu-id="c99e2-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="c99e2-124">DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。</span><span class="sxs-lookup"><span data-stu-id="c99e2-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="c99e2-125">当然，在实际的 NuGet 包中，可实现许多有用的功能，让其他人可通过这些功能生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="c99e2-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="c99e2-126">但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。</span><span class="sxs-lookup"><span data-stu-id="c99e2-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="c99e2-127">但是，如果你需要此程序包的某个功能代码，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="c99e2-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="c99e2-128">除非你有其他选择理由，否则 .NET Standard 是 NuGet 包的首选目标，因为它提供了与最广泛的使用项目的兼容性。</span><span class="sxs-lookup"><span data-stu-id="c99e2-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="c99e2-129">配置包属性</span><span class="sxs-lookup"><span data-stu-id="c99e2-129">Configure package properties</span></span>

1. <span data-ttu-id="c99e2-130">在解决方案资源管理器中右键单击该项目，然后选择“属性”  菜单命令，然后选择“包”  选项卡。</span><span class="sxs-lookup"><span data-stu-id="c99e2-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="c99e2-131">“包”  选项卡仅在 Visual Studio 的 SDK 样式项目中显示，通常是 .NET Standard 或 .NET Core 类库项目；如果要针对非 SDK 样式项目（通常是 .NET Framework），请[迁移项目](../reference/migrate-packages-config-to-package-reference.md)并使用 `dotnet` CLI，或参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)或者改为参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)，以获取分步说明。</span><span class="sxs-lookup"><span data-stu-id="c99e2-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio 项目中的 NuGet 包属性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="c99e2-133">对于面向公共使用而生成的包，请特别注意 **Tags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="c99e2-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="c99e2-134">为包提供一个唯一标识符，并填写任何其他所需的属性。</span><span class="sxs-lookup"><span data-stu-id="c99e2-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="c99e2-135">有关不同属性的说明，请参阅 [.nuspec 文件引用](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="c99e2-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="c99e2-136">这里的所有属性都列入 Visual Studio 为项目创建的 `.nuspec` 清单。</span><span class="sxs-lookup"><span data-stu-id="c99e2-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="c99e2-137">你必须为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。</span><span class="sxs-lookup"><span data-stu-id="c99e2-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c99e2-138">对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。</span><span class="sxs-lookup"><span data-stu-id="c99e2-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="c99e2-139">如果你尝试发布名称已存在的包，则会看到一个错误。</span><span class="sxs-lookup"><span data-stu-id="c99e2-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="c99e2-140">可选：若要直接查看项目文件中的属性，请右击“解决方案资源管理器”中的“项目”，然后选择“编辑 AppLogger.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="c99e2-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="c99e2-141">此选项从 Visual Studio 2017 开始仅对使用 SDK 样式属性的项目可用。</span><span class="sxs-lookup"><span data-stu-id="c99e2-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="c99e2-142">否则，右键单击项目，并选择“卸载项目”  。</span><span class="sxs-lookup"><span data-stu-id="c99e2-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="c99e2-143">然后右键单击卸载的项目并选择“编辑 AppLogger.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="c99e2-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c99e2-144">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="c99e2-144">Run the pack command</span></span>

1. <span data-ttu-id="c99e2-145">将此配置设置为“发布”  。</span><span class="sxs-lookup"><span data-stu-id="c99e2-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="c99e2-146">请在“解决方案资源管理器”中右键单击该项目，然后选择“Pack”命令：  </span><span class="sxs-lookup"><span data-stu-id="c99e2-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 项目上下文菜单上的 NuGet pack 命令](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="c99e2-148">如果没有看到“Pack”  命令，那么项目可能不是 SDK 样式的项目，需要使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="c99e2-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="c99e2-149">[迁移项目](../reference/migrate-packages-config-to-package-reference.md)并使用 `dotnet` CLI，或者改为参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)，以获取分步说明。</span><span class="sxs-lookup"><span data-stu-id="c99e2-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="c99e2-150">Visual Studio 构建项目并创建 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="c99e2-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="c99e2-151">检查“输出”  窗口以查看详细信息（类似于以下内容），其中包含包文件的路径。</span><span class="sxs-lookup"><span data-stu-id="c99e2-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="c99e2-152">另请注意，生成的程序集位于适合 .NET Standard 2.0 目标的 `bin\Release\netstandard2.0` 中。</span><span class="sxs-lookup"><span data-stu-id="c99e2-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="c99e2-153">备用选项：使用 MSBuild 打包</span><span class="sxs-lookup"><span data-stu-id="c99e2-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="c99e2-154">作为使用“打包”菜单命令的备选项，当项目包含必要的包数据时，NuGet 4.x+ 和 MSBuild 15.1+ 支持 `pack` 目标  。</span><span class="sxs-lookup"><span data-stu-id="c99e2-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="c99e2-155">打开命令提示符，导航到项目文件夹并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="c99e2-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="c99e2-156">（用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置。）</span><span class="sxs-lookup"><span data-stu-id="c99e2-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="c99e2-157">然后可在 `bin\Release` 文件夹中找到此包。</span><span class="sxs-lookup"><span data-stu-id="c99e2-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="c99e2-158">有关 `msbuild -t:pack` 的其他选项，请参阅 [NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="c99e2-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="c99e2-159">发布包</span><span class="sxs-lookup"><span data-stu-id="c99e2-159">Publish the package</span></span>

<span data-ttu-id="c99e2-160">有了 `.nupkg` 文件后，可以使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c99e2-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c99e2-161">获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="c99e2-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="c99e2-162">用 dotnet nuget push 发布 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="c99e2-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="c99e2-163">此步骤是使用 `nuget.exe` 的推荐替代方法。</span><span class="sxs-lookup"><span data-stu-id="c99e2-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="c99e2-164">在发布包之前，必须先打开命令行。</span><span class="sxs-lookup"><span data-stu-id="c99e2-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="c99e2-165">用 nuget push 发布 (nuget.exe CLI)</span><span class="sxs-lookup"><span data-stu-id="c99e2-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="c99e2-166">该步骤是使用 `dotnet.exe` 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="c99e2-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="c99e2-167">打开命令行并更改到包含 `.nupkg` 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c99e2-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="c99e2-168">运行以下命令，指定包名称（唯一包 ID）并使用你的 API 密钥替换密钥值：</span><span class="sxs-lookup"><span data-stu-id="c99e2-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="c99e2-169">nuget.exe 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="c99e2-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="c99e2-170">请参阅 [nuget push](../reference/cli-reference/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="c99e2-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="c99e2-171">发布错误</span><span class="sxs-lookup"><span data-stu-id="c99e2-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="c99e2-172">管理已发布的包</span><span class="sxs-lookup"><span data-stu-id="c99e2-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="c99e2-173">添加自述文件和其他文件</span><span class="sxs-lookup"><span data-stu-id="c99e2-173">Adding a readme and other files</span></span>

<span data-ttu-id="c99e2-174">若要直接指定要包含在包中的文件，请编辑项目文件并使用 `content` 属性：</span><span class="sxs-lookup"><span data-stu-id="c99e2-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="c99e2-175">这将在包根目录中包含一个名为 `readme.txt` 的文件。</span><span class="sxs-lookup"><span data-stu-id="c99e2-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="c99e2-176">Visual Studio 在直接安装包之后立即将该文件的内容显示为纯文本。</span><span class="sxs-lookup"><span data-stu-id="c99e2-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="c99e2-177">（对于安装为依赖项的包，不会显示自述文件）。</span><span class="sxs-lookup"><span data-stu-id="c99e2-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="c99e2-178">例如，下面是 HtmlAgilityPack 包的自述文件的显示方式：</span><span class="sxs-lookup"><span data-stu-id="c99e2-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安装时 NuGet 包的自述文件的显示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="c99e2-180">只在项目根目录添加 readme.txt 不会导致它被包含在生成的包中。</span><span class="sxs-lookup"><span data-stu-id="c99e2-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="c99e2-181">相关主题</span><span class="sxs-lookup"><span data-stu-id="c99e2-181">Related topics</span></span>

- [<span data-ttu-id="c99e2-182">创建包</span><span class="sxs-lookup"><span data-stu-id="c99e2-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="c99e2-183">发布包</span><span class="sxs-lookup"><span data-stu-id="c99e2-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="c99e2-184">预发行包</span><span class="sxs-lookup"><span data-stu-id="c99e2-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="c99e2-185">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="c99e2-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="c99e2-186">包版本控制</span><span class="sxs-lookup"><span data-stu-id="c99e2-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c99e2-187">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="c99e2-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c99e2-188">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="c99e2-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="c99e2-189">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="c99e2-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
