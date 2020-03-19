---
title: dotnet tool restore 命令
description: dotnet tool restore 命令在计算机上安装当前目录范围内的 .NET Core 本地工具。
ms.date: 02/14/2020
ms.openlocfilehash: cb46f70afb58e482b6aedfddfbf5f3a0c40674f4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2020
ms.locfileid: "79146432"
---
# <a name="dotnet-tool-restore"></a><span data-ttu-id="ea934-103">dotnet tool restore</span><span class="sxs-lookup"><span data-stu-id="ea934-103">dotnet tool restore</span></span>

<span data-ttu-id="ea934-104">本文适用于： ✔️ .NET Core 3.0 SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="ea934-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="ea934-105">“属性”</span><span class="sxs-lookup"><span data-stu-id="ea934-105">Name</span></span>

<span data-ttu-id="ea934-106">`dotnet tool restore` - 在计算机上安装当前目录范围内的 .NET Core 本地工具。</span><span class="sxs-lookup"><span data-stu-id="ea934-106">`dotnet tool restore` - Installs on your machine the .NET Core local tools that are in scope for the current directory.</span></span>

## <a name="synopsis"></a><span data-ttu-id="ea934-107">摘要</span><span class="sxs-lookup"><span data-stu-id="ea934-107">Synopsis</span></span>

```dotnetcli
dotnet tool restore <PACKAGE_NAME>
    [--configfile] [--add-source] [tool-manifest]
    [--disable-parallel] [--ignore-failed-sources]
    [--no-cache] [-interactive] [-v|--verbosity]

dotnet tool restore <-h|--help>
```

## <a name="description"></a><span data-ttu-id="ea934-108">描述</span><span class="sxs-lookup"><span data-stu-id="ea934-108">Description</span></span>

<span data-ttu-id="ea934-109">`dotnet tool restore` 命令查找当前目录范围内的工具清单文件，并安装其中列出的工具。</span><span class="sxs-lookup"><span data-stu-id="ea934-109">The `dotnet tool restore` command finds the tool manifest file that is in scope for the current directory and installs the tools that are listed in it.</span></span> <span data-ttu-id="ea934-110">有关清单文件的信息，请参阅[安装本地工具](global-tools.md#install-a-local-tool)和[调用本地工具](global-tools.md#invoke-a-local-tool)。</span><span class="sxs-lookup"><span data-stu-id="ea934-110">For information about manifest files, see [Install a local tool](global-tools.md#install-a-local-tool) and [Invoke a local tool](global-tools.md#invoke-a-local-tool).</span></span>

## <a name="arguments"></a><span data-ttu-id="ea934-111">自变量</span><span class="sxs-lookup"><span data-stu-id="ea934-111">Arguments</span></span>

- **`PACKAGE_NAME`**

<span data-ttu-id="ea934-112">包含要安装的 .NET Core 工具的 NuGet 包的名称/ID。</span><span class="sxs-lookup"><span data-stu-id="ea934-112">Name/ID of the NuGet package that contains the .NET Core tool to install.</span></span>

## <a name="options"></a><span data-ttu-id="ea934-113">选项</span><span class="sxs-lookup"><span data-stu-id="ea934-113">Options</span></span>

- **`--configfile <FILE>`**

  <span data-ttu-id="ea934-114">要使用的 NuGet 配置 (nuget.config) 文件。</span><span class="sxs-lookup"><span data-stu-id="ea934-114">The NuGet configuration (*nuget.config*) file to use.</span></span>

- **`--add-source <SOURCE>`**

  <span data-ttu-id="ea934-115">添加安装过程中要使用的其他 NuGet 包源。</span><span class="sxs-lookup"><span data-stu-id="ea934-115">Adds an additional NuGet package source to use during installation.</span></span>

- **`--tool-manifest <PATH>`**

  <span data-ttu-id="ea934-116">清单文件的路径。</span><span class="sxs-lookup"><span data-stu-id="ea934-116">Path to the manifest file.</span></span>

- **`--disable-parallel`**

  <span data-ttu-id="ea934-117">防止并行还原多个项目。</span><span class="sxs-lookup"><span data-stu-id="ea934-117">Prevent restoring multiple projects in parallel.</span></span>

- **`--ignore-failed-sources`**

  <span data-ttu-id="ea934-118">将包源失败视为警告。</span><span class="sxs-lookup"><span data-stu-id="ea934-118">Treat package source failures as warnings.</span></span>

- **`--no-cache`**

  <span data-ttu-id="ea934-119">不要缓存包和 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="ea934-119">Do not cache packages and http requests.</span></span>

- **`--interactive`**

  <span data-ttu-id="ea934-120">允许命令停止并等待用户输入或操作（例如，完成身份验证）。</span><span class="sxs-lookup"><span data-stu-id="ea934-120">Allows the command to stop and wait for user input or action (for example to complete authentication).</span></span>

- **`-h|--help`**

  <span data-ttu-id="ea934-121">打印出有关命令的简短帮助。</span><span class="sxs-lookup"><span data-stu-id="ea934-121">Prints out a short help for the command.</span></span>

- **`-v|--verbosity <LEVEL>`**

  <span data-ttu-id="ea934-122">设置命令的详细级别。</span><span class="sxs-lookup"><span data-stu-id="ea934-122">Sets the verbosity level of the command.</span></span> <span data-ttu-id="ea934-123">允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="ea934-123">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span>

## <a name="example"></a><span data-ttu-id="ea934-124">示例</span><span class="sxs-lookup"><span data-stu-id="ea934-124">Example</span></span>

- **`dotnet tool restore`**

  <span data-ttu-id="ea934-125">还原当前目录的本地工具。</span><span class="sxs-lookup"><span data-stu-id="ea934-125">Restores local tools for the current directory.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea934-126">请参阅</span><span class="sxs-lookup"><span data-stu-id="ea934-126">See also</span></span>

- [<span data-ttu-id="ea934-127">.NET Core 工具</span><span class="sxs-lookup"><span data-stu-id="ea934-127">.NET Core tools</span></span>](global-tools.md)
- [<span data-ttu-id="ea934-128">教程：使用 .NET Core CLI 安装和使用 .NET Core 本地工具</span><span class="sxs-lookup"><span data-stu-id="ea934-128">Tutorial: Install and use a .NET Core local tool using the .NET Core CLI</span></span>](local-tools-how-to-use.md)