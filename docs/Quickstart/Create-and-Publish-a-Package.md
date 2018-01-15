---
title: "创建和发布 NuGet 包的介绍性指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "使用 nuget.exe 命令行接口和 Visual Studio 创建和发布 NuGet 包的演练教程。"
keywords: "NuGet 包创建, NuGet 包发布, NuGet 教程"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ab5235537d869047075b93f9d8255ae9e61dfedd
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="34d00-104">创建和发布包</span><span class="sxs-lookup"><span data-stu-id="34d00-104">Create and publish a package</span></span>

<span data-ttu-id="34d00-105">从 .NET 类库创建 NuGet 包并将其发布到 nuget.org 是很简单的过程。以下步骤将逐步介绍使用 NuGet 命令行接口 (CLI) 和 Visual Studio 的过程：</span><span class="sxs-lookup"><span data-stu-id="34d00-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="34d00-106">先决条件</span><span class="sxs-lookup"><span data-stu-id="34d00-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="34d00-107">创建 .nuspec 包清单文件</span><span class="sxs-lookup"><span data-stu-id="34d00-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="34d00-108">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="34d00-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="34d00-109">发布包</span><span class="sxs-lookup"><span data-stu-id="34d00-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="34d00-110">先决条件</span><span class="sxs-lookup"><span data-stu-id="34d00-110">Pre-requisites</span></span>

1. <span data-ttu-id="34d00-111">从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="34d00-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="34d00-112">安装 NuGet CLI 工具，`nuget.exe`，方法是从 [nuget.org/downloads](https://nuget.org/downloads) 下载最新版本的 `nuget.exe` 并将 `.exe` 保存到你的路径中的位置。</span><span class="sxs-lookup"><span data-stu-id="34d00-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="34d00-113">请注意，下载是工具本身，而不是安装程序。</span><span class="sxs-lookup"><span data-stu-id="34d00-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="34d00-114">为要打包的代码创建合适的 .NET 类库项目。</span><span class="sxs-lookup"><span data-stu-id="34d00-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="34d00-115">如果还没有项目，可按如下所示创建一个简单的项目：</span><span class="sxs-lookup"><span data-stu-id="34d00-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="34d00-116">在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C# > Windows”节点，选择“类库”模板，将项目命名为“AppLogger”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="34d00-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="34d00-117">右键单击生成的项目文件并选择“生成”，确保已正确创建项目。</span><span class="sxs-lookup"><span data-stu-id="34d00-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="34d00-118">DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。</span><span class="sxs-lookup"><span data-stu-id="34d00-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="34d00-119">当然，在实际的 NuGet 包中，可实现许多有用的功能，其他人可基于这些功能生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="34d00-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="34d00-120">但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。</span><span class="sxs-lookup"><span data-stu-id="34d00-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="34d00-121">创建 .nuspec 程序包清单文件</span><span class="sxs-lookup"><span data-stu-id="34d00-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="34d00-122">每个 NuGet 包都需要清单 &mdash; 一种 `.nuspec` 文件 &mdash; 以描述其内容和依赖项。</span><span class="sxs-lookup"><span data-stu-id="34d00-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="34d00-123">`nuget spec` 命令会创建此文件，然后你可对其进行自定义。</span><span class="sxs-lookup"><span data-stu-id="34d00-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="34d00-124">在此示例中，将从项目文件创建 `.nuspec`；还可以通过[创建包](../create-packages/creating-a-package.md)中所述的其他方式创建清单。</span><span class="sxs-lookup"><span data-stu-id="34d00-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="34d00-125">打开命令提示符并导航到包含项目文件的文件夹 (`.csproj`)。</span><span class="sxs-lookup"><span data-stu-id="34d00-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="34d00-126">运行 NuGet CLI `spec` 命令生成清单，清单以项目命名，如 `AppLogger.nuspec`：</span><span class="sxs-lookup"><span data-stu-id="34d00-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="34d00-127">在文本编辑器中打开文件。</span><span class="sxs-lookup"><span data-stu-id="34d00-127">Open the file in a text editor.</span></span> <span data-ttu-id="34d00-128">清单看起来类似于下面的代码，其中 `<token>` 形式的令牌（例如，`$id$`）在打包过程中被替换为项目的 Properties/AssemblyInfo.cs 文件中的值。</span><span class="sxs-lookup"><span data-stu-id="34d00-128">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="34d00-129">有关令牌的更多详细信息，请参阅[创建 .nuspec 文件](../create-packages/creating-a-package.md#creating-the-nuspec-file)。</span><span class="sxs-lookup"><span data-stu-id="34d00-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="34d00-130">选择在 nuget.org 上唯一的包 ID。我们建议使用[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定。</span><span class="sxs-lookup"><span data-stu-id="34d00-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="34d00-131">务必更新作者和说明标记，否则下一步会出现错误。</span><span class="sxs-lookup"><span data-stu-id="34d00-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="34d00-132">以下是已更新 `.nuspec` 文件的示例：</span><span class="sxs-lookup"><span data-stu-id="34d00-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="34d00-133">对于供公共使用而生成的包，请特别注意 `<tags>` 元素，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="34d00-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="34d00-134">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="34d00-134">Run the pack command</span></span>

<span data-ttu-id="34d00-135">若要从项目中生成 NuGet 包（一个 `.nupkg` 文件），请运行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="34d00-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="34d00-136">此命令使用 `.nuspec` 文件的包名称和版本号创建 `AppLogger.1.0.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="34d00-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="34d00-137">如果尚未更新 `.nuspec` 文件的各个字段的默认值，该命令会发出警告。</span><span class="sxs-lookup"><span data-stu-id="34d00-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="34d00-138">发布包</span><span class="sxs-lookup"><span data-stu-id="34d00-138">Publish the package</span></span>

<span data-ttu-id="34d00-139">拥有 `.nupkg` 文件后，使用 `push` 命令将其发布到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="34d00-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="34d00-140">（或者，可以使用 [nuget.org 发布工作流](../create-packages/publish-a-package.md#publish-to-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="34d00-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="34d00-141">发布到 nuget.org 的包对其他开发人员公开可见。</span><span class="sxs-lookup"><span data-stu-id="34d00-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="34d00-142">若要专门托管包，请参阅[托管包](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="34d00-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="34d00-143">在 [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) 上创建免费帐户，如果已有帐户，请登录。</span><span class="sxs-lookup"><span data-stu-id="34d00-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="34d00-144">创建新帐户会发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="34d00-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="34d00-145">必须先确认该帐户，才能上传包。</span><span class="sxs-lookup"><span data-stu-id="34d00-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="34d00-146">登录后，选择用户名（在右上角），然后选择“API 密钥”。</span><span class="sxs-lookup"><span data-stu-id="34d00-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="34d00-147">选择“创建”，提供密钥的名称，在“API 密钥”下，选择“作用域”>“推送”，为“Glob 模式”输入“\*”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="34d00-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="34d00-148">创建密钥后，选择“复制”，检索需要在 CLI 中使用的访问密钥：</span><span class="sxs-lookup"><span data-stu-id="34d00-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![将 API 密钥复制到剪贴板](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="34d00-150">将密钥保存在安全位置，并保密。</span><span class="sxs-lookup"><span data-stu-id="34d00-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="34d00-151">如果密钥意外泄露，可随时重新生成密钥。</span><span class="sxs-lookup"><span data-stu-id="34d00-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="34d00-152">如果不再希望通过 CLI 推送包，还可以删除 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="34d00-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="34d00-153">在命令提示符处，运行以下命令，指定包名称并使用步骤 4 中复制的值替换密钥：</span><span class="sxs-lookup"><span data-stu-id="34d00-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="34d00-154">nuget.exe 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="34d00-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="34d00-155">从 nuget.org 上的配置文件中，选择“管理包”，查看刚刚发布的包。</span><span class="sxs-lookup"><span data-stu-id="34d00-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="34d00-156">同样也会收到确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="34d00-156">You also receive a confirmation email.</span></span> <span data-ttu-id="34d00-157">请注意，包可能需要一些时间才能编入索引并显示在可供他人查看的搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="34d00-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="34d00-158">在该时间段，包页面会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="34d00-158">During that time your package page shows the message below:</span></span>

    ![此包未编制索引。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="34d00-161">**病毒扫描**：所有上传到 nuget.org 的包都会进行病毒扫描，如果发现任何病毒，将拒绝包。</span><span class="sxs-lookup"><span data-stu-id="34d00-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="34d00-162">此外，还会定期扫描 nuget.org 上列出的所有包。</span><span class="sxs-lookup"><span data-stu-id="34d00-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="34d00-163">就是这么简单！</span><span class="sxs-lookup"><span data-stu-id="34d00-163">And that's it!</span></span> <span data-ttu-id="34d00-164">刚刚已将第一个 NuGet 包发布到 [nuget.org](https://www.nuget.org/)，其他开发人员可在自己的项目中使用它。</span><span class="sxs-lookup"><span data-stu-id="34d00-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="34d00-165">相关主题</span><span class="sxs-lookup"><span data-stu-id="34d00-165">Related topics</span></span>

- [<span data-ttu-id="34d00-166">创建包</span><span class="sxs-lookup"><span data-stu-id="34d00-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="34d00-167">发布包</span><span class="sxs-lookup"><span data-stu-id="34d00-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="34d00-168">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="34d00-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="34d00-169">包版本控制</span><span class="sxs-lookup"><span data-stu-id="34d00-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="34d00-170">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="34d00-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
