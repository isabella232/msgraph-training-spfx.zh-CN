---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823300"
---
<!-- markdownlint-disable MD002 MD041 -->

在本教程中，你将创建一个 [SharePoint 客户端 web 部件，该 web 部件](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) 将使用 Microsoft Graph 获取当前周的用户日历，并允许用户向其日历中添加事件。

## <a name="create-a-web-part-project"></a>创建 web 部件项目

1. 在要创建项目的空目录中打开命令行界面 (CLI) 。 运行以下命令以启动 Yeoman SharePoint 生成器。

    ```Shell
    yo @microsoft/sharepoint
    ```

1. 按如下所示响应提示。

    - **您的解决方案名称是什么？** `graph-tutorial`
    - **你想要为你的组件设定哪些基准包？** `SharePoint Online only (latest)`
    - **要将文件存放在哪里?** `Use the current folder`
    - **是否要允许租户管理员选择能够立即将解决方案部署到所有站点的选项，而无需运行任何站点中的部署或添加应用程序功能?** `Yes`
    - **解决方案中的组件是否需要权限来访问唯一且不与十个 ant 中的其他组件共享的 web Api？** `No`
    - **要创建哪种类型的客户端组件?** `WebPart`
    - **Web 部件名称是什么?** `GraphTutorial`
    - **Web 部件说明是什么?** `GraphTutorial description`
    - **要使用哪种框架?** `No JavaScript framework`

1. 运行以下命令以将项目中的 TypeScript 版本更新为3.7。

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. 打开 **。/tsconfig.js** ，并将替换 `rush-stack-compiler-3.3` 为 `rush-stack-compiler-3.7` 。

1. 打开 **。/tslint.js** 并删除 `"no-use-before-declare": true,` 该行。 该 `no-use-before-declare` 规则已弃用，并将在生成过程中导致错误。

## <a name="install-dependencies"></a>安装依赖项

在继续之前，请安装稍后将使用的一些其他 NPM 包。

- [Microsoft Graph TypeScript 定义](https://github.com/microsoftgraph/msgraph-typescript-typings) ，以提供 microsoft graph 对象的智能感知。
- [Microsoft Graph 工具包](https://docs.microsoft.com/graph/toolkit/overview) ，以提供 web 部件的 UI 组件。
- [日期-fns](https://date-fns.org/) 用于处理日期的有用功能。

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
