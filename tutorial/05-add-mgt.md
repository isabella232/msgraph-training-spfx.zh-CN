---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823314"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="223ab-101">在本节中，您将使用 [Microsoft Graph 工具包](https://docs.microsoft.com/graph/toolkit/overview) 将事件的简单列表替换为丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="223ab-101">In this section, you'll use the [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to replace the simple list of events with rich UI.</span></span>

<span data-ttu-id="223ab-102">该工具包提供了一个 [议程组件](https://docs.microsoft.com/graph/toolkit/components/agenda)，它非常适合呈现我们的事件列表。</span><span class="sxs-lookup"><span data-stu-id="223ab-102">The toolkit provides an [Agenda component](https://docs.microsoft.com/graph/toolkit/components/agenda), which is well-suited to render our list of events.</span></span>

## <a name="update-the-web-part"></a><span data-ttu-id="223ab-103">更新 web 部件</span><span class="sxs-lookup"><span data-stu-id="223ab-103">Update the web part</span></span>

1. <span data-ttu-id="223ab-104">打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss** 。</span><span class="sxs-lookup"><span data-stu-id="223ab-104">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss**.</span></span> <span data-ttu-id="223ab-105">将 `background-color` 条目中属性的值更改 `.row` 为 `$ms-color-white` 。</span><span class="sxs-lookup"><span data-stu-id="223ab-105">Change the value of the `background-color` attribute in the `.row` entry to `$ms-color-white`.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. <span data-ttu-id="223ab-106">在条目中添加以下条目 `.graphTutorial` 。</span><span class="sxs-lookup"><span data-stu-id="223ab-106">Add the following entry inside the `.graphTutorial` entry.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. <span data-ttu-id="223ab-107">打开 **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** 并将以下语句添加到 `import` 文件顶部。</span><span class="sxs-lookup"><span data-stu-id="223ab-107">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. <span data-ttu-id="223ab-108">将以下函数添加到 **GraphTutorialWebPart** 类以初始化工具包。</span><span class="sxs-lookup"><span data-stu-id="223ab-108">Add the following function to the **GraphTutorialWebPart** class to initialize the toolkit.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. <span data-ttu-id="223ab-109">将现有的 `renderCalendarView` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="223ab-109">Replace the existing `renderCalendarView` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    <span data-ttu-id="223ab-110">这会将基本列表替换为工具包中的 " **议程** " 组件。</span><span class="sxs-lookup"><span data-stu-id="223ab-110">This replaces the basic list with the **Agenda** component from the toolkit.</span></span>

1. <span data-ttu-id="223ab-111">生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。</span><span class="sxs-lookup"><span data-stu-id="223ab-111">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

    ![带有 "议程" 组件的 web 部件的屏幕截图](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a><span data-ttu-id="223ab-113">另一种方法</span><span class="sxs-lookup"><span data-stu-id="223ab-113">An alternate approach</span></span>

<span data-ttu-id="223ab-114">在这种情况下，您可以使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="223ab-114">At this point, you have code that:</span></span>

- <span data-ttu-id="223ab-115">使用 **MSGraphClient** 从 Microsoft Graph 中获取当前周的用户的日历视图。</span><span class="sxs-lookup"><span data-stu-id="223ab-115">Uses the **MSGraphClient** to get the user's calendar view for the current week from Microsoft Graph.</span></span>
- <span data-ttu-id="223ab-116">将这些事件添加到 Microsoft Graph 工具包中的 " **议程** " 组件。</span><span class="sxs-lookup"><span data-stu-id="223ab-116">Add those events to the **Agenda** component from the Microsoft Graph Toolkit.</span></span>

<span data-ttu-id="223ab-117">通过此方法，您可以完全控制 Graph API 调用，并且可以在呈现所需的事件之前对其进行任何处理。</span><span class="sxs-lookup"><span data-stu-id="223ab-117">With this approach, you have full control over the Graph API call and can do any processing of the events prior to rendering that you want.</span></span> <span data-ttu-id="223ab-118">但是，如果不需要这样做，可以通过让 " **议程** " 组件为您完成工作来简化。</span><span class="sxs-lookup"><span data-stu-id="223ab-118">However, if that isn't required, you can simplify by letting the **Agenda** component do the work for you.</span></span>

<span data-ttu-id="223ab-119">所有 Microsoft Graph 工具包组件都能够将所有相关的 API 调用都建立到 Microsoft Graph 中。</span><span class="sxs-lookup"><span data-stu-id="223ab-119">All Microsoft Graph Toolkit components are capable of making all of the relevant API calls to the Microsoft Graph.</span></span> <span data-ttu-id="223ab-120">例如，只需将 " **议程** " 组件添加到 web 部件，而不设置任何属性，web 部件就会使用其默认设置获取当天的事件。</span><span class="sxs-lookup"><span data-stu-id="223ab-120">For example, by just adding the **Agenda** component to the web part, and not setting any properties, the web part would use its default settings to get events for the current day.</span></span> <span data-ttu-id="223ab-121">让我们来看看我们如何可以获得当前周) 的 (事件的相同结果。</span><span class="sxs-lookup"><span data-stu-id="223ab-121">Let's look at how we can achieve the same results we currently have (events for the current week).</span></span>

1. <span data-ttu-id="223ab-122">将现有 `render` 的方法替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="223ab-122">Replace the existing `render` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    <span data-ttu-id="223ab-123">现在， `render` 您只需在 HTML 中直接添加一个元素，而不是在中进行 API 调用 `mgt-agenda` 。</span><span class="sxs-lookup"><span data-stu-id="223ab-123">Now, instead of making an API call in `render`, you simply add an `mgt-agenda` element directly into the HTML.</span></span> <span data-ttu-id="223ab-124">通过设置 `date` 为一周的开始和 `days` 7，组件将进行相同的 API 调用，这是以前版本的 `render` 。</span><span class="sxs-lookup"><span data-stu-id="223ab-124">By setting `date` to the start of the week, and `days` to 7, the component will make the same API call the previous version of `render` was making.</span></span>

1. <span data-ttu-id="223ab-125">将以下空函数添加到 **GraphTutorialWebPart** 类中。</span><span class="sxs-lookup"><span data-stu-id="223ab-125">Add the following empty function to the **GraphTutorialWebPart** class.</span></span>

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > <span data-ttu-id="223ab-126">我们还向 web 部件添加了 " **添加团队社会性** " 按钮，并将该 `addSocialToCalendar` 方法添加为事件侦听器。</span><span class="sxs-lookup"><span data-stu-id="223ab-126">We also added an **Add team social** button to the web part, and added the `addSocialToCalendar` method as an event listener.</span></span>  <span data-ttu-id="223ab-127">您将在下一节中实现后面的代码。</span><span class="sxs-lookup"><span data-stu-id="223ab-127">You'll implement the code behind that in the next section.</span></span> <span data-ttu-id="223ab-128">现在，我们只需要编译代码。</span><span class="sxs-lookup"><span data-stu-id="223ab-128">For now, we just want the code to compile.</span></span>

1. <span data-ttu-id="223ab-129">生成、打包并重新上载 web 部件，然后刷新要对其进行测试的页面。</span><span class="sxs-lookup"><span data-stu-id="223ab-129">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span> <span data-ttu-id="223ab-130">视图应与上一次测试相同。</span><span class="sxs-lookup"><span data-stu-id="223ab-130">The view should be the same as your previous test.</span></span>

### <a name="using-the-toolkit-vs-making-api-calls"></a><span data-ttu-id="223ab-131">使用工具包和进行 API 调用</span><span class="sxs-lookup"><span data-stu-id="223ab-131">Using the toolkit vs making API calls</span></span>

<span data-ttu-id="223ab-132">此时，当工具包为您完成工作时，您可能想知道为什么您在使用 **MSGraphClient** 时遇到了麻烦。</span><span class="sxs-lookup"><span data-stu-id="223ab-132">At this point you may be wondering why you went through the trouble of using the **MSGraphClient** at all, when the toolkit does the work for you.</span></span> <span data-ttu-id="223ab-133">该工具包旨在呈现从 Microsoft Graph 查询的结果，如事件列表。</span><span class="sxs-lookup"><span data-stu-id="223ab-133">The toolkit is designed for rendering results that you query from Microsoft Graph, such as a list of events.</span></span> <span data-ttu-id="223ab-134">但是，在某些情况下，可能需要自己进行 API 调用。</span><span class="sxs-lookup"><span data-stu-id="223ab-134">However, there are scenarios where making API calls yourself is necessary.</span></span>

- <span data-ttu-id="223ab-135">不是请求的任何 API 调用 `GET` 。</span><span class="sxs-lookup"><span data-stu-id="223ab-135">Any API calls that are not a `GET` request.</span></span> <span data-ttu-id="223ab-136">例如，在日历上创建新事件或更新用户的电话号码。</span><span class="sxs-lookup"><span data-stu-id="223ab-136">For example, creating a new event on the calendar, or updating a user's phone number.</span></span>
- <span data-ttu-id="223ab-137">API 调用，以获取旨在 "幕后" 使用且不直接呈现的数据。</span><span class="sxs-lookup"><span data-stu-id="223ab-137">API calls to get data that's intended to be used "behind the scenes" and not rendered directly.</span></span>
