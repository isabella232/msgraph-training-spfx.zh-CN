---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823272"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="7712d-101">在本节中，您将更新 web 部件，以允许用户将事件添加到其日历中的团队每周的社会工时。</span><span class="sxs-lookup"><span data-stu-id="7712d-101">In this section you'll update the web part to allow the user to add an event to their calendar for the team's weekly social hour.</span></span> <span data-ttu-id="7712d-102">在这种情况下，团队每周的社会工时在星期五下午4点。</span><span class="sxs-lookup"><span data-stu-id="7712d-102">In this scenario, the team has a weekly social hour at 4 PM on Friday.</span></span>

1. <span data-ttu-id="7712d-103">打开 **/src/webparts/graphTutorial/GraphTutorialWebPart.ts** ，并将现有 `addSocialToCalendar()` 的方法替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="7712d-103">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and replace the existing `addSocialToCalendar()` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    <span data-ttu-id="7712d-104">请考虑此代码执行的操作。</span><span class="sxs-lookup"><span data-stu-id="7712d-104">Consider what this code does.</span></span>

    - <span data-ttu-id="7712d-105">它确定下一个即将开始的周五，并在该日期上构建 4 PM 的 **日期** 。</span><span class="sxs-lookup"><span data-stu-id="7712d-105">It determines the next upcoming Friday and constructs a **Date** for 4 PM on that day.</span></span>
    - <span data-ttu-id="7712d-106">它将构造一个新的 **MicrosoftGraph** 对象，将 start 设置为 **日期** 的值，然后将结束时间设置为一小时后。</span><span class="sxs-lookup"><span data-stu-id="7712d-106">It constructs a new **MicrosoftGraph.Event** object, setting the start to the value of the **Date** , and the end for one hour later.</span></span>
    - <span data-ttu-id="7712d-107">它使用 **MSGraphClient** 将新事件发布到 `/me/events` 终结点。</span><span class="sxs-lookup"><span data-stu-id="7712d-107">It uses the **MSGraphClient** to POST the new event to the `/me/events` endpoint.</span></span>
    - <span data-ttu-id="7712d-108">它将重新呈现 web 部件，以便使用新事件更新视图。</span><span class="sxs-lookup"><span data-stu-id="7712d-108">It re-renders the web part so the view is updated with the new event.</span></span>

1. <span data-ttu-id="7712d-109">生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。</span><span class="sxs-lookup"><span data-stu-id="7712d-109">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

1. <span data-ttu-id="7712d-110">单击 " **添加团队社会性** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="7712d-110">Click the **Add team social** button.</span></span> <span data-ttu-id="7712d-111">页面刷新后，向下滚动到 "星期五" 并找到新事件。</span><span class="sxs-lookup"><span data-stu-id="7712d-111">Once the page refreshes, scroll down to Friday and find the new event.</span></span>

    ![在 web 部件中呈现的新创建事件的屏幕截图](images/new-event.png)
