# 设置

## 同步设置

> **警告；**
>
> 确保Settings/Preferences中的Plugins下启用了Settings Repository插件。`Ctrl+Alt+S`

### 配置设置存储库﻿

1. 在任何托管服务（例如[GitHub](https://github.com/) ）上创建 Git 存储库。

   > **提示；**
   >
   > 如果您选择使用[GitHub](https://github.com/)，我们建议您创建一个对所有人不可见的[私有存储库。](https://help.github.com/en/articles/about-repositories)

2. 在安装了您要共享其设置的 Android Studio 实例的计算机上，选择**File | Manage IDE Settings | Settings Repository**主菜单中的设置存储库。指定您创建的存储库的 URL，然后单击Overwrite Remote。

   确保使用 指定 URL `HTTP`。当前不支持`ssh://`和链接。`git://`

3. 在您希望应用设置的每台计算机上，选择**File | Manage IDE Settings | Settings Repository**主菜单中的设置存储库。指定您创建的存储库的 URL，然后单击Overwrite Local。

   如果您希望存储库保留远程设置和本地设置的组合，您可以单击合并。如果检测到任何冲突，将显示一个对话框，您可以在其中解决这些冲突。

   如果您想用本地设置覆盖远程设置，请单击覆盖远程。

每次执行更新项目或推送操作，或者关闭项目或退出 Android studio 时，您的本地设置将自动与存储库中存储的设置同步。

在第一次同步时，系统会提示您指定用户名和密码。建议使用[访问令牌](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)进行 GitHub 身份验证。如果您想使用用户名和密码而不是访问令牌，或者您的 Git 托管服务提供商不支持它，建议您配置[Git 凭证助手](https://help.github.com/articles/caching-your-github-password-in-git/)。

> [支持macOS 钥匙串](https://support.apple.com/kb/PH20093)，这意味着您可以在所有基于 IntelliJ 平台的产品之间共享您的凭据（如果原始 IDE 与请求者 IDE 不同，则会提示您授予访问权限）。

如果要禁用自动设置同步，请在设置/首选项对话框 ( Ctrl+Alt+S) 中，转到工具 | 设置存储库并禁用自动同步选项。您将能够通过选择VCS |手动更新您的设置。从主菜单同步设置。

### 通过其他只读存储库共享更多设置﻿

除了*Settings Repository*之外，您还可以配置任意数量的附加存储库，其中包含要共享的任何类型的设置，包括实时模板、文件模板、方案、部署选项等。

这些存储库被称为*只读源*，因为它们不能被覆盖或合并，只能用作设置源。

与来自只读源的设置同步的执行方式与*设置存储库*相同。

### 配置只读存储库﻿

1. 在设置/首选项对话框 ( Ctrl+Alt+S) 中，转到工具 | 设置存储库。
2. 单击![添加按钮](settings-images/app.general.add.svg+xml)并添加包含您要共享的设置的 GitHub 存储库的 URL。