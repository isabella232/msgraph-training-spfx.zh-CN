---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823272"
---
<!-- markdownlint-disable MD002 MD041 -->

在本节中，您将更新 web 部件，以允许用户将事件添加到其日历中的团队每周的社会工时。 在这种情况下，团队每周的社会工时在星期五下午4点。

1. 打开 **/src/webparts/graphTutorial/GraphTutorialWebPart.ts** ，并将现有 `addSocialToCalendar()` 的方法替换为以下项。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    请考虑此代码执行的操作。

    - 它确定下一个即将开始的周五，并在该日期上构建 4 PM 的 **日期** 。
    - 它将构造一个新的 **MicrosoftGraph** 对象，将 start 设置为 **日期** 的值，然后将结束时间设置为一小时后。
    - 它使用 **MSGraphClient** 将新事件发布到 `/me/events` 终结点。
    - 它将重新呈现 web 部件，以便使用新事件更新视图。

1. 生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。

1. 单击 " **添加团队社会性** " 按钮。 页面刷新后，向下滚动到 "星期五" 并找到新事件。

    ![在 web 部件中呈现的新创建事件的屏幕截图](images/new-event.png)
