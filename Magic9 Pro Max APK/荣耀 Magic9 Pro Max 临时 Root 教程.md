# 荣耀 Magic9 Pro Max 临时 Root 教程

本教程对应已用 ADB 核对的国行荣耀 Magic9 Pro Max。使用 HOneClick 在手机上临时提权，无需解锁 Bootloader 或刷写分区。手机重启后，Root 权限会失效。

| 项目 | 已核对的值 |
| --- | --- |
| 型号 | `WKL-AN20` |
| 系统版本 | `11.0.0.115(SP8C00E115R101P7)` |
| 完整内核 | `6.18.21-android17-5-ge186062ea75f-abogki564062290-4k` |
| HOneClick 配置 | `98260-115` |

## 1. 确认应用已装好

| 应用 | 文件 | 用途 |
| --- | --- | --- |
| Shizuku 13.6.0 | `shizuku-v13.6.0.r1086.2650830c-release.apk` | 通过无线调试提供 ADB 权限 |
| KernelSU 管理器 3.3.1 | `KernelSU_v3.3.1_32680-release.apk` | 查看 Root 状态并管理应用授权 |
| HOneClick 2.0 Beta 6 | `HOneClick-2.0-Beta-6.apk` | 执行临时提权 |

这台手机的三个应用都已经用 ADB 确认安装，可以直接从第 2 步开始。原 APK 也在手机「文件管理 → 本机／内部存储 → Download → Magic9-Root-APK」里。

## 2. 配对并启动 Shizuku

1. 手机连上 Wi-Fi。在「设置 → 关于手机」连续点版本号 7 次即可启用开发人员选项，已经启用的可以直接打开。进入「设置 → 系统和更新 → 开发人员选项」，打开「USB 调试」和「无线调试」。
2. 打开 Shizuku，在「通过无线调试启动」里点「配对」。进入系统的「无线调试」页面，点「使用配对码配对设备」，把显示的配对码填入 Shizuku 通知里的输入框。
3. 回到 Shizuku 点「启动」，等主界面显示服务正在运行。配对通常只需一次，手机重启后需要重新启动服务。

[Shizuku 官方配对图解](https://shizuku.rikka.app/zh-hans/guide/setup/#通过无线调试启动)

## 3. 用 HOneClick 提权

1. 提权前备份重要资料。如果手机后来更新过系统，用 `adb shell uname -r` 重新检查完整内核（在 Mac 的 Platform-Tools 目录里可以用 `./adb shell uname -r`）。如果输出与上表不同，先核对项目的适配说明。
2. 打开 HOneClick，点「01 连接 Shizuku」，在弹出的 Shizuku 授权框中允许。确认它识别出匹配的 `115` 内核配置，保留自动选择的 `98260` 后端。
3. 如果 HOneClick 已识别到安装好的 KernelSU，直接继续。若界面提示缺少管理器，再点「02 安装 KernelSU」。
4. 保持手机亮屏，点「03 开始提权」，等待应用给出结果。若提示需要重启，先重启，再启动 Shizuku 后重试。失败时可以先保存日志，避免反复点击。

[HOneClick 使用说明](https://github.com/superboyyy/HOneClick#使用) · [2.0 Beta 6 发布说明](https://github.com/superboyyy/HOneClick/releases/tag/v2.0-beta6)

## 4. 验证 Root

HOneClick 报告提权成功后，打开 KernelSU 管理器，确认能识别 KernelSU 运行状态，再给确实需要 Root 的应用授权。重启会结束本次提权。已经写入的文件或设置不会因为重启而自动还原。

HOneClick 是实验性工具，项目记录了部分内置组件尚待核验的事项。下面的校验值可以确认手里的 APK 与本次交付文件一致。

```text
6e273ab0e991c4e79bc8b1bbb9b9dd739ccac1a8712a541a214078886b7b790f  shizuku-v13.6.0.r1086.2650830c-release.apk
b4a059ace71de2fa65cc7f12b1c58d55fc23ab25e057ee4230ce779742abe450  KernelSU_v3.3.1_32680-release.apk
bb911536e45c8652c1215a3c0e2813453b728af7f3531fb9ec53fa55c5f4181d  HOneClick-2.0-Beta-6.apk
```

[Shizuku 原版](https://github.com/RikkaApps/Shizuku/releases/tag/v13.6.0) · [KernelSU 管理器原版](https://github.com/tiann/KernelSU/releases/tag/v3.3.1) · [HOneClick 组件来源说明](https://github.com/superboyyy/HOneClick/blob/main/ASSET_PROVENANCE.md)
