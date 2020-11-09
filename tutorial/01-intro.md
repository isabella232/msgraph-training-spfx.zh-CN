---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823304"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="679b1-101">本教程向您介绍如何构建使用 Microsoft Graph API 检索用户的日历信息的 [SharePoint 客户端 web 部件](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) 。</span><span class="sxs-lookup"><span data-stu-id="679b1-101">This tutorial teaches you how to build a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="679b1-102">如果您只想下载已完成的教程，可以下载或克隆 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-spfx)。</span><span class="sxs-lookup"><span data-stu-id="679b1-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="679b1-103">必备条件</span><span class="sxs-lookup"><span data-stu-id="679b1-103">Prerequisites</span></span>

<span data-ttu-id="679b1-104">在开始本教程之前，您应在开发计算机上安装以下工具。</span><span class="sxs-lookup"><span data-stu-id="679b1-104">Before you start this tutorial, you should have the following tools installed on your development machine.</span></span>

- [<span data-ttu-id="679b1-105">Node.js</span><span class="sxs-lookup"><span data-stu-id="679b1-105">Node.js</span></span>](https://nodejs.org/en/download/releases/)
- [<span data-ttu-id="679b1-106">Yeoman</span><span class="sxs-lookup"><span data-stu-id="679b1-106">Yeoman</span></span>](https://yeoman.io/)
- [<span data-ttu-id="679b1-107">Gulp</span><span class="sxs-lookup"><span data-stu-id="679b1-107">Gulp</span></span>](https://gulpjs.com/)
- [<span data-ttu-id="679b1-108">Yeoman SharePoint 生成器</span><span class="sxs-lookup"><span data-stu-id="679b1-108">Yeoman SharePoint generator</span></span>](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

<span data-ttu-id="679b1-109">您可以在 [设置 Sharepoint 框架开发环境](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment)中找到有关 sharepoint 框架开发要求的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="679b1-109">You can find more details about requirements for SharePoint Framework development at [Set up your SharePoint Framework development environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="679b1-110">SharePoint 框架需要 Node.js 版本10。</span><span class="sxs-lookup"><span data-stu-id="679b1-110">SharePoint Framework requires Node.js version 10.x.</span></span> <span data-ttu-id="679b1-111">请务必安装正确的版本。</span><span class="sxs-lookup"><span data-stu-id="679b1-111">Be sure to install the correct version.</span></span>

<span data-ttu-id="679b1-112">此外，还应具有 Microsoft 工作或学校帐户，并访问同一组织中的全局管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="679b1-112">You should also have a Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="679b1-113">如果你没有 Microsoft 帐户，可以 [注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) 以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="679b1-113">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

<span data-ttu-id="679b1-114">您的 Microsoft 365 租户应 [设置为 SharePoint Framework 开发](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)，并在开始本教程之前创建应用程序目录和测试网站。</span><span class="sxs-lookup"><span data-stu-id="679b1-114">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="679b1-115">本教程是使用上述工具的以下版本编写的。</span><span class="sxs-lookup"><span data-stu-id="679b1-115">This tutorial was written with the following versions of the above tools.</span></span> <span data-ttu-id="679b1-116">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="679b1-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="679b1-117">Node.js 10.22。0</span><span class="sxs-lookup"><span data-stu-id="679b1-117">Node.js 10.22.0</span></span>
> - <span data-ttu-id="679b1-118">Yeoman 3.1。1</span><span class="sxs-lookup"><span data-stu-id="679b1-118">Yeoman 3.1.1</span></span>
> - <span data-ttu-id="679b1-119">Gulp 4.0。2</span><span class="sxs-lookup"><span data-stu-id="679b1-119">Gulp 4.0.2</span></span>
> - <span data-ttu-id="679b1-120">Yeoman SharePoint 生成器1.11。0</span><span class="sxs-lookup"><span data-stu-id="679b1-120">Yeoman SharePoint generator 1.11.0</span></span>

## <a name="feedback"></a><span data-ttu-id="679b1-121">反馈</span><span class="sxs-lookup"><span data-stu-id="679b1-121">Feedback</span></span>

<span data-ttu-id="679b1-122">请在 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-spfx)中提供有关本教程的任何反馈。</span><span class="sxs-lookup"><span data-stu-id="679b1-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>
