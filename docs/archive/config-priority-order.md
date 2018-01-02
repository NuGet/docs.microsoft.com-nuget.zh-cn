### <a name="priority-ordering"></a><span data-ttu-id="206ad-101">优先级排序</span><span class="sxs-lookup"><span data-stu-id="206ad-101">Priority ordering</span></span>

<span data-ttu-id="206ad-102">考虑按“优先级顺序”应用设置也可提供帮助，该顺序实质上与处理顺序相反。</span><span class="sxs-lookup"><span data-stu-id="206ad-102">It can also help to think about the "priority order" in which settings are applied, which is essentially the reverse of the processing order.</span></span> <span data-ttu-id="206ad-103">例如，如果项目位于 `c:\A\B\C` 中，则 NuGet 按照以下优先级顺序应用设置，即优先应用顺序中靠前的设置：</span><span class="sxs-lookup"><span data-stu-id="206ad-103">For example, if a project is located in `c:\A\B\C`, then NuGet applies settings in the following priority order, meaning settings found higher up in the order win:</span></span>

    (For solution-level packages only in NuGet 2.x; ignored in NuGet 3.x)
    c:\A\B\C\.nuget\NuGet.Config

    (For all version of NuGet)
    c:\A\B\C\NuGet.Config
    c:\A\B\NuGet.Config
    c:\A\NuGet.Config
    c:\NuGet.Config

    configFile, if specified

    (Ignored in NuGet 3.4 and later if -configFile is used)
    %AppData%\NuGet\NuGet.Config

    (NuGet 2.6 to 3.5)
    %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramData%\NuGet\Config\NuGet.Config

    (NuGet 4.0+)
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\NuGet.Config