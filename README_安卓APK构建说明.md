# 好好记账 Android APK 构建包

这是将现有“好好记账”网页应用封装为 Android 应用的源项目。页面文件打包在 APK 内，打开和记账不需要网络；记录保存于本应用 WebView 的本地存储，不会自动上传账目。

**注意：本压缩包是可构建 APK 的源项目，不是已经编译好的 APK。** 当前制作环境没有 Android SDK/Gradle 构建环境，无法在此处直接产出并验证 APK。项目内提供 GitHub Actions 自动构建配置，照步骤上传后可自动构建安装包。

## 推荐方法：用 GitHub 自动构建（不用在电脑上安装 Android Studio）

需要你操作一次电脑；安装到手机后，日常记账只需用手机。

1. 下载 ZIP 并在电脑上解压。解压后会有 `app`、`.github`、`build.gradle`、`settings.gradle` 等文件。
2. 登录 GitHub，新建一个**Private（私有）**仓库，例如 `haohao-ledger-android`。仓库里不要放任何个人账目或备份文件；这个项目本身不含你的账目。
3. 在电脑安装 GitHub Desktop，并登录同一个 GitHub 账号；在 GitHub Desktop 中克隆刚建的空仓库到电脑。
4. 把解压后的项目**所有内容**复制到克隆出来的仓库目录，注意 `.github/workflows/build-apk.yml` 也必须复制进去。不要只把 ZIP 文件传进仓库。
5. 在 GitHub Desktop 里填写提交说明（例如“初始上传”），点击 **Commit to main**，再点击 **Push origin**。
6. 打开 GitHub 仓库网页的 **Actions** 页面，等待 `Build HaoHao Ledger APK` 工作流运行完成。第一次如果提示需要启用 Actions，按页面提示启用。若没有自动运行，在工作流页选择 `Build HaoHao Ledger APK` → **Run workflow**。
7. 打开完成的工作流运行记录，在页面下方 **Artifacts** 区域下载 `haohao-ledger-apk`，解压得到 `app-debug.apk`。GitHub 构建产物默认保留 14 天，请及时下载。
8. 把 `app-debug.apk` 传到安卓手机（USB、自己的文件传输方式或私有网盘均可），在手机文件管理器中点开 APK 安装。若系统拦截，只有在你确认 APK 是自己仓库这次工作流生成的前提下，才允许所用文件管理器临时“安装未知应用”；安装完成后可关闭该授权。
9. 安装后打开“好好记账”，先记一笔测试账，测试“账本设置 → 导出备份”和“导入备份”。确认正常后再开始记真实账目。

## 可选方法：电脑本地构建

如果电脑已经安装 Android Studio，可尝试打开此项目并等待 Gradle Sync。使用 JDK 17、Android SDK Platform 35。同步成功后，在 Build 菜单构建 **Build APK(s)**，生成的调试安装包通常位于 `app/build/outputs/apk/debug/app-debug.apk`。

## 隐私和数据注意事项

- APK 不需要账号，也不请求互联网权限；所有应用页面文件打包在 APK 内。
- 账目保存在手机应用本地。不会在手机和电脑之间自动同步。
- **卸载应用会删除应用的本地数据。** 卸载、清理应用数据或换手机前，请先在设置里导出 JSON 备份，并确认备份文件已保存。
- 导出的备份可能包含完整的个人消费信息，请放在自己可控的位置，不要上传到公开仓库。
- 这是调试签名 APK，适合个人侧载体验，不是已经经过应用商店审核的正式发布包。后续更新最好固定应用签名；不要为了更新而直接卸载旧应用，否则本地账目会丢失。
- 目前不自动读取支付宝或微信流水，仍需手动记账。
