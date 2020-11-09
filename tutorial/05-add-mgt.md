---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823314"
---
<!-- markdownlint-disable MD002 MD041 -->

在本节中，您将使用 [Microsoft Graph 工具包](https://docs.microsoft.com/graph/toolkit/overview) 将事件的简单列表替换为丰富的 UI。

该工具包提供了一个 [议程组件](https://docs.microsoft.com/graph/toolkit/components/agenda)，它非常适合呈现我们的事件列表。

## <a name="update-the-web-part"></a>更新 web 部件

1. 打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss** 。 将 `background-color` 条目中属性的值更改 `.row` 为 `$ms-color-white` 。

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. 在条目中添加以下条目 `.graphTutorial` 。

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. 打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** 并将以下语句添加到 `import` 文件顶部。

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. 将以下函数添加到 **GraphTutorialWebPart** 类以初始化工具包。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. 将现有的 `renderCalendarView` 函数替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    这会将基本列表替换为工具包中的 " **议程** " 组件。

1. 生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。

    ![带有 "议程" 组件的 web 部件的屏幕截图](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a>另一种方法

在这种情况下，您可以使用以下代码：

- 使用 **MSGraphClient** 从 Microsoft Graph 中获取当前周的用户的日历视图。
- 将这些事件添加到 Microsoft Graph 工具包中的 " **议程** " 组件。

通过此方法，您可以完全控制 Graph API 调用，并且可以在呈现所需的事件之前对其进行任何处理。 但是，如果不需要这样做，可以通过让 " **议程** " 组件为您完成工作来简化。

所有 Microsoft Graph 工具包组件都能够将所有相关的 API 调用都建立到 Microsoft Graph 中。 例如，只需将 " **议程** " 组件添加到 web 部件，而不设置任何属性，web 部件就会使用其默认设置获取当天的事件。 让我们来看看我们如何可以获得当前周) 的 (事件的相同结果。

1. 将现有 `render` 的方法替换为以下项。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    现在， `render` 您只需在 HTML 中直接添加一个元素，而不是在中进行 API 调用 `mgt-agenda` 。 通过设置 `date` 为一周的开始和 `days` 7，组件将进行相同的 API 调用，这是以前版本的 `render` 。

1. 将以下空函数添加到 **GraphTutorialWebPart** 类中。

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > 我们还向 web 部件添加了 " **添加团队社会性** " 按钮，并将该 `addSocialToCalendar` 方法添加为事件侦听器。  您将在下一节中实现后面的代码。 现在，我们只需要编译代码。

1. 生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。 视图应与上一次测试相同。

### <a name="using-the-toolkit-vs-making-api-calls"></a>使用工具包和进行 API 调用

此时，当工具包为您完成工作时，您可能想知道为什么您在使用 **MSGraphClient** 时遇到了麻烦。 该工具包旨在呈现从 Microsoft Graph 查询的结果，如事件列表。 但是，在某些情况下，可能需要自己进行 API 调用。

- 不是请求的任何 API 调用 `GET` 。 例如，在日历上创建新事件或更新用户的电话号码。
- API 调用，以获取旨在 "幕后" 使用且不直接呈现的数据。
