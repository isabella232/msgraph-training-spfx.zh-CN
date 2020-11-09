---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823300"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="77ac7-101">在本教程中，你将创建一个 [SharePoint 客户端 web 部件，该 web 部件](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) 将使用 Microsoft Graph 获取当前周的用户日历，并允许用户向其日历中添加事件。</span><span class="sxs-lookup"><span data-stu-id="77ac7-101">In this tutorial, you'll create a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that will use Microsoft Graph to get the user's calendar for the current week and allow the user to add an event to their calendar.</span></span>

## <a name="create-a-web-part-project"></a><span data-ttu-id="77ac7-102">创建 web 部件项目</span><span class="sxs-lookup"><span data-stu-id="77ac7-102">Create a web part project</span></span>

1. <span data-ttu-id="77ac7-103">在要创建项目的空目录中打开命令行界面 (CLI) 。</span><span class="sxs-lookup"><span data-stu-id="77ac7-103">Open your command-line interface (CLI) in an empty directory where you want to create the project.</span></span> <span data-ttu-id="77ac7-104">运行以下命令以启动 Yeoman SharePoint 生成器。</span><span class="sxs-lookup"><span data-stu-id="77ac7-104">Run the following command to start the Yeoman SharePoint generator.</span></span>

    ```Shell
    yo @microsoft/sharepoint
    ```

1. <span data-ttu-id="77ac7-105">按如下所示响应提示。</span><span class="sxs-lookup"><span data-stu-id="77ac7-105">Respond to the prompts as follows.</span></span>

    - <span data-ttu-id="77ac7-106">**您的解决方案名称是什么？**</span><span class="sxs-lookup"><span data-stu-id="77ac7-106">**What is your solution name?**</span></span> `graph-tutorial`
    - <span data-ttu-id="77ac7-107">**你想要为你的组件设定哪些基准包？**</span><span class="sxs-lookup"><span data-stu-id="77ac7-107">**Which baseline packages do you want to target for your component(s)?**</span></span> `SharePoint Online only (latest)`
    - <span data-ttu-id="77ac7-108">**要将文件存放在哪里?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-108">**Where do you want to place the files?**</span></span> `Use the current folder`
    - <span data-ttu-id="77ac7-109">**是否要允许租户管理员选择能够立即将解决方案部署到所有站点的选项，而无需运行任何站点中的部署或添加应用程序功能?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-109">**Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**</span></span> `Yes`
    - <span data-ttu-id="77ac7-110">**解决方案中的组件是否需要权限来访问唯一且不与十个 ant 中的其他组件共享的 web Api？**</span><span class="sxs-lookup"><span data-stu-id="77ac7-110">**Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the ten ant?**</span></span> `No`
    - <span data-ttu-id="77ac7-111">**要创建哪种类型的客户端组件?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-111">**Which type of client-side component to create?**</span></span> `WebPart`
    - <span data-ttu-id="77ac7-112">**Web 部件名称是什么?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-112">**What is your Web part name?**</span></span> `GraphTutorial`
    - <span data-ttu-id="77ac7-113">**Web 部件说明是什么?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-113">**What is your Web part description?**</span></span> `GraphTutorial description`
    - <span data-ttu-id="77ac7-114">**要使用哪种框架?**</span><span class="sxs-lookup"><span data-stu-id="77ac7-114">**Which framework would you like to use?**</span></span> `No JavaScript framework`

1. <span data-ttu-id="77ac7-115">运行以下命令以将项目中的 TypeScript 版本更新为3.7。</span><span class="sxs-lookup"><span data-stu-id="77ac7-115">Run the following command to update the TypeScript version in the project to 3.7.</span></span>

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. <span data-ttu-id="77ac7-116">打开 **。/tsconfig.js** ，并将替换 `rush-stack-compiler-3.3` 为 `rush-stack-compiler-3.7` 。</span><span class="sxs-lookup"><span data-stu-id="77ac7-116">Open **./tsconfig.json** and replace `rush-stack-compiler-3.3` with `rush-stack-compiler-3.7`.</span></span>

1. <span data-ttu-id="77ac7-117">打开 **。/tslint.js** 并删除 `"no-use-before-declare": true,` 该行。</span><span class="sxs-lookup"><span data-stu-id="77ac7-117">Open **./tslint.json** and remove the `"no-use-before-declare": true,` line.</span></span> <span data-ttu-id="77ac7-118">该 `no-use-before-declare` 规则已弃用，并将在生成过程中导致错误。</span><span class="sxs-lookup"><span data-stu-id="77ac7-118">The `no-use-before-declare` rule is deprecated and will cause an error during the build process.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="77ac7-119">安装依赖项</span><span class="sxs-lookup"><span data-stu-id="77ac7-119">Install dependencies</span></span>

<span data-ttu-id="77ac7-120">在继续之前，请安装稍后将使用的一些其他 NPM 包。</span><span class="sxs-lookup"><span data-stu-id="77ac7-120">Before moving on, install some additional NPM packages that you will use later.</span></span>

- <span data-ttu-id="77ac7-121">[Microsoft Graph TypeScript 定义](https://github.com/microsoftgraph/msgraph-typescript-typings) ，以提供 microsoft graph 对象的智能感知。</span><span class="sxs-lookup"><span data-stu-id="77ac7-121">[Microsoft Graph TypeScript definitions](https://github.com/microsoftgraph/msgraph-typescript-typings) to provide Intellisense for Microsoft Graph objects.</span></span>
- <span data-ttu-id="77ac7-122">[Microsoft Graph 工具包](https://docs.microsoft.com/graph/toolkit/overview) ，以提供 web 部件的 UI 组件。</span><span class="sxs-lookup"><span data-stu-id="77ac7-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to provide UI components for the web part.</span></span>
- <span data-ttu-id="77ac7-123">[日期-fns](https://date-fns.org/) 用于处理日期的有用功能。</span><span class="sxs-lookup"><span data-stu-id="77ac7-123">[date-fns](https://date-fns.org/) for helpful functions for working with dates.</span></span>

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
