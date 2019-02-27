# <a name="licensesnugetorg"></a><span data-ttu-id="bc9f9-101">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="bc9f9-101">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="bc9f9-102">阐释</span><span class="sxs-lookup"><span data-stu-id="bc9f9-102">Rationale</span></span>

<span data-ttu-id="bc9f9-103">通过引入[许可证表达式](nuspec.md#license)要求出现了用来将提供单个许可证标识符、 异常标识符或许可证表达式引用文本的可靠服务。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-103">With the introduction of the [license expressions](nuspec.md#license) a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="bc9f9-104">此服务的一个额外的要求是具有稳定的 URL 架构，不是易受链接 rot，以便我们可以安全地用于较旧的客户端提供向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-104">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="bc9f9-105">Licenses.nuget.org 可满足该角色。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-105">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="bc9f9-106">Nuget.org 使用它来为包指定其许可证的使用许可证表达式提供许可证文本引用。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-106">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="bc9f9-107">`nuget pack` 或与其他包装[客户端工具](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)设置[ `licenseUrl` ](nuspec.md#licenseurl)元素以指向 licenses.nuget.org 以提供向后兼容性与旧版客户端不支持的`license`元素。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-107">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="bc9f9-108">协议</span><span class="sxs-lookup"><span data-stu-id="bc9f9-108">Protocol</span></span>

<span data-ttu-id="bc9f9-109">Licenses.nuget.org 用于查看他们的浏览器中的人员，提供没有机器可读的响应。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-109">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="bc9f9-110">必须使用 HTTPS 协议，并且请求要求以特定方式构造。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-110">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="bc9f9-111">它仅支持`GET`请求。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-111">It only supports `GET` requests.</span></span>
<span data-ttu-id="bc9f9-112">它接受许可证表达式或许可证异常标识符作为输入下面指定的方式。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-112">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="bc9f9-113">请注意，许可证表达式的所有元素都均区分大小写，因此所有输入 licenses.nuget.org 都也区分大小写。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-113">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="bc9f9-114">许可证表达式</span><span class="sxs-lookup"><span data-stu-id="bc9f9-114">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="bc9f9-115">请求</span><span class="sxs-lookup"><span data-stu-id="bc9f9-115">Request</span></span>

<span data-ttu-id="bc9f9-116">许可证 （包括普通的情况下，当表达式包含的单个许可证） 的表达式必须为[URL 编码](https://tools.ietf.org/html/rfc3986#section-2.1)，用作对 licenses.nuget.org 的请求中的路径。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-116">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="bc9f9-117">许可证表达式</span><span class="sxs-lookup"><span data-stu-id="bc9f9-117">License expression</span></span> | <span data-ttu-id="bc9f9-118">若要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="bc9f9-118">URL to use</span></span> |
|:---|:---|
<span data-ttu-id="bc9f9-119">MIT</span><span class="sxs-lookup"><span data-stu-id="bc9f9-119">MIT</span></span>                                                | https://licenses.nuget.org/MIT
<span data-ttu-id="bc9f9-120">(MIT)</span><span class="sxs-lookup"><span data-stu-id="bc9f9-120">(MIT)</span></span>                                              | https://licenses.nuget.org/(MIT)
<span data-ttu-id="bc9f9-121">(LGPL 2.0-仅限使用 FLTK 异常或 Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="bc9f9-121">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

<span data-ttu-id="bc9f9-122">该服务仅支持许可证标识符和接受的 nuget.org 的许可证异常标识符。所有许可证表达式包含不受支持的许可证标识符或许可证异常标识符或不符合许可证表达式语法将被都视为无效。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-122">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="bc9f9-123">响应</span><span class="sxs-lookup"><span data-stu-id="bc9f9-123">Response</span></span>

<span data-ttu-id="bc9f9-124">Licenses.nuget.org 响应请求包含有效的许可证与 HTTP 200 状态代码和网页包含说明的许可证表达式的表达式：</span><span class="sxs-lookup"><span data-stu-id="bc9f9-124">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>
* <span data-ttu-id="bc9f9-125">如果提供许可证的表达式，包含单个许可证标识符，其中包含该许可证引用文本; 返回 web 页</span><span class="sxs-lookup"><span data-stu-id="bc9f9-125">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="bc9f9-126">如果提供许可证表达式是复合许可证表达式，包含与单个许可证或许可证异常引用的链接许可证表达式返回 web 页。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-126">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="bc9f9-127">包含 HTTP 404 响应中的某个许可证无效表达式结果的任何请求。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-127">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="bc9f9-128">许可证异常</span><span class="sxs-lookup"><span data-stu-id="bc9f9-128">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="bc9f9-129">请求</span><span class="sxs-lookup"><span data-stu-id="bc9f9-129">Request</span></span>

<span data-ttu-id="bc9f9-130">许可证异常标识符必须是 URL 编码并将其用作到 licenses.nuget.org 请求中的路径。仅单个许可证异常标识符可以在单个请求中提供。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-130">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="bc9f9-131">除了许可异常标识符没有其他字符可能在 URL 的路径部分中提供。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-131">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="bc9f9-132">许可证异常标识符</span><span class="sxs-lookup"><span data-stu-id="bc9f9-132">License exception identifier</span></span> | <span data-ttu-id="bc9f9-133">若要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="bc9f9-133">URL to use</span></span> |
|:---|:---|
<span data-ttu-id="bc9f9-134">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="bc9f9-134">FLTK-exception</span></span>            | https://licenses.nuget.org/FLTK-exception
<span data-ttu-id="bc9f9-135">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="bc9f9-135">openvpn-openssl-exception</span></span> | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a><span data-ttu-id="bc9f9-136">响应</span><span class="sxs-lookup"><span data-stu-id="bc9f9-136">Response</span></span>

<span data-ttu-id="bc9f9-137">Licenses.nuget.org 响应 HTTP 200 响应进行回应包含指定的许可证异常的引用文本的网页的已知的许可证异常标识符的请求。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-137">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="bc9f9-138">包含不受支持的许可证异常标识符的任何请求会导致 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="bc9f9-138">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>