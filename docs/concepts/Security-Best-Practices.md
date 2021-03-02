---
title: 关于安全软件供应链的最佳做法
description: 使用 NuGet 和 GitHub 保护软件供应链的最佳做法。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 125579832db2ac32217d24f6fc6fc1b555f54350
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101379"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a><span data-ttu-id="242ff-103">关于安全软件供应链的最佳做法</span><span class="sxs-lookup"><span data-stu-id="242ff-103">Best practices for a secure software supply chain</span></span>

<span data-ttu-id="242ff-104">开源代码无处不在。</span><span class="sxs-lookup"><span data-stu-id="242ff-104">Open Source is everywhere.</span></span> <span data-ttu-id="242ff-105">它存在于许多专有代码库和社区项目中。</span><span class="sxs-lookup"><span data-stu-id="242ff-105">It is in many proprietary codebases and community projects.</span></span> <span data-ttu-id="242ff-106">对于组织和个人来说，现在的问题不是你是否在使用开源代码，而是你在使用什么开源代码，以及使用多少。</span><span class="sxs-lookup"><span data-stu-id="242ff-106">For organizations and individuals, the question today is not whether you are or are not using open-source code, but what open-source code you are using, and how much.</span></span>

<span data-ttu-id="242ff-107">如果你不知道软件供应链中的内容，当其中一个依赖项中的上游漏洞可能是致命的，你和你的客户就容易受到潜在的损害。</span><span class="sxs-lookup"><span data-stu-id="242ff-107">If you're not aware of what is in your software supply chain, an upstream vulnerability in one of your dependencies can be fatal, making you, and your customers, vulnerable to a potential compromise.</span></span> <span data-ttu-id="242ff-108">在本文档中，我们将深入探讨术语“软件供应链”的含义、为什么它很重要，以及如何通过最佳做法来帮助保护项目的供应链。</span><span class="sxs-lookup"><span data-stu-id="242ff-108">In this document, we will dive deeper into what the term “software supply chain” means, why it matters, and how you can help secure your project’s supply chain with best practices.</span></span>

![State of the Octoverse 2020 - 开放源代码](media/opensource-percent.png)

## <a name="dependencies"></a><span data-ttu-id="242ff-110">依赖项</span><span class="sxs-lookup"><span data-stu-id="242ff-110">Dependencies</span></span> 

<span data-ttu-id="242ff-111">术语“软件供应链”用于指进入软件中的所有内容以及它的来源。</span><span class="sxs-lookup"><span data-stu-id="242ff-111">The term software supply chain is used to refer to everything that goes into your software and where it comes from.</span></span> <span data-ttu-id="242ff-112">它是软件供应链依赖的依赖项的依赖关系和属性。</span><span class="sxs-lookup"><span data-stu-id="242ff-112">It is the dependencies and properties of your dependencies that your software supply chain depends on.</span></span> <span data-ttu-id="242ff-113">依赖项是软件运行时需要的内容。</span><span class="sxs-lookup"><span data-stu-id="242ff-113">A dependency is what your software needs to run.</span></span> <span data-ttu-id="242ff-114">它可以是代码、二进制文件或其他组件，也可以是这些组件的来源，例如存储库或包管理器。</span><span class="sxs-lookup"><span data-stu-id="242ff-114">It can be code, binaries, or other components, and where they come from, such as a repository or package manager.</span></span>

<span data-ttu-id="242ff-115">它包括代码作者、贡献时间、审查安全问题的方式、已知漏洞、受支持的版本、许可证信息，以及在整个过程中的任何时候接触到它的任何内容。</span><span class="sxs-lookup"><span data-stu-id="242ff-115">It includes who wrote the code, when it was contributed, how it was reviewed for security issues, known vulnerabilities, supported versions, license information, and just about anything that touches it at any point of the process.</span></span>

<span data-ttu-id="242ff-116">供应链还包括套件中除单个应用程序外的其他部分，如生成和打包脚本或运行应用程序所依赖的基础结构的软件。</span><span class="sxs-lookup"><span data-stu-id="242ff-116">Your supply chain also encompasses other parts of your stack beyond a single application, such as your build and packaging scripts or the software that runs the infrastructure your application relies on.</span></span>

## <a name="vulnerabilities"></a><span data-ttu-id="242ff-117">漏洞</span><span class="sxs-lookup"><span data-stu-id="242ff-117">Vulnerabilities</span></span>

<span data-ttu-id="242ff-118">如今，软件的依赖关系非常普遍。</span><span class="sxs-lookup"><span data-stu-id="242ff-118">Today, software dependencies are pervasive.</span></span> <span data-ttu-id="242ff-119">经常见到项目使用数百个开源依赖项来实现某种功能，而你不必亲自编写该功能。</span><span class="sxs-lookup"><span data-stu-id="242ff-119">It is quite common for your projects to use hundreds of open-source dependencies for functionality that you did not have to write yourself.</span></span> <span data-ttu-id="242ff-120">这可能意味着大多数应用程序都包含并非你创作的代码。</span><span class="sxs-lookup"><span data-stu-id="242ff-120">This may mean that most of your application consists of code that you did not author.</span></span> 

![State of the Octoverse 2020 - 依赖关系](media/dependencies.png)

<span data-ttu-id="242ff-122">第三方或开源依赖项中可能存在的漏洞多半是依赖项，因为你不能像自己编写的代码那样严格控制这些依赖项，可能会在你的供应链中产生潜在的安全风险。</span><span class="sxs-lookup"><span data-stu-id="242ff-122">Possible vulnerabilities in your third-party or open-source dependencies, are presumably dependencies you cannot control as tightly as the code you write, which can create potential security risks in your supply chain.</span></span>

<span data-ttu-id="242ff-123">如果这些依赖项中有一个存在漏洞，则很可能你也会遇到漏洞。</span><span class="sxs-lookup"><span data-stu-id="242ff-123">If one of these dependencies has a vulnerability, the chances are you have a vulnerability as well.</span></span> <span data-ttu-id="242ff-124">这可能很可怕，因为你的一个依赖项可能会发生更改，而你甚至都不知道。</span><span class="sxs-lookup"><span data-stu-id="242ff-124">This can be scary as one of your dependencies may change without you even knowing.</span></span> <span data-ttu-id="242ff-125">即使依赖项中存在的漏洞现在不会被攻击，将来也会被攻击。</span><span class="sxs-lookup"><span data-stu-id="242ff-125">Even if a vulnerability exists in a dependency today, but is not exploitable, it can be exploitable in the future.</span></span> 

<span data-ttu-id="242ff-126">能够利用数千名开源开发者和库作者的工作成果意味着数千名陌生人可以有效地直接为你贡献生产代码。</span><span class="sxs-lookup"><span data-stu-id="242ff-126">Being able to leverage the work of thousands of open-source developers and library authors means that thousands of strangers can effectively contribute directly to your production code.</span></span> <span data-ttu-id="242ff-127">通过产品供应链获得的产品会受到未修补漏洞、无意错误甚至对依赖项的恶意攻击的影响。</span><span class="sxs-lookup"><span data-stu-id="242ff-127">Your product, through your software supply chain, is affected by unpatched vulnerabilities, innocent mistakes, or even malicious attacks against dependencies.</span></span>

## <a name="supply-chain-compromises"></a><span data-ttu-id="242ff-128">供应链漏洞</span><span class="sxs-lookup"><span data-stu-id="242ff-128">Supply chain compromises</span></span>

<span data-ttu-id="242ff-129">供应链的传统定义来自于制造业；它是制造和供应某物所需的过程链。</span><span class="sxs-lookup"><span data-stu-id="242ff-129">The traditional definition of a supply chain comes from manufacturing; it is the chain of processes required to make and supply something.</span></span> <span data-ttu-id="242ff-130">它包括规划、材料供应、制造和零售。</span><span class="sxs-lookup"><span data-stu-id="242ff-130">It includes planning, supply of materials, manufacturing, and retail.</span></span> <span data-ttu-id="242ff-131">软件供应链类似，但不是供应材料，而是供应代码。</span><span class="sxs-lookup"><span data-stu-id="242ff-131">A software supply chain is similar, except instead of materials, it is code.</span></span> <span data-ttu-id="242ff-132">它不是制造，而是开发。</span><span class="sxs-lookup"><span data-stu-id="242ff-132">Instead of manufacturing, it is development.</span></span> <span data-ttu-id="242ff-133">代码不是从地下挖矿石，而是由供应商提供，分为商业来源和开放源，而一般情况下，开源代码来自存储库。</span><span class="sxs-lookup"><span data-stu-id="242ff-133">Instead of digging ore from the ground, code is sourced from suppliers, commercial or open source, and, in general, the open-source code comes from repositories.</span></span> <span data-ttu-id="242ff-134">从存储库添加代码意味着产品依赖于该代码。</span><span class="sxs-lookup"><span data-stu-id="242ff-134">Adding code from a repository means your product takes a dependency on that code.</span></span>

<span data-ttu-id="242ff-135">举个软件供应链攻击的例子：当恶意代码被故意加入依赖项中，使用该依赖项的供应链将代码分发给受害者时，就会发生这种攻击。</span><span class="sxs-lookup"><span data-stu-id="242ff-135">One example of a software supply chain attack occurs when malicious code is purposefully added to a dependency, using the supply chain of that dependency to distribute the code to its victims.</span></span> <span data-ttu-id="242ff-136">供应链攻击是真实存在的。</span><span class="sxs-lookup"><span data-stu-id="242ff-136">Supply chain attacks are real.</span></span> <span data-ttu-id="242ff-137">攻击供应链的方法有很多：从直接以新贡献者的身份插入恶意代码到在别人不注意的情况下接管贡献者的帐户，甚至破解签名密钥来分发不属于正式依赖项的软件。</span><span class="sxs-lookup"><span data-stu-id="242ff-137">There are many methods to attack a supply chain, from directly inserting malicious code as a new contributor, to taking over a contributor’s account without others noticing, or even compromising a signing key to distribute software that is not officially part of the dependency.</span></span>

<span data-ttu-id="242ff-138">软件供应链攻击本身很少是最终目标，但提供了一个让攻击者插入恶意软件或为将来的访问提供后门的机会。</span><span class="sxs-lookup"><span data-stu-id="242ff-138">A software supply chain attack is in and of itself rarely the end goal, rather it is the beginning of an opportunity for an attacker to insert malware or provide a backdoor for future access.</span></span>

![State of the Octoverse 2020 - 漏洞生命周期](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a><span data-ttu-id="242ff-140">未修补软件</span><span class="sxs-lookup"><span data-stu-id="242ff-140">Unpatched software</span></span>

<span data-ttu-id="242ff-141">当今开源代码的使用非常普遍，而且预计不会很快放缓。</span><span class="sxs-lookup"><span data-stu-id="242ff-141">The use of open source today is significant and is not expected to slow down anytime soon.</span></span> <span data-ttu-id="242ff-142">假设我们不打算停止使用开源软件，则提供链安全性的威胁是未修补软件。</span><span class="sxs-lookup"><span data-stu-id="242ff-142">Given that we are not going to stop using open-source software, the threat to supply chain security is unpatched software.</span></span> <span data-ttu-id="242ff-143">知道这一点，你如何解决项目的依赖项有漏洞的风险呢？</span><span class="sxs-lookup"><span data-stu-id="242ff-143">Knowing that, how can you address the risk that a dependency of your project has a vulnerability?</span></span>

- <span data-ttu-id="242ff-144">**了解环境中的内容。**</span><span class="sxs-lookup"><span data-stu-id="242ff-144">**Knowing what is in your environment.**</span></span> <span data-ttu-id="242ff-145">这需要发现依赖项和任何过渡性依赖向，以了解这些依赖项的风险，如漏洞或许可限制。</span><span class="sxs-lookup"><span data-stu-id="242ff-145">This requires discovering your dependencies and any transitive dependencies to understand the risks of those dependencies such as vulnerabilities or licensing restrictions.</span></span>
- <span data-ttu-id="242ff-146">**管理依赖项。**</span><span class="sxs-lookup"><span data-stu-id="242ff-146">**Manage your dependencies.**</span></span> <span data-ttu-id="242ff-147">发现新的安全漏洞时，必须确定你是否受影响，如果是，则更新到可用的最新版本和安全修补程序。</span><span class="sxs-lookup"><span data-stu-id="242ff-147">When a new security vulnerability is discovered, you must determine whether you are impacted, and if so, update to the latest version and security patch available.</span></span> <span data-ttu-id="242ff-148">这对于审查引入新依赖项的更改或定期审计旧的依赖项尤为重要。</span><span class="sxs-lookup"><span data-stu-id="242ff-148">This is especially important to review changes that introduce new dependencies or regularly auditing older dependencies.</span></span>
- <span data-ttu-id="242ff-149">**监视供应链。**</span><span class="sxs-lookup"><span data-stu-id="242ff-149">**Monitor your supply chain.**</span></span> <span data-ttu-id="242ff-150">这是通过审核已有的控件来管理依赖项。</span><span class="sxs-lookup"><span data-stu-id="242ff-150">This is by auditing the controls you have in place to manage your dependencies.</span></span> <span data-ttu-id="242ff-151">这将帮助你为依赖项强制实施更严格的条件。</span><span class="sxs-lookup"><span data-stu-id="242ff-151">This will help you enforce more restrictive conditions to be met for your dependencies.</span></span>

![State of the Octoverse 2020 - 顾问](media/advisories.png)

<span data-ttu-id="242ff-153">我们将介绍 NuGet 和 GitHub 提供的各种工具和技术，你现在可以使用它们来解决项目中的潜在风险。</span><span class="sxs-lookup"><span data-stu-id="242ff-153">We will cover various tools and techniques that NuGet and GitHub provides, which you can use today to address potential risks inside your project.</span></span> 

## <a name="knowing-what-is-in-your-environment"></a><span data-ttu-id="242ff-154">了解环境中的内容</span><span class="sxs-lookup"><span data-stu-id="242ff-154">Knowing what is in your environment</span></span>

### <a name="nuget-dependency-graph"></a><span data-ttu-id="242ff-155">NuGet 依赖项关系图</span><span class="sxs-lookup"><span data-stu-id="242ff-155">NuGet dependency graph</span></span>

<span data-ttu-id="242ff-156">**📦 包使用者**</span><span class="sxs-lookup"><span data-stu-id="242ff-156">**📦 Package Consumer**</span></span>

<span data-ttu-id="242ff-157">可以通过直接查看相应的项目文件来查看项目中的 NuGet 依赖项。</span><span class="sxs-lookup"><span data-stu-id="242ff-157">You can view your NuGet dependencies in your project by looking directly at the respective project file.</span></span>

<span data-ttu-id="242ff-158">一般在以下两个位置中可以找到：</span><span class="sxs-lookup"><span data-stu-id="242ff-158">This is typically found in one of two places:</span></span>

-   <span data-ttu-id="242ff-159">[`packages.config`](../reference/packages-config.md) – 位于项目根目录中。</span><span class="sxs-lookup"><span data-stu-id="242ff-159">[`packages.config`](../reference/packages-config.md) – Located in the project root.</span></span>
-   <span data-ttu-id="242ff-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – 位于项目根文件中。</span><span class="sxs-lookup"><span data-stu-id="242ff-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Located in the project file.</span></span> 

<span data-ttu-id="242ff-161">根据你用来管理 NuGet 依赖项的方法，还可以使用 Visual Studio 在[解决方案资源管理器](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer)或 [NuGet 包管理器](../consume-packages/install-use-packages-visual-studio.md)中直接查看依赖项。</span><span class="sxs-lookup"><span data-stu-id="242ff-161">Depending on what method you use to manage your NuGet dependencies, you can also use Visual Studio to view your dependencies directly in [Solution Explorer](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer) or [NuGet Package Manager](../consume-packages/install-use-packages-visual-studio.md).</span></span>

<span data-ttu-id="242ff-162">在 CLI 环境中，可以使用 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令列出项目或解决方案的依赖项。</span><span class="sxs-lookup"><span data-stu-id="242ff-162">For CLI environments, you can use the [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command to list out your project or solution’s dependencies.</span></span> 

<span data-ttu-id="242ff-163">有关管理 NuGet 依赖项的详细信息，[请参阅以下文档](../consume-packages/overview-and-workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="242ff-163">For more information on managing NuGet dependencies, [see the following documentation](../consume-packages/overview-and-workflow.md).</span></span>

### <a name="github-dependency-graph"></a><span data-ttu-id="242ff-164">GitHub 依赖项关系图</span><span class="sxs-lookup"><span data-stu-id="242ff-164">GitHub dependency graph</span></span> 

<span data-ttu-id="242ff-165">**📦 包使用者 | 📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-165">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-166">可以使用 GitHub 的依赖项关系图来查看项目依赖的包以及依赖于该项目的存储库。</span><span class="sxs-lookup"><span data-stu-id="242ff-166">You can use GitHub’s dependency graph to see the packages your project depends on and the repositories that depend on it.</span></span> <span data-ttu-id="242ff-167">这可以帮助你查看其依赖项中检测到的任何漏洞。</span><span class="sxs-lookup"><span data-stu-id="242ff-167">This can help you see any vulnerabilities detected in its dependencies.</span></span>

<span data-ttu-id="242ff-168">有关 GitHub 存储库依赖项的详细信息，[请参阅以下文档](https://github.co/dependency-graph)。</span><span class="sxs-lookup"><span data-stu-id="242ff-168">For more information on GitHub repository dependencies, [see the following documentation](https://github.co/dependency-graph).</span></span>

### <a name="dependency-versions"></a><span data-ttu-id="242ff-169">依赖项版本</span><span class="sxs-lookup"><span data-stu-id="242ff-169">Dependency versions</span></span>

<span data-ttu-id="242ff-170">**📦 包使用者 | 📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-170">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-171">为了确保依赖项供应链的安全，你需要确保所有依赖项和工具定期更新到最新稳定版本，因为这些版本通常会包含最新功能和已知漏洞的安全修补程序。</span><span class="sxs-lookup"><span data-stu-id="242ff-171">To ensure a secure supply chain of dependencies, you will want to ensure that all of your dependencies & tooling are regularly updated to the latest stable version as they will often include the latest functionality and security patches to known vulnerabilities.</span></span> <span data-ttu-id="242ff-172">你的依赖项可以包括依赖的代码、使用的二进制文件、使用的工具以及其他组件。</span><span class="sxs-lookup"><span data-stu-id="242ff-172">Your dependencies can include code you depend on, binaries you consume, tooling you use, and other components.</span></span> <span data-ttu-id="242ff-173">这可能包括：</span><span class="sxs-lookup"><span data-stu-id="242ff-173">This may include:</span></span>

-   [<span data-ttu-id="242ff-174">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="242ff-174">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)
-   [<span data-ttu-id="242ff-175">.NET SDK 和运行时</span><span class="sxs-lookup"><span data-stu-id="242ff-175">.NET SDK & Runtime</span></span>](https://dotnet.microsoft.com/download)
-   [<span data-ttu-id="242ff-176">NuGet</span><span class="sxs-lookup"><span data-stu-id="242ff-176">NuGet</span></span>](https://www.nuget.org/downloads)
-   [<span data-ttu-id="242ff-177">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="242ff-177">NuGet packages</span></span>](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a><span data-ttu-id="242ff-178">管理依赖项</span><span class="sxs-lookup"><span data-stu-id="242ff-178">Manage your dependencies</span></span>

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a><span data-ttu-id="242ff-179">NuGet 已弃用且有漏洞的依赖项</span><span class="sxs-lookup"><span data-stu-id="242ff-179">NuGet deprecated and vulnerable dependencies</span></span>

<span data-ttu-id="242ff-180">**📦 包使用者 | 📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-180">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-181">可以使用 [dotnet CLI](/dotnet/core/tools/dotnet-list-package) 列出项目或解决方案中的任何已知的已弃用或有漏洞的依赖项。</span><span class="sxs-lookup"><span data-stu-id="242ff-181">You can use the [dotnet CLI](/dotnet/core/tools/dotnet-list-package) to list any known deprecated or vulnerable dependencies you may have inside your project or solution.</span></span> <span data-ttu-id="242ff-182">可以使用命令 `dotnet list package --deprecated` 或 `dotnet list package --vulnerable` 获得任何已知的弃用功能或漏洞的列表。</span><span class="sxs-lookup"><span data-stu-id="242ff-182">You can use the command `dotnet list package --deprecated` or `dotnet list package --vulnerable` to provide you a list of any known deprecations or vulnerabilities.</span></span>

### <a name="github-vulnerable-dependencies"></a><span data-ttu-id="242ff-183">GitHub 有漏洞的依赖项</span><span class="sxs-lookup"><span data-stu-id="242ff-183">GitHub vulnerable dependencies</span></span>

<span data-ttu-id="242ff-184">**📦 包使用者 | 📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-184">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-185">如果项目托管在 GitHub 上，则可以利用 [GitHub 安全性](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors)在项目中查找安全漏洞和错误，Dependabot 将通过针对你的代码库打开拉取请求来修复它们。</span><span class="sxs-lookup"><span data-stu-id="242ff-185">If your project is hosted on GitHub, you can leverage [GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) to find security vulnerabilities and errors in your project and Dependabot will fix them by opening up a pull request against your codebase.</span></span> 

<span data-ttu-id="242ff-186">在引入有漏洞的依赖项之前将其捕获是[“左移”](https://en.wikipedia.org/wiki/Shift-left_testing)的一个目标。</span><span class="sxs-lookup"><span data-stu-id="242ff-186">Catching vulnerable dependencies before they are introduced is one goal of the [“Shift Left”](https://en.wikipedia.org/wiki/Shift-left_testing) movement.</span></span> <span data-ttu-id="242ff-187">能够获得有关依赖项的信息（例如许可证、过渡性依赖项和依赖项的存在时间）可帮助你做到这一点。</span><span class="sxs-lookup"><span data-stu-id="242ff-187">Being able to have information about your dependencies such as their license, transitive dependencies, and the age of dependencies helps you do just that.</span></span>

<span data-ttu-id="242ff-188">有关 Dependabot 警报和安全更新的详细信息，[请参阅以下文档](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="242ff-188">For more information about Dependabot alerts & security updates, [see the following documentation](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).</span></span>

### <a name="nuget-feeds"></a><span data-ttu-id="242ff-189">NuGet 源</span><span class="sxs-lookup"><span data-stu-id="242ff-189">NuGet feeds</span></span>

<span data-ttu-id="242ff-190">**📦 包使用者**</span><span class="sxs-lookup"><span data-stu-id="242ff-190">**📦 Package Consumer**</span></span>

<span data-ttu-id="242ff-191">当使用多个公共和专用 NuGet 数据源的源时，可以从任何源下载包。</span><span class="sxs-lookup"><span data-stu-id="242ff-191">When using multiple public & private NuGet source feeds, a package can be downloaded from any of the feeds.</span></span> <span data-ttu-id="242ff-192">若要确保你的生成是可预测和安全的，且不受已知攻击（如[依赖项混淆](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)）的影响，最佳做法是了解包来自哪些特定的源。</span><span class="sxs-lookup"><span data-stu-id="242ff-192">To ensure your build is predictable and secure from known attacks such as [Dependency Confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), knowing what specific feed(s) your packages are coming from is a best practice.</span></span> <span data-ttu-id="242ff-193">可以使用具有上游追溯功能的单个源或专用源来提供保护。</span><span class="sxs-lookup"><span data-stu-id="242ff-193">You can use a single feed or private feed with upstreaming capabilities for protection.</span></span>

<span data-ttu-id="242ff-194">若要详细了解如何保护包源，请参阅[使用专用包源时降低风险的 3 种方法](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)。</span><span class="sxs-lookup"><span data-stu-id="242ff-194">For more information to secure your package feeds, see [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).</span></span>

### <a name="client-trust-policies"></a><span data-ttu-id="242ff-195">客户端信任策略</span><span class="sxs-lookup"><span data-stu-id="242ff-195">Client trust policies</span></span>

<span data-ttu-id="242ff-196">**📦 包使用者**</span><span class="sxs-lookup"><span data-stu-id="242ff-196">**📦 Package Consumer**</span></span>

<span data-ttu-id="242ff-197">你可以选择采用某些策略，以要求签署你所使用的包。</span><span class="sxs-lookup"><span data-stu-id="242ff-197">There are policies that you can opt-into in which you require the packages you use to be signed.</span></span> <span data-ttu-id="242ff-198">这样，只要包具有作者签名，你就可以信任包作者，或者如果包由 NuGet.org 进行存储库签名的特定用户或帐户拥有，就可以信任该包。</span><span class="sxs-lookup"><span data-stu-id="242ff-198">This allows you to trust a package author, as long as it is author signed, or trust a package if it is owned by a specific user or account that is repository signed by NuGet.org.</span></span>

<span data-ttu-id="242ff-199">若要配置客户端信任策略，[请参阅以下文档](../consume-packages/installing-signed-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="242ff-199">To configure client trust policies, [see the following documentation](../consume-packages/installing-signed-packages.md).</span></span>

### <a name="lock-files"></a><span data-ttu-id="242ff-200">锁定文件</span><span class="sxs-lookup"><span data-stu-id="242ff-200">Lock files</span></span>

<span data-ttu-id="242ff-201">**📦 包使用者**</span><span class="sxs-lookup"><span data-stu-id="242ff-201">**📦 Package Consumer**</span></span>

<span data-ttu-id="242ff-202">锁定文件存储包内容的哈希。</span><span class="sxs-lookup"><span data-stu-id="242ff-202">Lock files store the hash of your package’s content.</span></span> <span data-ttu-id="242ff-203">如果要安装的包的内容哈希与锁定文件匹配，则将确保包的可重复性。</span><span class="sxs-lookup"><span data-stu-id="242ff-203">If the content hash of a package you want to install matches with the lock file, it will ensure package repeatability.</span></span>

<span data-ttu-id="242ff-204">若要启用锁定文件，[请参阅以下文档](../consume-packages/package-references-in-project-files#locking-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="242ff-204">To enable lock files, [see the following documentation](../consume-packages/package-references-in-project-files#locking-dependencies).</span></span>

## <a name="monitor-your-supply-chain"></a><span data-ttu-id="242ff-205">监视供应链</span><span class="sxs-lookup"><span data-stu-id="242ff-205">Monitor your supply chain</span></span>

### <a name="github-secret-scanning"></a><span data-ttu-id="242ff-206">GitHub 机密扫描</span><span class="sxs-lookup"><span data-stu-id="242ff-206">GitHub secret scanning</span></span>

<span data-ttu-id="242ff-207">**📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-207">**📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-208">GitHub 会扫描 NuGet API 密钥的存储库，以防止欺诈性地使用意外提交的机密。</span><span class="sxs-lookup"><span data-stu-id="242ff-208">GitHub scans repositories for NuGet API keys to prevent fraudulent uses of secrets that were accidentally committed.</span></span> 

<span data-ttu-id="242ff-209">若要详细了解密钥扫描，请参阅[关于密钥扫描](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)。</span><span class="sxs-lookup"><span data-stu-id="242ff-209">To learn more about secret scanning, see [About secret scanning](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).</span></span>

### <a name="author-package-signing"></a><span data-ttu-id="242ff-210">作者包签名</span><span class="sxs-lookup"><span data-stu-id="242ff-210">Author Package Signing</span></span>

<span data-ttu-id="242ff-211">**📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-211">**📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-212">[作者签名](../reference/signed-packages-reference.md)允许包作者在包上加盖标识，方便使用者认出这是你创作的包。</span><span class="sxs-lookup"><span data-stu-id="242ff-212">[Author signing](../reference/signed-packages-reference.md) allows a package author to stamp their identity on a package and for a consumer to verify it came from you.</span></span> <span data-ttu-id="242ff-213">这可以保护内容不被篡改，并充当确定包来源和包真伪的唯一真实源。</span><span class="sxs-lookup"><span data-stu-id="242ff-213">This protects you against content tampering and serves as a single source of truth about the origin of the package and the package authenticity.</span></span> <span data-ttu-id="242ff-214">与客户端信任策略结合使用时，可以验证包是否来自特定的作者。</span><span class="sxs-lookup"><span data-stu-id="242ff-214">When combined with client trust policies, you can verify a package came from a specific author.</span></span>

<span data-ttu-id="242ff-215">要创作包签名，请参阅[对包进行签名](../create-packages/sign-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="242ff-215">To author sign a package, see [Sign a package](../create-packages/sign-a-package.md).</span></span>

### <a name="two-factor-authentication-2fa"></a><span data-ttu-id="242ff-216">双因素身份验证 (2FA)</span><span class="sxs-lookup"><span data-stu-id="242ff-216">Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="242ff-217">**📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-217">**📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-218">启用双因素身份验证 (2FA) 在[登录到 GitHub 帐户](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)或 [NuGet.org 公共包存储库](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)时，可以增加额外的安全层。</span><span class="sxs-lookup"><span data-stu-id="242ff-218">Enabling two-factor authentication (2FA) can add an extra layer of security when [logging into your GitHub account](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) or the [NuGet.org public package repository](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa).</span></span> <span data-ttu-id="242ff-219">建议启用双因素身份验证来保护帐户。</span><span class="sxs-lookup"><span data-stu-id="242ff-219">It is recommended that you enable two-factor authentication to protect your account.</span></span>

### <a name="package-id-prefix-reservation"></a><span data-ttu-id="242ff-220">包 ID 前缀预留</span><span class="sxs-lookup"><span data-stu-id="242ff-220">Package ID prefix reservation</span></span> 

<span data-ttu-id="242ff-221">**📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-221">**📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-222">为了保护包的标识，可以使用各自的命名空间保留与匹配的所有者关联的包 ID 前缀，前提是包 ID 前缀符合[指定标准](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="242ff-222">To protect the identity of your packages, you can reserve a package ID prefix with your respective namespace to associate a matching owner if your package ID prefix properly falls under the [specified criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).</span></span> 

<span data-ttu-id="242ff-223">若要了解有关保留 ID 前缀的信息，请参阅[包 ID 前缀保留](../nuget-org/id-prefix-reservation.md)。</span><span class="sxs-lookup"><span data-stu-id="242ff-223">To learn about reserving ID prefixes, see [Package ID prefix reservation](../nuget-org/id-prefix-reservation.md).</span></span>

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a><span data-ttu-id="242ff-224">弃用和下架有漏洞的包</span><span class="sxs-lookup"><span data-stu-id="242ff-224">Deprecating and unlisting a vulnerable package</span></span>

<span data-ttu-id="242ff-225">**📦🖊 包作者**</span><span class="sxs-lookup"><span data-stu-id="242ff-225">**📦🖊 Package Author**</span></span>

<span data-ttu-id="242ff-226">为了保护 .NET 包生态系统，当你发现自己创作的包中存在漏洞时，请务必将该包弃用并下架，以防用户搜到该包。</span><span class="sxs-lookup"><span data-stu-id="242ff-226">To protect the .NET package ecosystem when you are aware of a vulnerability in a package you have authored, do your best to deprecate and unlist the package so it is hidden from users searching for packages.</span></span> <span data-ttu-id="242ff-227">如果你正在使用已弃用且下架的包，应避免使用该包。</span><span class="sxs-lookup"><span data-stu-id="242ff-227">If you are consuming a package that is deprecated and unlisted, you should avoid using the package.</span></span>

<span data-ttu-id="242ff-228">若要了解如何将包弃用和下架，请参阅以下有关将包[弃用](../nuget-org/deprecate-packages.md)和[下架](../nuget-org/policies/deleting-packages.md#unlisting-a-package)的文档。</span><span class="sxs-lookup"><span data-stu-id="242ff-228">To learn how to deprecate and unlist a package, see the following documentation on [deprecating](../nuget-org/deprecate-packages.md) and [unlisting packages](../nuget-org/policies/deleting-packages.md#unlisting-a-package).</span></span>

## <a name="summary"></a><span data-ttu-id="242ff-229">总结</span><span class="sxs-lookup"><span data-stu-id="242ff-229">Summary</span></span>

<span data-ttu-id="242ff-230">软件供应链是进入或影响代码的任何内容。</span><span class="sxs-lookup"><span data-stu-id="242ff-230">Your software supply chain is anything that goes into or affects your code.</span></span> <span data-ttu-id="242ff-231">即使供应链漏洞真实存在且发展迅速，它们仍非常罕见；因此，你可以做的最重要的事情就是通过了解依赖项、管理依赖项和监视供应链来保护供应链 。</span><span class="sxs-lookup"><span data-stu-id="242ff-231">Even though supply chain compromises are real and growing in popularity, they are still rare; so the most important thing you can do is protect your supply chain by **being aware of your dependencies, managing your dependencies** and **monitoring your supply chain.**</span></span>

<span data-ttu-id="242ff-232">你已经了解 NuGet 和 [GitHub](/learn/modules/maintain-secure-repository-github/) 提供的用于更高效查看、管理和监视供应链的各种方法。</span><span class="sxs-lookup"><span data-stu-id="242ff-232">You learned about various methods that NuGet and [GitHub](/learn/modules/maintain-secure-repository-github/) provide that are available to you today to be more effective in viewing, managing, and monitoring your supply chain.</span></span>

<span data-ttu-id="242ff-233">有关保护全球软件的详细信息，请参阅 [State of the Octoverse 2020 安全报告](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)。</span><span class="sxs-lookup"><span data-stu-id="242ff-233">For more information about securing the world's software, see [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).</span></span>
