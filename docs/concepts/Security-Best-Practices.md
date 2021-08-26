---
title: 关于安全软件供应链的最佳做法
description: 使用 NuGet 和 GitHub 保护软件供应链的最佳做法。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726972"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>关于安全软件供应链的最佳做法

开源代码无处不在。 它存在于许多专有代码库和社区项目中。 对于组织和个人来说，现在的问题不是你是否在使用开源代码，而是你在使用什么开源代码，以及使用多少。

如果你不知道软件供应链中的内容，当其中一个依赖项中的上游漏洞可能是致命的，你和你的客户就容易受到潜在的损害。 在本文档中，我们将深入探讨术语“软件供应链”的含义、为什么它很重要，以及如何通过最佳做法来帮助保护项目的供应链。

![State of the Octoverse 2020 - 开放源代码](media/opensource-percent.png)

## <a name="dependencies"></a>依赖项 

术语“软件供应链”用于指进入软件中的所有内容以及它的来源。 它是软件供应链依赖的依赖项的依赖关系和属性。 依赖项是软件运行时需要的内容。 它可以是代码、二进制文件或其他组件，也可以是这些组件的来源，例如存储库或包管理器。

它包括代码作者、贡献时间、审查安全问题的方式、已知漏洞、受支持的版本、许可证信息，以及在整个过程中的任何时候接触到它的任何内容。

供应链还包括套件中除单个应用程序外的其他部分，如生成和打包脚本或运行应用程序所依赖的基础结构的软件。

## <a name="vulnerabilities"></a>漏洞

如今，软件的依赖关系非常普遍。 经常见到项目使用数百个开源依赖项来实现某种功能，而你不必亲自编写该功能。 这可能意味着大多数应用程序都包含并非你创作的代码。 

![State of the Octoverse 2020 - 依赖关系](media/dependencies.png)

第三方或开源依赖项中可能存在的漏洞多半是依赖项，因为你不能像自己编写的代码那样严格控制这些依赖项，可能会在你的供应链中产生潜在的安全风险。

如果这些依赖项中有一个存在漏洞，则很可能你也会遇到漏洞。 这可能很可怕，因为你的一个依赖项可能会发生更改，而你甚至都不知道。 即使依赖项中存在的漏洞现在不会被攻击，将来也会被攻击。 

能够利用数千名开源开发者和库作者的工作成果意味着数千名陌生人可以有效地直接为你贡献生产代码。 通过产品供应链获得的产品会受到未修补漏洞、无意错误甚至对依赖项的恶意攻击的影响。

## <a name="supply-chain-compromises"></a>供应链漏洞

供应链的传统定义来自于制造业；它是制造和供应某物所需的过程链。 它包括规划、材料供应、制造和零售。 软件供应链类似，但不是供应材料，而是供应代码。 它不是制造，而是开发。 代码不是从地下挖矿石，而是由供应商提供，分为商业来源和开放源，而一般情况下，开源代码来自存储库。 从存储库添加代码意味着产品依赖于该代码。

举个软件供应链攻击的例子：当恶意代码被故意加入依赖项中，使用该依赖项的供应链将代码分发给受害者时，就会发生这种攻击。 供应链攻击是真实存在的。 攻击供应链的方法有很多：从直接以新贡献者的身份插入恶意代码到在别人不注意的情况下接管贡献者的帐户，甚至破解签名密钥来分发不属于正式依赖项的软件。

软件供应链攻击本身很少是最终目标，但提供了一个让攻击者插入恶意软件或为将来的访问提供后门的机会。

![State of the Octoverse 2020 - 漏洞生命周期](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>未修补软件

当今开源代码的使用非常普遍，而且预计不会很快放缓。 假设我们不打算停止使用开源软件，则提供链安全性的威胁是未修补软件。 知道这一点，你如何解决项目的依赖项有漏洞的风险呢？

- **了解环境中的内容。** 这需要发现依赖项和任何过渡性依赖向，以了解这些依赖项的风险，如漏洞或许可限制。
- **管理依赖项。** 发现新的安全漏洞时，必须确定你是否受影响，如果是，则更新到可用的最新版本和安全修补程序。 这对于审查引入新依赖项的更改或定期审计旧的依赖项尤为重要。
- **监视供应链。** 这是通过审核已有的控件来管理依赖项。 这将帮助你为依赖项强制实施更严格的条件。

![State of the Octoverse 2020 - 顾问](media/advisories.png)

我们将介绍 NuGet 和 GitHub 提供的各种工具和技术，你现在可以使用它们来解决项目中的潜在风险。 

## <a name="knowing-what-is-in-your-environment"></a>了解环境中的内容

### <a name="nuget-dependency-graph"></a>NuGet 依赖项关系图

**📦 包使用者**

可以通过直接查看相应的项目文件来查看项目中的 NuGet 依赖项。

一般在以下两个位置中可以找到：

-   [`packages.config`](../reference/packages-config.md) – 位于项目根目录中。
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – 位于项目根文件中。 

根据你用来管理 NuGet 依赖项的方法，还可以使用 Visual Studio 在[解决方案资源管理器](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer)或 [NuGet 包管理器](../consume-packages/install-use-packages-visual-studio.md)中直接查看依赖项。

在 CLI 环境中，可以使用 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令列出项目或解决方案的依赖项。 

有关管理 NuGet 依赖项的详细信息，[请参阅以下文档](../consume-packages/overview-and-workflow.md)。

### <a name="github-dependency-graph"></a>GitHub 依赖项关系图 

**📦 包使用者 | 📦🖊 包作者**

可以使用 GitHub 的依赖项关系图来查看项目依赖的包以及依赖于该项目的存储库。 这可以帮助你查看其依赖项中检测到的任何漏洞。

有关 GitHub 存储库依赖项的详细信息，[请参阅以下文档](https://github.co/dependency-graph)。

### <a name="dependency-versions"></a>依赖项版本

**📦 包使用者 | 📦🖊 包作者**

为了确保依赖项供应链的安全，你需要确保所有依赖项和工具定期更新到最新稳定版本，因为这些版本通常会包含最新功能和已知漏洞的安全修补程序。 你的依赖项可以包括依赖的代码、使用的二进制文件、使用的工具以及其他组件。 这可能包括：

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK 和运行时](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet 包](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>管理依赖项

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet 已弃用且有漏洞的依赖项

**📦 包使用者 | 📦🖊 包作者**

可以使用 [dotnet CLI](/dotnet/core/tools/dotnet-list-package) 列出项目或解决方案中的任何已知的已弃用或有漏洞的依赖项。 可以使用命令 `dotnet list package --deprecated` 或 `dotnet list package --vulnerable` 获得任何已知的弃用功能或漏洞的列表。

### <a name="github-vulnerable-dependencies"></a>GitHub 有漏洞的依赖项

**📦 包使用者 | 📦🖊 包作者**

如果项目托管在 GitHub 上，则可以利用 [GitHub 安全性](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors)在项目中查找安全漏洞和错误，Dependabot 将通过针对你的代码库打开拉取请求来修复它们。 

在引入有漏洞的依赖项之前将其捕获是[“左移”](https://en.wikipedia.org/wiki/Shift-left_testing)的一个目标。 能够获得有关依赖项的信息（例如许可证、过渡性依赖项和依赖项的存在时间）可帮助你做到这一点。

有关 Dependabot 警报和安全更新的详细信息，[请参阅以下文档](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。

### <a name="nuget-feeds"></a>NuGet 源

**📦 包使用者**

当使用多个公共和专用 NuGet 数据源的源时，可以从任何源下载包。 若要确保你的生成是可预测和安全的，且不受已知攻击（如[依赖项混淆](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)）的影响，最佳做法是了解包来自哪些特定的源。 可以使用具有上游追溯功能的单个源或专用源来提供保护。

若要详细了解如何保护包源，请参阅[使用专用包源时降低风险的 3 种方法](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)。

### <a name="client-trust-policies"></a>客户端信任策略

**📦 包使用者**

你可以选择采用某些策略，以要求签署你所使用的包。 这样，只要包具有作者签名，你就可以信任包作者，或者如果包由 NuGet.org 进行存储库签名的特定用户或帐户拥有，就可以信任该包。

若要配置客户端信任策略，[请参阅以下文档](../consume-packages/installing-signed-packages.md)。

### <a name="lock-files"></a>锁定文件

**📦 包使用者**

锁定文件存储包内容的哈希。 如果要安装的包的内容哈希与锁定文件匹配，则将确保包的可重复性。

若要启用锁定文件，[请参阅以下文档](../consume-packages/package-references-in-project-files.md#locking-dependencies)。

## <a name="monitor-your-supply-chain"></a>监视供应链

### <a name="github-secret-scanning"></a>GitHub 机密扫描

**📦🖊 包作者**

GitHub 会扫描 NuGet API 密钥的存储库，以防止欺诈性地使用意外提交的机密。 

若要详细了解密钥扫描，请参阅[关于密钥扫描](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)。

### <a name="author-package-signing"></a>作者包签名

**📦🖊 包作者**

[作者签名](../reference/signed-packages-reference.md)允许包作者在包上加盖标识，方便使用者认出这是你创作的包。 这可以保护内容不被篡改，并充当确定包来源和包真伪的唯一真实源。 与客户端信任策略结合使用时，可以验证包是否来自特定的作者。

要创作包签名，请参阅[对包进行签名](../create-packages/sign-a-package.md)。

### <a name="two-factor-authentication-2fa"></a>双因素身份验证 (2FA)

**📦🖊 包作者**

启用双因素身份验证 (2FA) 在[登录到 GitHub 帐户](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)或 [NuGet.org 公共包存储库](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)时，可以增加额外的安全层。 建议启用双因素身份验证来保护帐户。

### <a name="package-id-prefix-reservation"></a>包 ID 前缀预留 

**📦🖊 包作者**

为了保护包的标识，可以使用各自的命名空间保留与匹配的所有者关联的包 ID 前缀，前提是包 ID 前缀符合[指定标准](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)。 

若要了解有关保留 ID 前缀的信息，请参阅[包 ID 前缀保留](../nuget-org/id-prefix-reservation.md)。

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>弃用和下架有漏洞的包

**📦🖊 包作者**

为了保护 .NET 包生态系统，当你发现自己创作的包中存在漏洞时，请务必将该包弃用并下架，以防用户搜到该包。 如果你正在使用已弃用且下架的包，应避免使用该包。

若要了解如何将包弃用和下架，请参阅以下有关将包[弃用](../nuget-org/deprecate-packages.md)和[下架](../nuget-org/policies/deleting-packages.md#unlisting-a-package)的文档。

## <a name="summary"></a>总结

软件供应链是进入或影响代码的任何内容。 即使供应链漏洞真实存在且发展迅速，它们仍非常罕见；因此，你可以做的最重要的事情就是通过了解依赖项、管理依赖项和监视供应链来保护供应链 。

你已经了解 NuGet 和 [GitHub](/learn/modules/maintain-secure-repository-github/) 提供的用于更高效查看、管理和监视供应链的各种方法。

有关保护全球软件的详细信息，请参阅 [State of the Octoverse 2020 安全报告](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)。
