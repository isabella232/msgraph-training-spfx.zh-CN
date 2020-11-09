---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823312"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="25a06-101">SharePoint 框架消除了在 Azure AD 中注册应用程序以获取访问 Microsoft Graph 的访问令牌的需求。</span><span class="sxs-lookup"><span data-stu-id="25a06-101">The SharePoint Framework eliminates the need to register an application in Azure AD for getting access tokens to access Microsoft Graph.</span></span> <span data-ttu-id="25a06-102">它处理登录到 SharePoint 的用户的身份验证，允许 web 部件获取用户令牌。</span><span class="sxs-lookup"><span data-stu-id="25a06-102">It handles the authentication for the user that is logged into SharePoint, allowing your web part to get user tokens.</span></span> <span data-ttu-id="25a06-103">您的 web 部件需要指明它所需的 [图表权限范围](https://docs.microsoft.com/graph/permissions-reference) ，并且租户管理员可以在安装过程中批准这些权限。</span><span class="sxs-lookup"><span data-stu-id="25a06-103">Your web part needs to indicate which [Graph permission scopes](https://docs.microsoft.com/graph/permissions-reference) it requires, and a tenant admin can approve those permissions during installation.</span></span>

## <a name="configure-permissions"></a><span data-ttu-id="25a06-104">配置权限</span><span class="sxs-lookup"><span data-stu-id="25a06-104">Configure permissions</span></span>

1. <span data-ttu-id="25a06-105">打开 **./config/package-solution.js** 。</span><span class="sxs-lookup"><span data-stu-id="25a06-105">Open **./config/package-solution.json**.</span></span>

1. <span data-ttu-id="25a06-106">将以下代码添加到该 `solution` 属性中。</span><span class="sxs-lookup"><span data-stu-id="25a06-106">Add the following code to the `solution` property.</span></span>

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

<span data-ttu-id="25a06-107">此 `Calendars.ReadWrite` 权限允许 web 部件检索用户的日历并使用 Microsoft Graph 添加事件。</span><span class="sxs-lookup"><span data-stu-id="25a06-107">The `Calendars.ReadWrite` permission allows your web part to retrieve the user's calendar and add events using Microsoft Graph.</span></span> <span data-ttu-id="25a06-108">Microsoft Graph 工具包中的组件使用其他权限来呈现有关事件与会者和组织者的信息。</span><span class="sxs-lookup"><span data-stu-id="25a06-108">The other permissions are used by components in the Microsoft Graph Toolkit to render information about event attendees and organizers.</span></span>

## <a name="optional-test-token-acquisition"></a><span data-ttu-id="25a06-109">可选：测试令牌获取</span><span class="sxs-lookup"><span data-stu-id="25a06-109">Optional: Test token acquisition</span></span>

> [!NOTE]
> <span data-ttu-id="25a06-110">此页面上的其余步骤是可选的。</span><span class="sxs-lookup"><span data-stu-id="25a06-110">The rest of the steps on this page are optional.</span></span> <span data-ttu-id="25a06-111">如果你希望立即获取 Microsoft Graph 编码，可以继续 [获取日历视图](/graph/tutorials/spfx?tutorial-step=3)。</span><span class="sxs-lookup"><span data-stu-id="25a06-111">If you'd prefer to get to the Microsoft Graph coding right away, you can proceed to [Get a calendar view](/graph/tutorials/spfx?tutorial-step=3).</span></span>

<span data-ttu-id="25a06-112">让我们将一些临时代码添加到 web 部件以测试令牌获取。</span><span class="sxs-lookup"><span data-stu-id="25a06-112">Let's add some temporary code to the web part to test token acquisition.</span></span>

1. <span data-ttu-id="25a06-113">打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** 并将以下语句添加到 `import` 文件顶部。</span><span class="sxs-lookup"><span data-stu-id="25a06-113">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. <span data-ttu-id="25a06-114">将现有的 `render` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="25a06-114">Replace the existing `render` function with the following.</span></span>

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a><span data-ttu-id="25a06-115">部署 web 部件</span><span class="sxs-lookup"><span data-stu-id="25a06-115">Deploy the web part</span></span>

1. <span data-ttu-id="25a06-116">在 CLI 中运行以下两个命令以生成和打包 web 部件。</span><span class="sxs-lookup"><span data-stu-id="25a06-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="25a06-117">打开浏览器并转到租户的 SharePoint 应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="25a06-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="25a06-118">选择左侧的 " **SharePoint 相关应用程序** " 菜单项。</span><span class="sxs-lookup"><span data-stu-id="25a06-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="25a06-119">上载 **/sharepoint/solution/graph-tutorial.sppkg** 文件。</span><span class="sxs-lookup"><span data-stu-id="25a06-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="25a06-120">在 " **是否信任 ...** " 提示符处，确认该提示是否列出了您在 " **在package-solution.js打开** " 文件中设置的4个 Microsoft Graph 权限。</span><span class="sxs-lookup"><span data-stu-id="25a06-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="25a06-121">选择 **"使此解决方案可用于组织中的所有站点** "，然后选择 " **部署** "。</span><span class="sxs-lookup"><span data-stu-id="25a06-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="25a06-122">使用租户管理员转到 [SharePoint 管理中心](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) 。</span><span class="sxs-lookup"><span data-stu-id="25a06-122">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="25a06-123">在左侧菜单中，依次选择 " **高级** "、" **API 访问** "。</span><span class="sxs-lookup"><span data-stu-id="25a06-123">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="25a06-124">从 **图-教程-客户端解决方案** 包中选择每个挂起的请求，然后选择 " **批准** "。</span><span class="sxs-lookup"><span data-stu-id="25a06-124">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![SharePoint 管理中心的 API 访问页面的屏幕截图](images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="25a06-126">测试 web 部件</span><span class="sxs-lookup"><span data-stu-id="25a06-126">Test the web part</span></span>

1. <span data-ttu-id="25a06-127">转到要在其中测试 web 部件的 SharePoint 网站。</span><span class="sxs-lookup"><span data-stu-id="25a06-127">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="25a06-128">创建要在上测试 web 部件的新页面。</span><span class="sxs-lookup"><span data-stu-id="25a06-128">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="25a06-129">使用 web 部件选取器查找 **GraphTutorial** web 部件，并将其添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="25a06-129">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Web 部件选取器中的 GraphTutorial web 部件的屏幕截图](images/add-web-part.png)

1. <span data-ttu-id="25a06-131">访问令牌打印在 **欢迎使用 SharePoint** 的下方！</span><span class="sxs-lookup"><span data-stu-id="25a06-131">The access token is printed below the **Welcome to SharePoint!**</span></span> <span data-ttu-id="25a06-132">web 部件中的邮件。</span><span class="sxs-lookup"><span data-stu-id="25a06-132">message in the web part.</span></span> <span data-ttu-id="25a06-133">您可以复制此令牌并 [https://jwt.ms/](https://jwt.ms/) 对其进行分析以确认它包含 web 部件所需的权限范围。</span><span class="sxs-lookup"><span data-stu-id="25a06-133">You can copy this token and parse it at [https://jwt.ms/](https://jwt.ms/) to confirm that it contains the permission scopes required by the web part.</span></span>

    ![显示访问令牌的 web 部件的屏幕截图](images/access-token.png)
