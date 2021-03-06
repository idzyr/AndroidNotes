# 概览

**Build** 菜单中的构建选项。

| 菜单项                                       | 说明                                                         |
| :------------------------------------------- | :----------------------------------------------------------- |
| **Make Module**                              | 编译自上次构建以来已修改的所选模块中的所有源文件，以及所选模块以递归方式依赖的所有模块。编译包括相关源文件和所有关联的构建任务。您可以通过在 **Project** 窗口中选择模块名称或模块的某个文件来选择要构建的模块。此命令不会生成 APK。 |
| **Make Project**                             | 生成所有模块。                                               |
| **Clean Project**                            | 删除所有中间/缓存的构建文件。                                |
| **Rebuild Project**                          | 针对所选构建变体运行 **Clean Project** 并生成 APK。          |
| **Build Bundle(s)/APK(s) > Build APK(s)**    | 构建包含当前项目中所有模块的 APK（使用模块的选定变体进行构建）。构建完成后，系统将显示确认通知，提供指向该 APK 文件的链接以及用于在 [APK 分析器](https://developer.android.google.cn/studio/build/apk-analyzer)中分析该文件的链接。如果您选择的构建变体是调试构建类型，则系统会使用调试密钥为该 APK 签名，然后您就可以安装该 APK 了。如果您选择了发布变体，则默认情况下，APK 处于未签名状态，您必须手动[为 APK 签名](https://developer.android.google.cn/studio/publish/app-signing)。 或者，您也可以从菜单栏中依次选择 **Build > Generate Signed Bundle/APK**。Android Studio 会将您构建的 APK 保存在 `project-name/module-name/build/outputs/apk/` 中。 |
| **Build Bundle(s)/APK(s) > Build Bundle(s)** | 构建包含当前项目中所有模块的 [Android App Bundle](https://developer.android.google.cn/guide/app-bundle)（使用模块的选定变体进行构建）。构建完成后，系统将显示确认通知，提供指向该 App Bundle 的链接以及用于在 [APK 分析器](https://developer.android.google.cn/studio/build/apk-analyzer)中分析该 App Bundle 的链接。如果您选择的构建变体是调试构建类型，则系统会使用调试密钥为该 App Bundle 签名，然后您就可以[使用 `bundletool`](https://developer.android.google.cn/studio/command-line/bundletool) 通过该 App Bundle 将应用部署到连接的设备。如果您选择了发布变体，则默认情况下，app bundle 处于未签名状态，您必须使用 [`jarsigner`](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/jarsigner.html) 手动为其签名。 或者，您也可以从菜单栏中依次选择 **Build > Generate Signed Bundle/APK**。Android Studio 会将您构建的 APK 保存在 `project-name/module-name/build/outputs/bundle/` 中。 |
| **Generate Signed Bundle/APK**               | 弹出一个包含向导的对话框，用于设置新的签名配置，以及构建签名的 App Bundle 或 APK。您需要先使用发布密钥为您的应用签名，然后才能将其上传到 Play 管理中心。如需详细了解应用签名，请参阅[为您的应用签名](https://developer.android.google.cn/studio/publish/app-signing)。 |



> **注意**：
>
> **Run** 按钮 ![img](overview-images/toolbar-run.png) 可以在设置了 `testOnly="true"` 的情况下构建 APK，这意味着，只能通过 Android Studio 使用的 `adb` 安装 APK。如需获得无需 adb 即可安装的可调试 APK，请选择您的调试变体，然后依次点击 **Build Bundle(s)/APK(s) > Build APK(s)**。