---
title: 包创作最佳做法
description: 创建高质量 NuGet 包的最佳做法的一般指南。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 35eb000bddaa58726857cd3c1fd2362917f83196
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "99420763"
---
# <a name="package-authoring-best-practices"></a><span data-ttu-id="a54b1-103">包创作最佳做法</span><span class="sxs-lookup"><span data-stu-id="a54b1-103">Package authoring best practices</span></span>

<span data-ttu-id="a54b1-104">本指南旨在为 NuGet 包作者创建和发布高质量包提供轻型参考。</span><span class="sxs-lookup"><span data-stu-id="a54b1-104">This guidance is intended to give NuGet package authors a lightweight reference to create and publish high-quality packages.</span></span> <span data-ttu-id="a54b1-105">它主要重点介绍特定于包的最佳做法，如元数据和打包。</span><span class="sxs-lookup"><span data-stu-id="a54b1-105">It will primarily focus on package-specific best practices such as metadata and packing.</span></span> <span data-ttu-id="a54b1-106">有关生成高质量库的更深入的建议，请参阅 .NET [开放源代码库指南](https://docs.microsoft.com/dotnet/standard/library-guidance/)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-106">For more in-depth suggestions for building high quality libraries, see the .NET [Open-source library guidance](https://docs.microsoft.com/dotnet/standard/library-guidance/).</span></span>

## <a name="types-of-recommendations"></a><span data-ttu-id="a54b1-107">建议类型</span><span class="sxs-lookup"><span data-stu-id="a54b1-107">Types of recommendations</span></span>

<span data-ttu-id="a54b1-108">每篇文章介绍四种类型的建议：“请执行”、“请考虑”、、“请避免”、和“请勿”。</span><span class="sxs-lookup"><span data-stu-id="a54b1-108">Each article presents four types of recommendations: **Do**, **Consider**, **Avoid**, and **Do not**.</span></span> <span data-ttu-id="a54b1-109">建议类型表示了应遵循的程度。</span><span class="sxs-lookup"><span data-stu-id="a54b1-109">The type of recommendation indicates how closely it should be followed.</span></span>

<span data-ttu-id="a54b1-110">应始终遵循“请执行”建议。</span><span class="sxs-lookup"><span data-stu-id="a54b1-110">You should almost always follow a **Do** recommendation.</span></span> <span data-ttu-id="a54b1-111">例如：</span><span class="sxs-lookup"><span data-stu-id="a54b1-111">For example:</span></span>

<span data-ttu-id="a54b1-112">✔️ 请包含描述其用途的包的简短说明。</span><span class="sxs-lookup"><span data-stu-id="a54b1-112">✔️ DO include a short description for your package that describes what it's for.</span></span>

<span data-ttu-id="a54b1-113">在另一方面，“请考虑”建议是在一般情况下要遵循的建议，但存在该规则的合法例外：</span><span class="sxs-lookup"><span data-stu-id="a54b1-113">On the other hand, **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule:</span></span>

<span data-ttu-id="a54b1-114">✔️ 请考虑选择带有满足 NuGet 前缀预留[条件](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)的前缀的 NuGet 包名称。</span><span class="sxs-lookup"><span data-stu-id="a54b1-114">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's prefix reservation [criteria](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="a54b1-115">“请避免”建议是指在一般情况下不应执行的操作，但有时也可以打破规则：</span><span class="sxs-lookup"><span data-stu-id="a54b1-115">**Avoid** recommendations mention things that are generally not a good idea, but breaking the rule sometimes makes sense:</span></span>

<span data-ttu-id="a54b1-116">❌ 请避免使用需要确切版本的 NuGet 包引用。</span><span class="sxs-lookup"><span data-stu-id="a54b1-116">❌ AVOID NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="a54b1-117">最后，“请勿”建议是指在大多数情况下不得执行的操作：</span><span class="sxs-lookup"><span data-stu-id="a54b1-117">And finally, **Do not** recommendations indicate something you should almost never do:</span></span>

<span data-ttu-id="a54b1-118">❌ 请勿使用 `LicenseUrl` 元数据属性。</span><span class="sxs-lookup"><span data-stu-id="a54b1-118">❌ DO NOT use the `LicenseUrl` metadata property.</span></span>

## <a name="create-a-nuget-package"></a><span data-ttu-id="a54b1-119">创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a54b1-119">Create a NuGet package</span></span>

<span data-ttu-id="a54b1-120">创建 NuGet 包的最新建议方法是通过 [SDK 样式的项目](https://docs.microsoft.com/nuget/resources/check-project-format)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-120">The latest recommended way to to create a NuGet package is from an [SDK-style project](https://docs.microsoft.com/nuget/resources/check-project-format).</span></span> <span data-ttu-id="a54b1-121">SDK 样式的项目属性（包括[目标框架](https://docs.microsoft.com/dotnet/standard/frameworks)和[包元数据](#package-metadata)）是在[项目文件](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)中定义的。</span><span class="sxs-lookup"><span data-stu-id="a54b1-121">SDK-style project properties, including [target framework](https://docs.microsoft.com/dotnet/standard/frameworks) and [package metadata](#package-metadata), are defined in the [project file](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).</span></span>

<span data-ttu-id="a54b1-122">通过在 [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) 或 [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli) 中定义所需的属性和打包，从 SDK 样式的项目创建包。</span><span class="sxs-lookup"><span data-stu-id="a54b1-122">Create a package from your SDK-style project by defining the required properties and packing in [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) or the [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).</span></span>

<span data-ttu-id="a54b1-123">✔️ 创建 SDK 样式的项目，并使用 Visual Studio 或 dotnet CLI 创建（打包）包。</span><span class="sxs-lookup"><span data-stu-id="a54b1-123">✔️ DO create an SDK-style project and create (pack) your package using Visual Studio or the dotnet CLI.</span></span>

<span data-ttu-id="a54b1-124">有关包创建的更详细指南，包括必要的客户端工具、项目文件示例和命令，请参阅[使用 dotnet CLI 创建 NuGet 包](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-124">For more detailed guidance regarding package creation including necessary client tools, project file example, and commands, see [Create a NuGet package using the dotnet CLI](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).</span></span>

<span data-ttu-id="a54b1-125">若要帮助决定要面向的 .NET 框架，请参阅我们的[跨平台目标的最新指南](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-125">To help decide which .NET frameworks to target, see our [latest guidance for cross-platform targeting](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).</span></span>

## <a name="package-metadata"></a><span data-ttu-id="a54b1-126">包元数据</span><span class="sxs-lookup"><span data-stu-id="a54b1-126">Package metadata</span></span>

<span data-ttu-id="a54b1-127">元数据是任何 NuGet 包的基础组件。</span><span class="sxs-lookup"><span data-stu-id="a54b1-127">Metadata is a foundational component of any NuGet package.</span></span> <span data-ttu-id="a54b1-128">你的元数据质量会极大地影响包的可发现性、可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="a54b1-128">The quality of your metadata can vastly influence the discoverability, usability, and trustworthiness of your package.</span></span>

<span data-ttu-id="a54b1-129">在 Visual Studio 中，指定包元数据的建议方法是转到“项目”>“[项目名称] 属性”>“包”。</span><span class="sxs-lookup"><span data-stu-id="a54b1-129">In Visual Studio, the recommended way to specify package metadata is to go Project > [Project Name] Properties > Package.</span></span>

<span data-ttu-id="a54b1-130">还可以[直接在项目文件中指定](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties)包元数据元素。</span><span class="sxs-lookup"><span data-stu-id="a54b1-130">Package metadata elements can also be [specified directly in the project file](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).</span></span>

<span data-ttu-id="a54b1-131">下面是一个表映射，其中描述可用的包元数据元素：</span><span class="sxs-lookup"><span data-stu-id="a54b1-131">Below is a table mapping and describing available package metadata elements:</span></span>

| <span data-ttu-id="a54b1-132">Visual Studio 属性名称</span><span class="sxs-lookup"><span data-stu-id="a54b1-132">Visual Studio property name</span></span>                   | [<span data-ttu-id="a54b1-133">项目文件/MSBuild 属性名称</span><span class="sxs-lookup"><span data-stu-id="a54b1-133">Project file/ MSBuild property name</span></span>](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [<span data-ttu-id="a54b1-134">Nuspec 属性名称</span><span class="sxs-lookup"><span data-stu-id="a54b1-134">Nuspec property name</span></span>](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | <span data-ttu-id="a54b1-135">说明</span><span class="sxs-lookup"><span data-stu-id="a54b1-135">Description</span></span>                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | <span data-ttu-id="a54b1-136">包名称或标识符。</span><span class="sxs-lookup"><span data-stu-id="a54b1-136">The package name or identifier.</span></span>                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | <span data-ttu-id="a54b1-137">NuGet 包版本。</span><span class="sxs-lookup"><span data-stu-id="a54b1-137">NuGet package version.</span></span>                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | <span data-ttu-id="a54b1-138">以逗号分隔的包作者列表，通常使用个人或组织的“友好名称”。</span><span class="sxs-lookup"><span data-stu-id="a54b1-138">A comma-separated list of package authors, often using the individual's or an organization's "pretty name."</span></span>                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | <span data-ttu-id="a54b1-139">对包的描述。</span><span class="sxs-lookup"><span data-stu-id="a54b1-139">A description of the package.</span></span>                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | <span data-ttu-id="a54b1-140">包的版权详细信息。</span><span class="sxs-lookup"><span data-stu-id="a54b1-140">Copyright details for the package.</span></span>                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | <span data-ttu-id="a54b1-141">SPDX 许可证表达式。</span><span class="sxs-lookup"><span data-stu-id="a54b1-141">An SPDX license expression.</span></span>       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | <span data-ttu-id="a54b1-142">自定义许可证文件的路径。</span><span class="sxs-lookup"><span data-stu-id="a54b1-142">Path to a custom license file.</span></span>                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | <span data-ttu-id="a54b1-143">项目主页的 URL。</span><span class="sxs-lookup"><span data-stu-id="a54b1-143">A URL for the project homepage.</span></span>                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | <span data-ttu-id="a54b1-144">包图标图像文件的路径。</span><span class="sxs-lookup"><span data-stu-id="a54b1-144">Path to the package icon image file.</span></span>                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | <span data-ttu-id="a54b1-145">从中生成包的存储库的 URL。</span><span class="sxs-lookup"><span data-stu-id="a54b1-145">URL to the repository from which the package was built.</span></span>                                                           |
| [`Repository type`](#repository-type-and-url) | [`RespositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | <span data-ttu-id="a54b1-146">存储库 URL 指向的存储库的类型（即“git”）。</span><span class="sxs-lookup"><span data-stu-id="a54b1-146">Type of repository the repository URL is pointing to (i.e. "git").</span></span>                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | <span data-ttu-id="a54b1-147">描述包的标记和关键字的空格分隔列表。</span><span class="sxs-lookup"><span data-stu-id="a54b1-147">A space-delimited list of tags and keywords that describe the package.</span></span> <span data-ttu-id="a54b1-148">搜索包时使用标记。</span><span class="sxs-lookup"><span data-stu-id="a54b1-148">Tags are used when searching for packages.</span></span> |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | <span data-ttu-id="a54b1-149">在此版本的包中进行的更改的说明。</span><span class="sxs-lookup"><span data-stu-id="a54b1-149">A description of the changes made in this release of the package.</span></span>                                                 |  |

### <a name="package-id"></a><span data-ttu-id="a54b1-150">包 ID</span><span class="sxs-lookup"><span data-stu-id="a54b1-150">Package ID</span></span>

<span data-ttu-id="a54b1-151">如果你要发布全新的包：</span><span class="sxs-lookup"><span data-stu-id="a54b1-151">If you're publishing a completely new package:</span></span>

<span data-ttu-id="a54b1-152">✔️ 请选择唯一的包 ID，并与 NuGet.org 上的现有包明确区分。</span><span class="sxs-lookup"><span data-stu-id="a54b1-152">✔️ DO choose a package ID that is unique and clearly differentiated from existing packages on NuGet.org.</span></span>
> <span data-ttu-id="a54b1-153">可以通过在 NuGet.org 上搜索 ID 或检查是否存在以下链接来检查包 ID 是否是唯一的和可区分的： https://www.nuget.org/packages/<package 名称\> 。</span><span class="sxs-lookup"><span data-stu-id="a54b1-153">You can check if a package ID is unique and differentiable by searching for the ID on NuGet.org or checking if the following link exists: https://www.nuget.org/packages/<package name\>.</span></span>

<span data-ttu-id="a54b1-154">✔️ 请考虑选择带有满足 NuGet [前缀预留条件](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)的前缀的 NuGet 包名称。</span><span class="sxs-lookup"><span data-stu-id="a54b1-154">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's [prefix reservation criteria](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria).</span></span>
> <span data-ttu-id="a54b1-155">保留包的前缀 ID 将可以获得已验证的复选标记：![图像](media/Verified-check-mark.png)</span><span class="sxs-lookup"><span data-stu-id="a54b1-155">Reserving the prefix ID for your package will let you get the verified check mark: ![image](media/Verified-check-mark.png)</span></span>
> 
> <span data-ttu-id="a54b1-156">若要了解详细信息，请查看[包 ID 前缀预留文档](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-156">Check out the [Package ID prefix reservation docs](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) to learn more.</span></span>

### <a name="package-version"></a><span data-ttu-id="a54b1-157">包版本</span><span class="sxs-lookup"><span data-stu-id="a54b1-157">Package Version</span></span>

<span data-ttu-id="a54b1-158">✔️ 请考虑使用 [SemVer](https://semver.org/) 控制 NuGet 包的版本。</span><span class="sxs-lookup"><span data-stu-id="a54b1-158">✔️ CONSIDER using [SemVer](https://semver.org/) to version your NuGet package.</span></span>
> <span data-ttu-id="a54b1-159">实质上，这意味着使用 Major.Minor.Patch[-prerelease] 格式。</span><span class="sxs-lookup"><span data-stu-id="a54b1-159">Essentially, this means using the Major.Minor.Patch[-prerelease] format.</span></span>

<span data-ttu-id="a54b1-160">✔️ 如果包不稳定或处于预览阶段，则将包作为[预发布包](https://docs.microsoft.com/nuget/create-packages/prerelease-packages)发布。</span><span class="sxs-lookup"><span data-stu-id="a54b1-160">✔️ DO publish a package as a [pre-release package](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) if it is non-stable or a preview.</span></span>

<span data-ttu-id="a54b1-161">请参阅 [.NET 库版本控制指南](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning)了解更多高级指南。</span><span class="sxs-lookup"><span data-stu-id="a54b1-161">See the [.NET library versioning guide](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) for more advanced guidance.</span></span>

### <a name="authors"></a><span data-ttu-id="a54b1-162">Authors</span><span class="sxs-lookup"><span data-stu-id="a54b1-162">Authors</span></span>

<span data-ttu-id="a54b1-163">✔️ 请使用“作者”字段作为你或你的组织的“友好名称”。</span><span class="sxs-lookup"><span data-stu-id="a54b1-163">✔️ DO use the author field for your or your organization's "pretty name."</span></span>
> <span data-ttu-id="a54b1-164">例如，如果我的 NuGet.org 用户名为“jdoe”，则将“Jane Doe”用作“作者”字段可帮助使用者将我识别为作者。</span><span class="sxs-lookup"><span data-stu-id="a54b1-164">For example, if my NuGet.org username is "jdoe" then using "Jane Doe" for the author field may help consumers recognize me as an author.</span></span> <span data-ttu-id="a54b1-165">如果我的组织的 NuGet.org 用户名为“ContosoToolkit”，则使用“Contoso Corporation”可能更具识别性，并激发更多使用者信任。</span><span class="sxs-lookup"><span data-stu-id="a54b1-165">If my organization's NuGet.org username is "ContosoToolkit" then using "Contoso Corporation" may be more recognizable and inspire more consumer trust.</span></span>
### <a name="description"></a><span data-ttu-id="a54b1-166">说明</span><span class="sxs-lookup"><span data-stu-id="a54b1-166">Description</span></span>

<span data-ttu-id="a54b1-167">✔️ 请包括描述包的简短说明（最多 4000 个字符）。</span><span class="sxs-lookup"><span data-stu-id="a54b1-167">✔️ DO include a short description (up to 4000 characters) to describe your package.</span></span>
> <span data-ttu-id="a54b1-168">包说明是 NuGet 搜索中最重要的字段之一，可能是潜在使用者在确定包是否适用时查看的第一个方面。</span><span class="sxs-lookup"><span data-stu-id="a54b1-168">Package descriptions are one of the most prominent fields surfaced in NuGet search and will likely be the first thing potential consumers looks at to determine if a package is right for them.</span></span>

### <a name="copyright"></a><span data-ttu-id="a54b1-169">Copyright</span><span class="sxs-lookup"><span data-stu-id="a54b1-169">Copyright</span></span>

<span data-ttu-id="a54b1-170">✔️ 请考虑对你的包使用版权“Copyright (c) <名称/公司\> <年\>”。</span><span class="sxs-lookup"><span data-stu-id="a54b1-170">✔️ CONSIDER copyrighting your package with "Copyright (c) <name/company\> <year\>."</span></span>
><span data-ttu-id="a54b1-171">版权声明实质上表示：未经你的允许，不可复制你的工作。</span><span class="sxs-lookup"><span data-stu-id="a54b1-171">A copyright notice essentially indicates that your work cannot be copied without your permission.</span></span> <span data-ttu-id="a54b1-172">在包中包含版权声明非常简单，不会造成任何损害！</span><span class="sxs-lookup"><span data-stu-id="a54b1-172">Including a copyright notice in your package is easy and won't do any harm!</span></span>

<span data-ttu-id="a54b1-173">示例：版权所有 (c) Contoso 2020</span><span class="sxs-lookup"><span data-stu-id="a54b1-173">Example: Copyright (c) Contoso 2020</span></span>

### <a name="licensing"></a><span data-ttu-id="a54b1-174">许可</span><span class="sxs-lookup"><span data-stu-id="a54b1-174">Licensing</span></span>

<span data-ttu-id="a54b1-175">✔️ [在包中包含许可证表达式或许可证文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-175">✔️ DO [include a license expression or license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a54b1-176">没有许可证的项目默认为[独家版权](https://choosealicense.com/no-permission/)，这意味着你未授予任何人使用你的项目的权限。</span><span class="sxs-lookup"><span data-stu-id="a54b1-176">A project without a license defaults to [exclusive copyright](https://choosealicense.com/no-permission/), meaning that you have not granted anyone permission to use your project.</span></span>

<span data-ttu-id="a54b1-177">❌ 请勿使用已弃用的 `LicenseUrl` 元数据属性。</span><span class="sxs-lookup"><span data-stu-id="a54b1-177">❌ DO NOT use the deprecated `LicenseUrl` metadata property.</span></span>
> <span data-ttu-id="a54b1-178">这会带来法律歧义，因为 URL 中的许可证更改将以追溯方式更改以前的包版本显示的许可证。</span><span class="sxs-lookup"><span data-stu-id="a54b1-178">This presents legal ambiguity as license changes at the URL will retroactively change the displayed license for previous package versions.</span></span>

#### <a name="if-your-package-is-open-source"></a><span data-ttu-id="a54b1-179">如果你的包是[开放源代码](https://opensource.org/osd)</span><span class="sxs-lookup"><span data-stu-id="a54b1-179">If your package is [open source](https://opensource.org/osd)</span></span>

<span data-ttu-id="a54b1-180">✔️ 请[选择开放源代码许可证](https://choosealicense.com/)，使包开放源代码。</span><span class="sxs-lookup"><span data-stu-id="a54b1-180">✔️ DO [choose an open source license](https://choosealicense.com/) to make your package open source.</span></span>
> <span data-ttu-id="a54b1-181">“开放源代码许可证是符合开放源代码定义的许可证 - 简而言之，它们允许免费使用、修改和共享软件。”</span><span class="sxs-lookup"><span data-stu-id="a54b1-181">*"Open source licenses are licenses that comply with the Open Source Definition — in brief, they allow software to be freely used, modified, and shared."*</span></span> <span data-ttu-id="a54b1-182">- 开放源代码计划。</span><span class="sxs-lookup"><span data-stu-id="a54b1-182">- Open Source Initiative.</span></span> <span data-ttu-id="a54b1-183">若要了解有关开放源代码软件和开放源代码计划的详细信息，请查看 https://opensource.org/ 。</span><span class="sxs-lookup"><span data-stu-id="a54b1-183">To learn more about open source software and the Open Source Initiative, check out https://opensource.org/.</span></span>

<span data-ttu-id="a54b1-184">✔️ 请考虑[在包中包含许可证表达式](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-184">✔️ CONSIDER [including a license expression in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="a54b1-185">如果许可证表达式可以使用你的包，或者如果许可证已更改，则它们会最明显地表现出来并让使用者更清楚地知道。</span><span class="sxs-lookup"><span data-stu-id="a54b1-185">License expressions are surfaced the most clearly and make it more obvious to consumers if they can use your package or if the license has changed.</span></span> 
> [!Note]
> <span data-ttu-id="a54b1-186">NuGet.org 仅接受开放源代码计划或免费软件基金会批准的许可证的许可证表达式。</span><span class="sxs-lookup"><span data-stu-id="a54b1-186">NuGet.org only accepts license expressions for licenses that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

#### <a name="if-your-package-is-not-open-source"></a><span data-ttu-id="a54b1-187">如果你的包未开放源代码</span><span class="sxs-lookup"><span data-stu-id="a54b1-187">If your package is not open source</span></span>

<span data-ttu-id="a54b1-188">✔️ 请[在包中包含许可证文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="a54b1-188">✔️ DO [include a license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="a54b1-189">可以将任何许可证文件（.txt 或 .md）（包括非标准许可证）添加到你的包。</span><span class="sxs-lookup"><span data-stu-id="a54b1-189">Any license file (.txt or .md) can be added to your package, including non-standard licenses.</span></span> 

### <a name="project-url"></a><span data-ttu-id="a54b1-190">项目 URL</span><span class="sxs-lookup"><span data-stu-id="a54b1-190">Project URL</span></span>

<span data-ttu-id="a54b1-191">✔️ 请考虑包括指向关联项目、存储库或公司网站的链接。</span><span class="sxs-lookup"><span data-stu-id="a54b1-191">✔️ CONSIDER including a link to an associated project, repository, or company website.</span></span>
> <span data-ttu-id="a54b1-192">你的项目网站应拥有用户需要了解的有关你的包的一切，并且很可能是用户查找文档的位置。</span><span class="sxs-lookup"><span data-stu-id="a54b1-192">Your project site should have everything users need to know about your package and will likely be where users look for documentation.</span></span>

### <a name="icon"></a><span data-ttu-id="a54b1-193">图标</span><span class="sxs-lookup"><span data-stu-id="a54b1-193">Icon</span></span>

<span data-ttu-id="a54b1-194">✔️ 请考虑[包含包的图标](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)，以帮助在视觉上对其进行区分。</span><span class="sxs-lookup"><span data-stu-id="a54b1-194">✔️ CONSIDER [including an icon with your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) to help visually differentiate it.</span></span> <span data-ttu-id="a54b1-195">它是一个相对较小的添加内容，可以提高对包质量的认知度。</span><span class="sxs-lookup"><span data-stu-id="a54b1-195">It's a relatively small addition that can improve perception of package quality.</span></span>
> <span data-ttu-id="a54b1-196">图标可以特定于单个包，也可以是品牌徽标。</span><span class="sxs-lookup"><span data-stu-id="a54b1-196">Icons can be specific to individual packages or be a brand logo.</span></span>

<span data-ttu-id="a54b1-197">✔️ 请使用属于 128x128 并具有透明背景的图像 (PNG)，以获得最佳查看结果。</span><span class="sxs-lookup"><span data-stu-id="a54b1-197">✔️ DO use an image that is 128x128 and has a transparent background (PNG) for best viewing results.</span></span>
> <span data-ttu-id="a54b1-198">NuGet 会根据显示它的客户端自动缩放图像。</span><span class="sxs-lookup"><span data-stu-id="a54b1-198">NuGet will automatically scale your image to the client it is being displayed on.</span></span>

<span data-ttu-id="a54b1-199">❌ 请勿使用已弃用的 `IconUrl` 元数据属性。</span><span class="sxs-lookup"><span data-stu-id="a54b1-199">❌ DO NOT use the deprecated `IconUrl` metadata property.</span></span>

### <a name="repository-type-and-url"></a><span data-ttu-id="a54b1-200">存储库类型和 URL</span><span class="sxs-lookup"><span data-stu-id="a54b1-200">Repository Type and URL</span></span>

<span data-ttu-id="a54b1-201">✔️考虑设置[源链接](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink)，以自动将源代码管理元数据添加到 NuGet 包，使库更易于调试。</span><span class="sxs-lookup"><span data-stu-id="a54b1-201">✔️ CONSIDER setting up [Source Link](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) to automatically add source control metadata to your NuGet package and make your library easier to debug.</span></span>
> <span data-ttu-id="a54b1-202">源链接会自动将 `Repository URL` 和 `Repository Type` 添加到包元数据中。</span><span class="sxs-lookup"><span data-stu-id="a54b1-202">Source Link automatically adds `Repository URL` and `Repository Type` to the package metadata.</span></span> <span data-ttu-id="a54b1-203">它还添加与包版本关联的特定提交。</span><span class="sxs-lookup"><span data-stu-id="a54b1-203">It also adds the specific commit associated with your package version.</span></span>

### <a name="tags"></a><span data-ttu-id="a54b1-204">标记</span><span class="sxs-lookup"><span data-stu-id="a54b1-204">Tags</span></span>

<span data-ttu-id="a54b1-205">✔️ 请包括多个标记，其中包含与包相关的关键术语，以增强可发现性。</span><span class="sxs-lookup"><span data-stu-id="a54b1-205">✔️ DO include several tags with key terms related to your package to enhance discoverability.</span></span>
> <span data-ttu-id="a54b1-206">在 NuGet. org 的搜索算法中考虑包括标记，这对于不在包 ID 中但相关的术语特别有用。</span><span class="sxs-lookup"><span data-stu-id="a54b1-206">Tags are taken into account in NuGet.org's search algorithm and are especially helpful for terms that are not in the Package ID but are relevant.</span></span>

<span data-ttu-id="a54b1-207">例如，如果我发布了一个包以将字符串记录到控制台中，我将包括：“日志记录、日志、控制台、字符串、输出”</span><span class="sxs-lookup"><span data-stu-id="a54b1-207">For example, if I published a package to log strings to the console, I would include: "logging, log, console, string, output"</span></span>

### <a name="release-notes"></a><span data-ttu-id="a54b1-208">发行说明</span><span class="sxs-lookup"><span data-stu-id="a54b1-208">Release notes</span></span>

<span data-ttu-id="a54b1-209">✔️ 请考虑包括发行说明，其中每个更新说明了所做的更改。</span><span class="sxs-lookup"><span data-stu-id="a54b1-209">✔️ CONSIDER including release notes with each update describing what changes were made.</span></span>
> <span data-ttu-id="a54b1-210">虽然发行说明不需要特定的格式，但建议包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="a54b1-210">While there is no specific format required for release notes, we recommend including:</span></span>
>
> 1. <span data-ttu-id="a54b1-211">中断性变更</span><span class="sxs-lookup"><span data-stu-id="a54b1-211">Breaking changes</span></span>
> 2. <span data-ttu-id="a54b1-212">新增功能</span><span class="sxs-lookup"><span data-stu-id="a54b1-212">New features</span></span>
> 3. <span data-ttu-id="a54b1-213">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="a54b1-213">Bug fixes</span></span>
> 
> <span data-ttu-id="a54b1-214">如果你已在存储库中跟踪发行说明或更改日志，则还可以包含指向相关文件的链接。</span><span class="sxs-lookup"><span data-stu-id="a54b1-214">If you already track release notes or a changelog in your repo, you can also include a link to the relevant file.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a54b1-215">相关主题</span><span class="sxs-lookup"><span data-stu-id="a54b1-215">Related topics</span></span>

- [<span data-ttu-id="a54b1-216">创建并发布包 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="a54b1-216">Create and publish a package (dotnet CLI)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [<span data-ttu-id="a54b1-217">创建并发布包 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a54b1-217">Create and publish a package (Visual Studio)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)