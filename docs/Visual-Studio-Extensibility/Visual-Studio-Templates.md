---
title: "Visual Studio 模板中的 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "在 Visual Studio 项目和项模板中添加 NuGet 包的说明。"
keywords: "Visual Studio 中的 NuGet, Visual Studio 项目模板, Visual Studio 项模板, 项目模板中的包, 项模板中的包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="e6d42-104">Visual Studio 模板中的包</span><span class="sxs-lookup"><span data-stu-id="e6d42-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="e6d42-105">创建项目或项时，Visual Studio 项目和项模板通常需要确保已安装某些包。</span><span class="sxs-lookup"><span data-stu-id="e6d42-105">Visual Studio project and item templates often need to ensure that certain packages are installed into when the project or item is created.</span></span> <span data-ttu-id="e6d42-106">例如，ASP.NET MVC 3 模板安装 jQuery、Modernizr 和其他包。</span><span class="sxs-lookup"><span data-stu-id="e6d42-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="e6d42-107">若要支持此功能，模板作者可指示 NuGet 安装必需的包，而不是单独的库。</span><span class="sxs-lookup"><span data-stu-id="e6d42-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="e6d42-108">此后，开发人员可随时轻松更新这些包。</span><span class="sxs-lookup"><span data-stu-id="e6d42-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="e6d42-109">若要了解有关创作模板本身的详细信息，请参阅[在 Visual Studio 中创建项目和项模板](https://msdn.microsoft.com/library/s365byhx.aspx)或[使用 Visual Studio SDK 创建自定义项目和项模板](https://msdn.microsoft.com/library/ff527340.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e6d42-109">To learn more about authoring templates themselves, refer to [Creating Project and Item Templates in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) or [Creating Custom Project and Item Templates with the Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span></span>

<span data-ttu-id="e6d42-110">本节其余部分介绍创作模板以正确添加 NuGet 包时应采取的具体步骤。</span><span class="sxs-lookup"><span data-stu-id="e6d42-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="e6d42-111">将包添加到模板</span><span class="sxs-lookup"><span data-stu-id="e6d42-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="e6d42-112">最佳做法</span><span class="sxs-lookup"><span data-stu-id="e6d42-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="e6d42-113">有关示例，请参阅 [NuGetInVsTemplates 示例](https://bitbucket.org/marcind/nugetinvstemplates)。</span><span class="sxs-lookup"><span data-stu-id="e6d42-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>


## <a name="adding-packages-to-a-template"></a><span data-ttu-id="e6d42-114">将包添加到模板</span><span class="sxs-lookup"><span data-stu-id="e6d42-114">Adding packages to a template</span></span>

<span data-ttu-id="e6d42-115">实例化模板后，会调用[模板向导](https://msdn.microsoft.com/library/ms185301.aspx)加载要安装的包列表以及有关在何处查找这些包的信息。</span><span class="sxs-lookup"><span data-stu-id="e6d42-115">When a template is instantiated, a [template wizard](https://msdn.microsoft.com/library/ms185301.aspx) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="e6d42-116">包可嵌入 VSIX，嵌入模板，或者位于本地硬盘上（在这种情况下，请使用注册表项引用文件路径）。</span><span class="sxs-lookup"><span data-stu-id="e6d42-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="e6d42-117">本节稍后将提供这些位置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e6d42-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="e6d42-118">预安装的包使用[模板向导](http://msdn.microsoft.com/library/ms185301.aspx)工作。</span><span class="sxs-lookup"><span data-stu-id="e6d42-118">Preinstalled packages work using [template wizards](http://msdn.microsoft.com/library/ms185301.aspx).</span></span> <span data-ttu-id="e6d42-119">模板实例化后会调用特殊向导。</span><span class="sxs-lookup"><span data-stu-id="e6d42-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="e6d42-120">该向导会加载需要安装的包列表，并将该信息传递到相应的 NuGet API。</span><span class="sxs-lookup"><span data-stu-id="e6d42-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="e6d42-121">将包添加到模板的步骤：</span><span class="sxs-lookup"><span data-stu-id="e6d42-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="e6d42-122">在 `vstemplate` 文件中，通过添加 [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) 元素向 NuGet 模板向导添加引用：</span><span class="sxs-lookup"><span data-stu-id="e6d42-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="e6d42-123">`NuGet.VisualStudio.Interop.dll` 为仅包含 `TemplateWizard` 类的程序集，该类是调用 `NuGet.VisualStudio.dll` 中实际实现的简单包装器。</span><span class="sxs-lookup"><span data-stu-id="e6d42-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="e6d42-124">程序集版本永远不会更改，因此项目/项模板可继续用于新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="e6d42-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="e6d42-125">在项目中添加要安装的包列表：</span><span class="sxs-lookup"><span data-stu-id="e6d42-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="e6d42-126">(NuGet 2.2.1+) 该向导支持多个 `<package>` 元素，从而支持多个包源。</span><span class="sxs-lookup"><span data-stu-id="e6d42-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="e6d42-127">`id` 和 `version` 属性都是必需的，这意味着即使可使用较新版本，仍将安装包的特定版本。</span><span class="sxs-lookup"><span data-stu-id="e6d42-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="e6d42-128">这可以防止包更新中断模板，并将是否更新包的选择权留给使用模板的开发人员。</span><span class="sxs-lookup"><span data-stu-id="e6d42-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>


1. <span data-ttu-id="e6d42-129">指定 NuGet 可找到包的存储库，如以下各节中所述。</span><span class="sxs-lookup"><span data-stu-id="e6d42-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="e6d42-130">VSIX 包存储库</span><span class="sxs-lookup"><span data-stu-id="e6d42-130">VSIX package repository</span></span>

<span data-ttu-id="e6d42-131">建议用于 Visual Studio 项目/项模板的部署方法是 [VSIX 扩展](http://msdn.microsoft.com/library/ff363239.aspx)，因为借助它，可将多个项目/项模板打包在一起，而且开发人员可使用 VS 扩展管理器或 Visual Studio 库轻松发现模板。</span><span class="sxs-lookup"><span data-stu-id="e6d42-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](http://msdn.microsoft.com/library/ff363239.aspx) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="e6d42-132">也可使用 [Visual Studio 扩展管理器自动更新机制](http://msdn.microsoft.com/library/dd997169.aspx)轻松部署扩展更新。</span><span class="sxs-lookup"><span data-stu-id="e6d42-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](http://msdn.microsoft.com/library/dd997169.aspx).</span></span>

<span data-ttu-id="e6d42-133">VSIX 本身可用作模板所需包的源：</span><span class="sxs-lookup"><span data-stu-id="e6d42-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="e6d42-134">修改 `.vstemplate` 文件中的 `<packages>` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e6d42-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="e6d42-135">`repository` 属性将存储库类型指定为 `extension`，而 `repositoryId` 是 VSIX 本身的唯一标识符（此值为扩展的 `vsixmanifest` 文件中的 [`ID` 属性](http://msdn.microsoft.com/library/dd393688.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="e6d42-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the [`ID` attribute](http://msdn.microsoft.com/library/dd393688.aspx) in the extension’s `vsixmanifest` file).</span></span>

1. <span data-ttu-id="e6d42-136">将 `nupkg` 文件放置于 VSIX 中名为 `Packages` 的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e6d42-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>
1. <span data-ttu-id="e6d42-137">在 `source.extension.vsixmanifest` 文件中添加必要的包文件作为[自定义扩展内容](http://msdn.microsoft.com/library/dd393737.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e6d42-137">Add the necessary package files as [custom extension content](http://msdn.microsoft.com/library/dd393737.aspx) in your `source.extension.vsixmanifest` file.</span></span> <span data-ttu-id="e6d42-138">如果使用的是 2.0 架构，应显示如下：</span><span class="sxs-lookup"><span data-stu-id="e6d42-138">If you're using the 2.0 schema it should look like this:</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    <span data-ttu-id="e6d42-139">如果使用的是 1.0 架构，应显示如下：</span><span class="sxs-lookup"><span data-stu-id="e6d42-139">If you're using the 1.0 schema it should look like this:</span></span>

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. <span data-ttu-id="e6d42-140">请注意，可在项目模板所在的同一 VSIX 中提供包，或者可将其放置在单独的 VSIX 中（如果这样对于你的方案更合理）。</span><span class="sxs-lookup"><span data-stu-id="e6d42-140">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="e6d42-141">但是，请不要引用任何你无法控制的 VSIX，因为对该扩展进行更改可能会中断模板。</span><span class="sxs-lookup"><span data-stu-id="e6d42-141">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>


### <a name="template-package-repository"></a><span data-ttu-id="e6d42-142">模板包存储库</span><span class="sxs-lookup"><span data-stu-id="e6d42-142">Template package repository</span></span>

<span data-ttu-id="e6d42-143">如果仅分发一个项目/项模板且无需将多个模板打包在一起，则可使用更为简单但受限更多的方法，该方法直接在项目/项模板 ZIP 文件中添加包：</span><span class="sxs-lookup"><span data-stu-id="e6d42-143">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="e6d42-144">修改 `.vstemplate` 文件中的 `<packages>` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e6d42-144">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="e6d42-145">`repository` 属性具有值 `template`，不需要 `repositoryId` 属性。</span><span class="sxs-lookup"><span data-stu-id="e6d42-145">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="e6d42-146">将包放置在项目/项模板 ZIP 文件的根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e6d42-146">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="e6d42-147">请注意，如果一个或多个包对模板通用，则在包含多个模板的 VSIX 中使用此方法会导致不必要的膨胀。</span><span class="sxs-lookup"><span data-stu-id="e6d42-147">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="e6d42-148">在这种情况下，请将 [VSIX 用作存储库](#vsix-package-repository)，如上一节中所述。</span><span class="sxs-lookup"><span data-stu-id="e6d42-148">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>


### <a name="registry-specified-folder-path"></a><span data-ttu-id="e6d42-149">注册表指定的文件夹路径</span><span class="sxs-lookup"><span data-stu-id="e6d42-149">Registry-specified folder path</span></span>

<span data-ttu-id="e6d42-150">使用 MSI 安装的 SDK 可直接在开发人员计算机上安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e6d42-150">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="e6d42-151">这使其在使用项目或项模板时立即可用，而不必在此期间进行提取。</span><span class="sxs-lookup"><span data-stu-id="e6d42-151">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="e6d42-152">ASP.NET 模板使用此方法。</span><span class="sxs-lookup"><span data-stu-id="e6d42-152">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="e6d42-153">利用 MSI 将包安装到计算机。</span><span class="sxs-lookup"><span data-stu-id="e6d42-153">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="e6d42-154">可仅安装 `.nupkg` 文件，也可将其与扩展内容一起安装，这可在使用模板时减少额外的步骤。</span><span class="sxs-lookup"><span data-stu-id="e6d42-154">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="e6d42-155">在这种情况下，请遵循 NuGet 的标准文件夹结构，其中 `.nupkg` 文件位于根文件夹中，然后每个包都有子文件夹，子文件夹使用 id/版本对作为名称。</span><span class="sxs-lookup"><span data-stu-id="e6d42-155">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="e6d42-156">写入注册表项以标识包位置：</span><span class="sxs-lookup"><span data-stu-id="e6d42-156">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="e6d42-157">项位置：如果是计算机范围内的 `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`，或为每个用户安装的模板和包，则使用 `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="e6d42-157">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="e6d42-158">项名称：使用唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="e6d42-158">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="e6d42-159">例如，适用于 VS 2012 的 ASP.NET MVC 4 模板使用 `AspNetMvc4VS11`。</span><span class="sxs-lookup"><span data-stu-id="e6d42-159">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="e6d42-160">值：包文件夹的完整路径。</span><span class="sxs-lookup"><span data-stu-id="e6d42-160">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="e6d42-161">在 `.vstemplate` 文件的 `<packages>` 元素中，添加属性 `repository="registry"` 并在 `keyName` 属性中指定注册表项名称。</span><span class="sxs-lookup"><span data-stu-id="e6d42-161">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="e6d42-162">如果已预先解压缩包，请使用 `isPreunzipped="true"` 属性。</span><span class="sxs-lookup"><span data-stu-id="e6d42-162">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="e6d42-163">(NuGet 3.2 +) 如果希望在包安装结束时强制执行设计时生成，请添加 `forceDesignTimeBuild="true"` 属性。</span><span class="sxs-lookup"><span data-stu-id="e6d42-163">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="e6d42-164">作为优化，添加 `skipAssemblyReferences="true"`，因为模板本身已包括必要的引用。</span><span class="sxs-lookup"><span data-stu-id="e6d42-164">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="e6d42-165">最佳做法</span><span class="sxs-lookup"><span data-stu-id="e6d42-165">Best Practices</span></span>

1. <span data-ttu-id="e6d42-166">通过在 VSIX 清单中添加对其的引用，声明 NuGet VSIX 上的依赖项：</span><span class="sxs-lookup"><span data-stu-id="e6d42-166">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="e6d42-167">通过在 `.vstemplate` 文件中设置 [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx)，要求在创建时保存项目/项模板。</span><span class="sxs-lookup"><span data-stu-id="e6d42-167">Require project/item templates to be saved on creation by setting [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="e6d42-168">模板不包括 `packages.config` 或 `project.json` 文件，也不包括安装 NuGet 包时将添加的任何引用或内容。</span><span class="sxs-lookup"><span data-stu-id="e6d42-168">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
