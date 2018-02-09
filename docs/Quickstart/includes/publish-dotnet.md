1. 更改到包含 `.nupkg` 文件的文件夹。

1. 运行以下命令，指定包名称并使用你的 API 密钥替换密钥值：

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet 会显示发布过程的结果：

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

请参阅 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。