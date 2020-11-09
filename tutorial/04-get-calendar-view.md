---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823308"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint 框架提供了对 Microsoft Graph 进行调用的 [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) 。 此类将包装 [Microsoft Graph JavaScript 客户端库](https://github.com/microsoftgraph/msgraph-sdk-javascript)，并使用当前登录用户对其进行预身份验证。

由于它包装现有的 JavaScript 库，因此其用法相同，并且与 Microsoft Graph TypeScript 定义完全兼容。

## <a name="get-the-users-calendar"></a>获取用户的日历

1. 打开 **/src/webparts/graphTutorial/GraphTutorialWebPart.ts** ，并 `import` 在文件顶部添加以下语句。

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. 将以下函数添加到 **GraphTutorialWebPart** 类以呈现错误。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. 添加以下函数以打印用户日历中的事件。

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. 将现有的 `render` 函数替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    请注意此代码执行的操作。

    - 它用于 `this.context.msGraphClientFactory.getClient` 获取经过身份验证的 **MSGraphClient** 对象。
    - 它调用 `/me/calendarView` 终结点，并将 `startDateTime` 和 `endDateTime` 查询参数设置为当前星期的开始和结束。
    - 它用 `select` 来限制返回的字段，只请求应用程序使用的字段。
    - 它用于 `orderby` 按事件的开始时间对事件进行排序。
    - 它用于将 `top` 结果限制为25个事件。

## <a name="deploy-the-web-part"></a>部署 web 部件

1. 在 CLI 中运行以下两个命令以生成和打包 web 部件。

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. 打开浏览器并转到租户的 SharePoint 应用程序目录。 选择左侧的 " **SharePoint 相关应用程序** " 菜单项。

1. 上载 **/sharepoint/solution/graph-tutorial.sppkg** 文件。

1. 在 " **是否信任 ...** " 提示符处，确认该提示是否列出了您在 " **在package-solution.js打开** " 文件中设置的4个 Microsoft Graph 权限。 选择 **"使此解决方案可用于组织中的所有站点** "，然后选择 " **部署** "。

1. 如果尚未为 web 部件审批关系图权限，请立即执行此操作。

    1. 使用租户管理员转到 [SharePoint 管理中心](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) 。

    1. 在左侧菜单中，依次选择 " **高级** "、" **API 访问** "。

    1. 从 **图-教程-客户端解决方案** 包中选择每个挂起的请求，然后选择 " **批准** "。

        ![SharePoint 管理中心的 API 访问页面的屏幕截图](images/api-access.png)

## <a name="test-the-web-part"></a>测试 web 部件

1. 转到要在其中测试 web 部件的 SharePoint 网站。 创建要在上测试 web 部件的新页面。

1. 使用 web 部件选取器查找 **GraphTutorial** web 部件，并将其添加到页面中。

    ![Web 部件选取器中的 GraphTutorial web 部件的屏幕截图](images/add-web-part.png)

1. 将在 web 部件中打印当前周的事件列表。

    ![显示事件列表的 web 部件的屏幕截图](images/calendar-list.png)
