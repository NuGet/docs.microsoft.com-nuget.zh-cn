1. <span data-ttu-id="1d986-101">更改到包含 `.nupkg` 文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1d986-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="1d986-102">运行以下命令，指定包名称并使用你的 API 密钥替换密钥值：</span><span class="sxs-lookup"><span data-stu-id="1d986-102">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="1d986-103">dotnet 会显示发布过程的结果：</span><span class="sxs-lookup"><span data-stu-id="1d986-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="1d986-104">请参阅 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。</span><span class="sxs-lookup"><span data-stu-id="1d986-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>