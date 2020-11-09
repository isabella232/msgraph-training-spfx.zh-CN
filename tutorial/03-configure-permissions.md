---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823312"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint 框架消除了在 Azure AD 中注册应用程序以获取访问 Microsoft Graph 的访问令牌的需求。 它处理登录到 SharePoint 的用户的身份验证，允许 web 部件获取用户令牌。 您的 web 部件需要指明它所需的 [图表权限范围](https://docs.microsoft.com/graph/permissions-reference) ，并且租户管理员可以在安装过程中批准这些权限。

## <a name="configure-permissions"></a>配置权限

1. 打开 **./config/package-solution.js** 。

1. 将以下代码添加到该 `solution` 属性中。

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

此 `Calendars.ReadWrite` 权限允许 web 部件检索用户的日历并使用 Microsoft Graph 添加事件。 Microsoft Graph 工具包中的组件使用其他权限来呈现有关事件与会者和组织者的信息。

## <a name="optional-test-token-acquisition"></a>可选：测试令牌获取

> [!NOTE]
> 此页面上的其余步骤是可选的。 如果你希望立即获取 Microsoft Graph 编码，可以继续 [获取日历视图](/graph/tutorials/spfx?tutorial-step=3)。

让我们将一些临时代码添加到 web 部件以测试令牌获取。

1. 打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** 并将以下语句添加到 `import` 文件顶部。

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. 将现有的 `render` 函数替换为以下内容。

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

### <a name="deploy-the-web-part"></a>部署 web 部件

1. 在 CLI 中运行以下两个命令以生成和打包 web 部件。

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. 打开浏览器并转到租户的 SharePoint 应用程序目录。 选择左侧的 " **SharePoint 相关应用程序** " 菜单项。

1. 上载 **/sharepoint/solution/graph-tutorial.sppkg** 文件。

1. 在 " **是否信任 ...** " 提示符处，确认该提示是否列出了您在 " **在package-solution.js打开** " 文件中设置的4个 Microsoft Graph 权限。 选择 **"使此解决方案可用于组织中的所有站点** "，然后选择 " **部署** "。

1. 使用租户管理员转到 [SharePoint 管理中心](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) 。

1. 在左侧菜单中，依次选择 " **高级** "、" **API 访问** "。

1. 从 **图-教程-客户端解决方案** 包中选择每个挂起的请求，然后选择 " **批准** "。

    ![SharePoint 管理中心的 API 访问页面的屏幕截图](images/api-access.png)

### <a name="test-the-web-part"></a>测试 web 部件

1. 转到要在其中测试 web 部件的 SharePoint 网站。 创建要在上测试 web 部件的新页面。

1. 使用 web 部件选取器查找 **GraphTutorial** web 部件，并将其添加到页面中。

    ![Web 部件选取器中的 GraphTutorial web 部件的屏幕截图](images/add-web-part.png)

1. 访问令牌打印在 **欢迎使用 SharePoint** 的下方！ web 部件中的邮件。 您可以复制此令牌并 [https://jwt.ms/](https://jwt.ms/) 对其进行分析以确认它包含 web 部件所需的权限范围。

    ![显示访问令牌的 web 部件的屏幕截图](images/access-token.png)
