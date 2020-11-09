---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831290"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="13691-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="13691-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13691-102">必备条件</span><span class="sxs-lookup"><span data-stu-id="13691-102">Prerequisites</span></span>

<span data-ttu-id="13691-103">若要在此文件夹中运行已完成的项目，您需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="13691-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="13691-104">[Node.js](https://nodejs.org/en/download/releases/) 版本 10. x</span><span class="sxs-lookup"><span data-stu-id="13691-104">[Node.js](https://nodejs.org/en/download/releases/) version 10.x</span></span>
- [<span data-ttu-id="13691-105">Gulp</span><span class="sxs-lookup"><span data-stu-id="13691-105">Gulp</span></span>](https://gulpjs.com/)
- <span data-ttu-id="13691-106">Microsoft 工作或学校帐户，有权访问同一组织中的全局管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="13691-106">A Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="13691-107">如果你没有 Microsoft 帐户，可以 [注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) 以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="13691-107">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>
- <span data-ttu-id="13691-108">您的 Microsoft 365 租户应 [设置为 SharePoint Framework 开发](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)，并在开始本教程之前创建应用程序目录和测试网站。</span><span class="sxs-lookup"><span data-stu-id="13691-108">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

### <a name="deploy-the-web-part"></a><span data-ttu-id="13691-109">部署 web 部件</span><span class="sxs-lookup"><span data-stu-id="13691-109">Deploy the web part</span></span>

1. <span data-ttu-id="13691-110">在 CLI 中运行以下两个命令以生成和打包 web 部件。</span><span class="sxs-lookup"><span data-stu-id="13691-110">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="13691-111">打开浏览器并转到租户的 SharePoint 应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="13691-111">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="13691-112">选择左侧的 " **SharePoint 相关应用程序** " 菜单项。</span><span class="sxs-lookup"><span data-stu-id="13691-112">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="13691-113">上载 **/sharepoint/solution/graph-tutorial.sppkg** 文件。</span><span class="sxs-lookup"><span data-stu-id="13691-113">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="13691-114">在 " **是否信任 ...** " 提示符处，确认该提示是否列出了您在 " **在package-solution.js打开** " 文件中设置的4个 Microsoft Graph 权限。</span><span class="sxs-lookup"><span data-stu-id="13691-114">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="13691-115">选择 **"使此解决方案可用于组织中的所有站点** "，然后选择 " **部署** "。</span><span class="sxs-lookup"><span data-stu-id="13691-115">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="13691-116">使用租户管理员转到 [SharePoint 管理中心](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) 。</span><span class="sxs-lookup"><span data-stu-id="13691-116">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="13691-117">在左侧菜单中，依次选择 " **高级** "、" **API 访问** "。</span><span class="sxs-lookup"><span data-stu-id="13691-117">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="13691-118">从 **图-教程-客户端解决方案** 包中选择每个挂起的请求，然后选择 " **批准** "。</span><span class="sxs-lookup"><span data-stu-id="13691-118">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![SharePoint 管理中心的 API 访问页面的屏幕截图](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="13691-120">测试 web 部件</span><span class="sxs-lookup"><span data-stu-id="13691-120">Test the web part</span></span>

1. <span data-ttu-id="13691-121">转到要在其中测试 web 部件的 SharePoint 网站。</span><span class="sxs-lookup"><span data-stu-id="13691-121">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="13691-122">创建要在上测试 web 部件的新页面。</span><span class="sxs-lookup"><span data-stu-id="13691-122">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="13691-123">使用 web 部件选取器查找 **GraphTutorial** web 部件，并将其添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="13691-123">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Web 部件选取器中的 GraphTutorial web 部件的屏幕截图](../tutorial/images/add-web-part.png)
