---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623015"
---
1. <span data-ttu-id="1b0f0-101">更改到包含 `.nupkg` 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1b0f0-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="1b0f0-102">运行以下命令，指定包名称（唯一包 ID）并使用你的 API 密钥替换密钥值：</span><span class="sxs-lookup"><span data-stu-id="1b0f0-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="1b0f0-103">dotnet 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="1b0f0-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="1b0f0-104">请参阅 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。</span><span class="sxs-lookup"><span data-stu-id="1b0f0-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>