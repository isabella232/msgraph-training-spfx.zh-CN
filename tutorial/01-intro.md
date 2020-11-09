---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823304"
---
<!-- markdownlint-disable MD002 MD041 -->

本教程向您介绍如何构建使用 Microsoft Graph API 检索用户的日历信息的 [SharePoint 客户端 web 部件](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) 。

> [!TIP]
> 如果您只想下载已完成的教程，可以下载或克隆 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-spfx)。

## <a name="prerequisites"></a>必备条件

在开始本教程之前，您应在开发计算机上安装以下工具。

- [Node.js](https://nodejs.org/en/download/releases/)
- [Yeoman](https://yeoman.io/)
- [Gulp](https://gulpjs.com/)
- [Yeoman SharePoint 生成器](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

您可以在 [设置 Sharepoint 框架开发环境](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment)中找到有关 sharepoint 框架开发要求的更多详细信息。

> [!IMPORTANT]
> SharePoint 框架需要 Node.js 版本10。 请务必安装正确的版本。

此外，还应具有 Microsoft 工作或学校帐户，并访问同一组织中的全局管理员帐户。 如果你没有 Microsoft 帐户，可以 [注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) 以获取免费的 office 365 订阅。

您的 Microsoft 365 租户应 [设置为 SharePoint Framework 开发](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)，并在开始本教程之前创建应用程序目录和测试网站。

> [!NOTE]
> 本教程是使用上述工具的以下版本编写的。 本指南中的步骤可能适用于其他版本，但尚未经过测试。
>
> - Node.js 10.22。0
> - Yeoman 3.1。1
> - Gulp 4.0。2
> - Yeoman SharePoint 生成器1.11。0

## <a name="feedback"></a>反馈

请在 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-spfx)中提供有关本教程的任何反馈。
