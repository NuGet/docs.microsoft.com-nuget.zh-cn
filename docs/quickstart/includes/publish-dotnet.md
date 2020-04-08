---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825311"
---
1. <span data-ttu-id="d0265-101">更改到包含 `.nupkg` 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0265-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="d0265-102">运行以下命令，指定包名称（唯一包 ID）并使用你的 API 密钥替换密钥值：</span><span class="sxs-lookup"><span data-stu-id="d0265-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="d0265-103">dotnet 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="d0265-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="d0265-104">请参阅 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。</span><span class="sxs-lookup"><span data-stu-id="d0265-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>