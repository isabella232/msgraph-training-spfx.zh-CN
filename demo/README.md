---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831290"
---
# <a name="how-to-run-the-completed-project"></a>如何运行已完成的项目

## <a name="prerequisites"></a>必备条件

若要在此文件夹中运行已完成的项目，您需要以下各项：

- [Node.js](https://nodejs.org/en/download/releases/) 版本 10. x
- [Gulp](https://gulpjs.com/)
- Microsoft 工作或学校帐户，有权访问同一组织中的全局管理员帐户。 如果你没有 Microsoft 帐户，可以 [注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) 以获取免费的 office 365 订阅。
- 您的 Microsoft 365 租户应 [设置为 SharePoint Framework 开发](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)，并在开始本教程之前创建应用程序目录和测试网站。

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

    ![SharePoint 管理中心的 API 访问页面的屏幕截图](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a>测试 web 部件

1. 转到要在其中测试 web 部件的 SharePoint 网站。 创建要在上测试 web 部件的新页面。

1. 使用 web 部件选取器查找 **GraphTutorial** web 部件，并将其添加到页面中。

    ![Web 部件选取器中的 GraphTutorial web 部件的屏幕截图](../tutorial/images/add-web-part.png)
