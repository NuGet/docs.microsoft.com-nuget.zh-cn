---
title: 在 Windows 上使用 Visual Studio 创建和发布 .NET Standard NuGet 包
description: 在 Windows 上使用 Visual Studio 创建和发布 .NET Standard NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428641"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="3ee36-103">快速入门：使用 Visual Studio 创建和发布 NuGet 包（仅限 .NET Standard 和 Windows）</span><span class="sxs-lookup"><span data-stu-id="3ee36-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="3ee36-104">从 Windows 上 Visual Studio 中的 .NET Standard 类库创建 NuGet 包，然后使用 CLI 工具将其发布到 nuget.org，这是一个很简单的过程。</span><span class="sxs-lookup"><span data-stu-id="3ee36-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="3ee36-105">如果使用的是 Visual Studio for Mac，请参阅有关创建 NuGet 包的[以下信息](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)或使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee36-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ee36-106">先决条件</span><span class="sxs-lookup"><span data-stu-id="3ee36-106">Prerequisites</span></span>

1. <span data-ttu-id="3ee36-107">通过与 .NET Core 相关的工作负载从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="3ee36-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="3ee36-108">如果尚未安装，则安装 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="3ee36-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="3ee36-109">对于 `dotnet` CLI，从 Visual Studio 2017 开始，`dotnet` CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="3ee36-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="3ee36-110">否则，请安装 [.NET Core SDK](https://www.microsoft.com/net/download/) 以获取 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="3ee36-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="3ee36-111">`dotnet` CLI 是使用 [SDK 样式格式](../resources/check-project-format.md)（SDK 属性）的 .NET Standard 项目所必需的。</span><span class="sxs-lookup"><span data-stu-id="3ee36-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="3ee36-112">Visual Studio 2017 及更高版本中的默认 .NET Standard 类库模板（本文所用模板）使用 SDK 属性。</span><span class="sxs-lookup"><span data-stu-id="3ee36-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="3ee36-113">如果使用的是非 SDK 样式的项目，请改为按照[创建和发布 .NET Framework 包 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) 中的过程来创建和发布包。</span><span class="sxs-lookup"><span data-stu-id="3ee36-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="3ee36-114">对于本文，建议使用 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="3ee36-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="3ee36-115">虽然可以使用 `nuget.exe` CLI 发布任何 NuGet 包，但本文中的某些步骤特定于 SDK 样式的项目和 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="3ee36-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="3ee36-116">nuget.exe CLI 用于[非 SDK 样式的项目](../resources/check-project-format.md)（通常为 .NET Framework）。</span><span class="sxs-lookup"><span data-stu-id="3ee36-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="3ee36-117">如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](../nuget-org/individual-accounts.md#add-a-new-individual-account)。</span><span class="sxs-lookup"><span data-stu-id="3ee36-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="3ee36-118">创建新帐户会发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="3ee36-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="3ee36-119">必须先确认该帐户，才能上传包。</span><span class="sxs-lookup"><span data-stu-id="3ee36-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="3ee36-120">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="3ee36-120">Create a class library project</span></span>

<span data-ttu-id="3ee36-121">可以使用现有的 .NET Standard 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ee36-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="3ee36-122">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C# > .NET Standard”节点，选择“类库 (.NET Standard)”模板，将项目命名为“AppLogger”，然后单击“确定”。   </span><span class="sxs-lookup"><span data-stu-id="3ee36-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="3ee36-123">除非你有其他选择理由，否则 .NET Standard 是 NuGet 包的首选目标，因为它提供了与最广泛的使用项目的兼容性。</span><span class="sxs-lookup"><span data-stu-id="3ee36-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="3ee36-124">右键单击生成的项目文件并选择“生成”，确保已正确创建项目。 </span><span class="sxs-lookup"><span data-stu-id="3ee36-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="3ee36-125">DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。</span><span class="sxs-lookup"><span data-stu-id="3ee36-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="3ee36-126">当然，在实际的 NuGet 包中，可实现许多有用的功能，让其他人可通过这些功能生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ee36-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="3ee36-127">但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。</span><span class="sxs-lookup"><span data-stu-id="3ee36-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="3ee36-128">但是，如果你需要此程序包的某个功能代码，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="3ee36-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="3ee36-129">配置包属性</span><span class="sxs-lookup"><span data-stu-id="3ee36-129">Configure package properties</span></span>

1. <span data-ttu-id="3ee36-130">在解决方案资源管理器中右键单击该项目，然后选择“属性”  菜单命令，然后选择“包”  选项卡。</span><span class="sxs-lookup"><span data-stu-id="3ee36-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="3ee36-131">“包”  选项卡仅在 Visual Studio 的 SDK 样式项目中显示，通常是 .NET Standard 或 .NET Core 类库项目；如果要针对非 SDK 样式项目（通常是 .NET Framework），请[迁移项目](../consume-packages/migrate-packages-config-to-package-reference.md)或者改为参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)，以获取分步说明。</span><span class="sxs-lookup"><span data-stu-id="3ee36-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio 项目中的 NuGet 包属性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="3ee36-133">对于面向公共使用而生成的包，请特别注意 **Tags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="3ee36-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="3ee36-134">为包提供一个唯一标识符，并填写任何其他所需的属性。</span><span class="sxs-lookup"><span data-stu-id="3ee36-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="3ee36-135">若要将 MSBuild 属性（SDK 样式项目）映射到 .nuspec 中的属性，请参阅[包目标](../reference/msbuild-targets.md#pack-target)  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="3ee36-136">有关属性的说明，请参阅 [.nuspec 文件引用](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee36-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="3ee36-137">这里的所有属性都列入 Visual Studio 为项目创建的 `.nuspec` 清单。</span><span class="sxs-lookup"><span data-stu-id="3ee36-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="3ee36-138">你必须为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。</span><span class="sxs-lookup"><span data-stu-id="3ee36-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="3ee36-139">对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。</span><span class="sxs-lookup"><span data-stu-id="3ee36-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="3ee36-140">如果你尝试发布名称已存在的包，则会看到一个错误。</span><span class="sxs-lookup"><span data-stu-id="3ee36-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="3ee36-141">（可选）若要直接查看项目文件中的属性，请右键单击“解决方案资源管理器”中的“项目”，然后选择“编辑 AppLogger.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="3ee36-142">此选项从 Visual Studio 2017 开始仅对使用 SDK 样式属性的项目可用。</span><span class="sxs-lookup"><span data-stu-id="3ee36-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="3ee36-143">否则，右键单击项目，并选择“卸载项目”  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="3ee36-144">然后右键单击卸载的项目并选择“编辑 AppLogger.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="3ee36-145">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="3ee36-145">Run the pack command</span></span>

1. <span data-ttu-id="3ee36-146">将此配置设置为“发布”  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="3ee36-147">请在“解决方案资源管理器”中右键单击该项目，然后选择“Pack”命令：  </span><span class="sxs-lookup"><span data-stu-id="3ee36-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 项目上下文菜单上的 NuGet pack 命令](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="3ee36-149">如果没有看到“Pack”  命令，那么项目可能不是 SDK 样式的项目，需要使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="3ee36-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="3ee36-150">[迁移项目](../consume-packages/migrate-packages-config-to-package-reference.md)并使用 `dotnet` CLI，或者改为参阅[创建和发布 .NET Framework 包](create-and-publish-a-package-using-visual-studio-net-framework.md)，以获取分步说明。</span><span class="sxs-lookup"><span data-stu-id="3ee36-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="3ee36-151">Visual Studio 构建项目并创建 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="3ee36-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="3ee36-152">检查“输出”  窗口以查看详细信息（类似于以下内容），其中包含包文件的路径。</span><span class="sxs-lookup"><span data-stu-id="3ee36-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="3ee36-153">另请注意，生成的程序集位于适合 .NET Standard 2.0 目标的 `bin\Release\netstandard2.0` 中。</span><span class="sxs-lookup"><span data-stu-id="3ee36-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="3ee36-154">（可选）在生成期间生成包</span><span class="sxs-lookup"><span data-stu-id="3ee36-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="3ee36-155">可以将 Visual Studio 配置为在生成项目时自动生成 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="3ee36-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="3ee36-156">在“解决方案资源管理器”中，右键单击项目，然后选择“属性”  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="3ee36-157">在“包”选项卡中，选择“在生成期间生成 NuGet 包”   。</span><span class="sxs-lookup"><span data-stu-id="3ee36-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![在生成期间自动生成包](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="3ee36-159">自动生成包时，打包时间会增加项目的生成时间。</span><span class="sxs-lookup"><span data-stu-id="3ee36-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="3ee36-160">（可选）使用 MSBuild 打包</span><span class="sxs-lookup"><span data-stu-id="3ee36-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="3ee36-161">作为使用“打包”菜单命令的备选项，当项目包含必要的包数据时，NuGet 4.x+ 和 MSBuild 15.1+ 支持 `pack` 目标  。</span><span class="sxs-lookup"><span data-stu-id="3ee36-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="3ee36-162">打开命令提示符，导航到项目文件夹并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="3ee36-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="3ee36-163">（用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置。）</span><span class="sxs-lookup"><span data-stu-id="3ee36-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="3ee36-164">有关详细信息，请参阅[使用 MSBuild 创建包](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee36-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="3ee36-165">发布包</span><span class="sxs-lookup"><span data-stu-id="3ee36-165">Publish the package</span></span>

<span data-ttu-id="3ee36-166">有了 `.nupkg` 文件后，可以使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="3ee36-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="3ee36-167">获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="3ee36-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="3ee36-168">使用 dotnet CLI 或 nuget.exe CLI 发布</span><span class="sxs-lookup"><span data-stu-id="3ee36-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="3ee36-169">选择 CLI 工具（.NET Core CLI  (dotnet CLI) 或 NuGet  (nuget.exe CLI)）对应的选项卡。</span><span class="sxs-lookup"><span data-stu-id="3ee36-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="3ee36-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="3ee36-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="3ee36-171">此步骤是使用 `nuget.exe` 的推荐替代方法。</span><span class="sxs-lookup"><span data-stu-id="3ee36-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="3ee36-172">在发布包之前，必须先打开命令行。</span><span class="sxs-lookup"><span data-stu-id="3ee36-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="3ee36-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="3ee36-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="3ee36-174">该步骤是使用 `dotnet.exe` 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="3ee36-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="3ee36-175">打开命令行并更改到包含 `.nupkg` 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ee36-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="3ee36-176">运行以下命令，指定包名称（唯一包 ID）并使用你的 API 密钥替换密钥值：</span><span class="sxs-lookup"><span data-stu-id="3ee36-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="3ee36-177">nuget.exe 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="3ee36-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="3ee36-178">请参阅 [nuget push](../reference/cli-reference/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="3ee36-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="3ee36-179">发布错误</span><span class="sxs-lookup"><span data-stu-id="3ee36-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="3ee36-180">管理已发布的包</span><span class="sxs-lookup"><span data-stu-id="3ee36-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="3ee36-181">添加自述文件和其他文件</span><span class="sxs-lookup"><span data-stu-id="3ee36-181">Adding a readme and other files</span></span>

<span data-ttu-id="3ee36-182">若要直接指定要包含在包中的文件，请编辑项目文件并使用 `content` 属性：</span><span class="sxs-lookup"><span data-stu-id="3ee36-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="3ee36-183">这将在包根目录中包含一个名为 `readme.txt` 的文件。</span><span class="sxs-lookup"><span data-stu-id="3ee36-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="3ee36-184">Visual Studio 在直接安装包之后立即将该文件的内容显示为纯文本。</span><span class="sxs-lookup"><span data-stu-id="3ee36-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="3ee36-185">（对于安装为依赖项的包，不会显示自述文件）。</span><span class="sxs-lookup"><span data-stu-id="3ee36-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="3ee36-186">例如，下面是 HtmlAgilityPack 包的自述文件的显示方式：</span><span class="sxs-lookup"><span data-stu-id="3ee36-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安装时 NuGet 包的自述文件的显示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="3ee36-188">只在项目根目录添加 readme.txt 不会导致它被包含在生成的包中。</span><span class="sxs-lookup"><span data-stu-id="3ee36-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="3ee36-189">相关视频</span><span class="sxs-lookup"><span data-stu-id="3ee36-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="3ee36-190">在[第 9 频道](https://channel9.msdn.com/Series/NuGet-101)和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) 上查找更多 NuGet 视频。</span><span class="sxs-lookup"><span data-stu-id="3ee36-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="3ee36-191">相关主题</span><span class="sxs-lookup"><span data-stu-id="3ee36-191">Related topics</span></span>

- [<span data-ttu-id="3ee36-192">创建包</span><span class="sxs-lookup"><span data-stu-id="3ee36-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="3ee36-193">发布包</span><span class="sxs-lookup"><span data-stu-id="3ee36-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="3ee36-194">预发行包</span><span class="sxs-lookup"><span data-stu-id="3ee36-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="3ee36-195">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="3ee36-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="3ee36-196">包版本控制</span><span class="sxs-lookup"><span data-stu-id="3ee36-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="3ee36-197">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="3ee36-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="3ee36-198">.NET Standard 库文档</span><span class="sxs-lookup"><span data-stu-id="3ee36-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="3ee36-199">从 .NET Framework 移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="3ee36-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
