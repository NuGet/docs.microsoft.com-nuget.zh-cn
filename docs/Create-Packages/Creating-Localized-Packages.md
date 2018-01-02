---
title: "如何创建本地化 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 824c3f45-c6c2-4c82-9d6d-62a19bfdc4a4
description: "详细介绍创建本地化 NuGet 包的两种方法：将所有程序集包含在一个包中，或者发布单独的程序集。"
keywords: "NuGet 包本地化, NuGet 附属程序集, 创建本地化包, NuGet 本地化约定"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aa48e77bd0e64cf45292687a2d4cada198ff5749
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="4d4b8-104">创建本地化 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4d4b8-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="4d4b8-105">有两种方法可创建库的本地化版本：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="4d4b8-106">将所有本地化资源程序集包含在一个包中。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-106">Include all localized resources assemblies in a single package.</span></span>
2. <span data-ttu-id="4d4b8-107">遵循一组严格的约定，创建单独的本地化附属包（NuGet 1.8 及更高版本）。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="4d4b8-108">两种方法各有优缺点，如以下部分中所述。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="4d4b8-109">本地化资源程序集位于一个包中</span><span class="sxs-lookup"><span data-stu-id="4d4b8-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="4d4b8-110">将本地化资源程序集包含在一个包中通常是最简单的方法。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="4d4b8-111">若要执行此操作，请在 `lib` 中创建文件夹用于支持的语言，而不是包默认语言（假定为 en-us）。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="4d4b8-112">在这些文件夹中，可以放置资源程序集和本地化 IntelliSense XML 文件。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="4d4b8-113">例如，以下文件夹结构支持德语 (de)、意大利语 (it)、日语 (ja)、俄语 (ru)、简体中文 (zh-Hans) 和繁体中文 (zh-Hant)：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="4d4b8-114">可以看到，这些语言全都列在 `net40` 目标框架文件夹下。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="4d4b8-115">如果[支持多个框架](../create-packages/supporting-multiple-target-frameworks.md)，则 `lib` 下将有每个变体的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you'll have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="4d4b8-116">这些文件夹准备就绪后，即可在 `.nuspec` 中引用所有文件：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-116">With these folders in place, you'll then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="4d4b8-117">使用此方法的一个包示例为 [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0)。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="4d4b8-118">优缺点</span><span class="sxs-lookup"><span data-stu-id="4d4b8-118">Advantages and disadvantages</span></span>

<span data-ttu-id="4d4b8-119">将所有语言捆绑到一个包中存在几个缺点：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="4d4b8-120">**共享元数据**：由于 NuGet 包只可包含一个 `.nuspec` 文件，因此仅可以为一种语言提供元数据。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="4d4b8-121">也就是说，NuGet 当前不支持本地化元数据。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-121">That is, NuGet does not present support localized metadata.</span></span>
2. <span data-ttu-id="4d4b8-122">**包大小**：根据支持的语言数量，库可能变得相当大，这会减慢包的安装和还原速度。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
3. <span data-ttu-id="4d4b8-123">**同时发布**：将本地化文件捆绑到一个包中需要同时发布该包中的所有资产，而不是能够单独发布每个本地化。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="4d4b8-124">此外，对任何一个本地化的任何更新都需要整个包的新版本。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="4d4b8-125">然而，它也存在几个优点：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="4d4b8-126">**简单**：包的使用者安装一次即可获得支持的所有语言，而不必单独安装每种语言。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="4d4b8-127">在 nuget.org 上查找单个包也更加轻松。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-127">A single package is also easier to find on nuget.org.</span></span>
2. <span data-ttu-id="4d4b8-128">**耦合版本**：由于所有资源程序集与主程序集都位于相同的包中，因此它们共享相同的版本号，且不存在错误分离的风险。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>


## <a name="localized-satellite-packages"></a><span data-ttu-id="4d4b8-129">本地化附属包</span><span class="sxs-lookup"><span data-stu-id="4d4b8-129">Localized satellite packages</span></span>

<span data-ttu-id="4d4b8-130">类似于 .NET Framework 支持附属程序集的方式，此方法将本地化资源和 IntelliSense XML 文件分离为附属包。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="4d4b8-131">若要执行此操作，主包会使用命名约定 `{identifier}.{version}.nupkg` 并包含默认语言（如 en-US）的程序集。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="4d4b8-132">例如，`ContosoUtilities.1.0.0.nupkg` 将包含以下结构：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="4d4b8-133">附属程序集然后会使用命名约定 `{identifier}.{language}.{version}.nupkg`，如 `ContosoUtilities.de.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="4d4b8-134">标识符必须与主包完全匹配。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="4d4b8-135">由于这是单独的包，因此它本身具有包含本地化元数据的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="4d4b8-136">请注意，`.nuspec` 中的语言必须与文件名中所使用的语言匹配。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="4d4b8-137">附属程序集还必须使用 [] 版本表示法，将主包的确切版本声明为依赖项（请参阅[包版本控制](../reference/package-versioning.md)）。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="4d4b8-138">例如，`ContosoUtilities.de.1.0.0.nupkg` 必须使用 `[1.0.0]` 表示法声明对 `ContosoUtilities.1.0.0.nupkg` 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="4d4b8-139">当然，附属包的版本号可以与主包不同。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="4d4b8-140">然后，附属包结构必须将资源程序集和 XML IntelliSense 包含在与包文件名中的 `{language}` 匹配的子文件夹中：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="4d4b8-141">注意：除非需要特定的子区域性（如 `ja-JP`），否则请始终使用更高级别的语言标识符，如 `ja`。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="4d4b8-142">在附属程序集中，NuGet 仅会识别文件名与 `{language}` 匹配的文件夹中的这些文件。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="4d4b8-143">将忽略所有其他成员。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-143">All others are ignored.</span></span>

<span data-ttu-id="4d4b8-144">如果满足所有这些约定，NuGet 会将包识别为附属包并将本地化文件安装到主包的 `lib` 文件夹中，就好像它们最初就进行了捆绑。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="4d4b8-145">卸载附属程序包将从该相同文件夹中删除其文件。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="4d4b8-146">你将以相同方式为支持的每种语言创建其他附属程序集。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="4d4b8-147">例如，检查一组 ASP.NET MVC 包：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

* <span data-ttu-id="4d4b8-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc)（主要为英语）</span><span class="sxs-lookup"><span data-stu-id="4d4b8-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
* <span data-ttu-id="4d4b8-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de)（德语）</span><span class="sxs-lookup"><span data-stu-id="4d4b8-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
* <span data-ttu-id="4d4b8-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja)（日语）</span><span class="sxs-lookup"><span data-stu-id="4d4b8-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
* <span data-ttu-id="4d4b8-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans)（简体中文）</span><span class="sxs-lookup"><span data-stu-id="4d4b8-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
* <span data-ttu-id="4d4b8-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant)（繁体中文）</span><span class="sxs-lookup"><span data-stu-id="4d4b8-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="4d4b8-153">所需约定摘要</span><span class="sxs-lookup"><span data-stu-id="4d4b8-153">Summary of required conventions</span></span>

- <span data-ttu-id="4d4b8-154">主包必须命名为 `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4d4b8-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="4d4b8-155">附属包必须命名为 `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4d4b8-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="4d4b8-156">附属包的 `.nuspec` 必须指定其语言以与文件名匹配。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="4d4b8-157">附属包必须在其 `.nuspec` 文件中使用 [] 表示法，声明对主包确切版本的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="4d4b8-158">不支持范围。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-158">Ranges are not supported.</span></span>
- <span data-ttu-id="4d4b8-159">附属包必须将文件放置于文件名与 `{language}` 完全匹配的 `lib\[{framework}\]{language}` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="4d4b8-160">优缺点</span><span class="sxs-lookup"><span data-stu-id="4d4b8-160">Advantages and disadvantages</span></span>

<span data-ttu-id="4d4b8-161">使用附属包有几个优点：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="4d4b8-162">**包大小**：主包的总内存占用量最小化，而且使用者仅承担要使用的语言的费用。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
2. <span data-ttu-id="4d4b8-163">**单独的元数据**：每个附属包都有自己的 `.nuspec` 文件，因此也拥有自己的本地化元数据。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="4d4b8-164">借此，一些使用者可通过使用本地化术语搜索 nuget.org，更加轻松地查找包。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
3. <span data-ttu-id="4d4b8-165">**分离发布**：附属程序集可随着时间推移进行发布，而不是一次完成，从而分散了本地化工作量。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="4d4b8-166">然而，附属包也有其自身的一些缺点：</span><span class="sxs-lookup"><span data-stu-id="4d4b8-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="4d4b8-167">**混乱**：许多包（而不是一个包）可能会导致 nuget.org 上的搜索结果混乱以及 Visual Studio 项目中的引用列表变长。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
2. <span data-ttu-id="4d4b8-168">**严格的约定**。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-168">**Strict conventions**.</span></span> <span data-ttu-id="4d4b8-169">附属包必须完全遵循约定，否则将不会正确选取本地化版本。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
3. <span data-ttu-id="4d4b8-170">**版本控制**：每个附属包必须对主包具有确切版本的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="4d4b8-171">这意味着更新主包可能也需要更新所有附属程序包，即使未更改资源。</span><span class="sxs-lookup"><span data-stu-id="4d4b8-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
