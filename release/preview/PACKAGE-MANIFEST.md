# 发包清单 · DS-Whalegirl v0.5.3.0-preview.1

- 生成时间：2026-11-05（第二版构建，已回填 HTTP 校验结论）
- 发布通道：预览（Preview），**不替代稳定版**
- 压缩包：`DS-Whalegirl-0.5.3.0-preview.1.zip`
- 稳定版：`DS-Whalegirl.user.js` v0.5.2.4（未改动，见 `check_release` 6/6）

## 1. 文件清单

| # | 文件名 | 字节数 | SHA256 |
|---|---|---|---|
| 1 | `DS-Whalegirl-preview.user.js` | 719315 | `6cbc1d1ac250dee6f5bb052501e265a53142c4a3d29d94a47f525bd343ad8f4e` |
| 2 | `README.md` | 6580 | `08fb0983e206a25c81bd650b12db1e28e018f773f3cf7497494b27eb7e396f3e` |
| 3 | `CHANGELOG.md` | 4061 | `e39a2b8ec65b590d5d33d8d7af716841ad3c6936eb4c0f86d4a68784b272d417` |
| 4 | `PRE-RELEASE-CHECKLIST.md` | 4626 | `89753a3ce6e104dab7537e2e796e4b4f63fa9e414922232da6c6e20b4188fff3` |
| 5 | `LICENSE` | 1059 | `28e76346109b297d34af769b179323ef5b72164bf33b2aab0694b30caf3cd83b` |
| 6 | `assets/preview-panel.jpg` | 147240 | `7973c4790dc723a2880f86e6dc3da3e5f0298f7078d4a7a70669715f57a953f9` |
| 7 | `assets/preview-version.jpg` | 36317 | `d3b8652de099fe5365fd983183696e8c42df44cb68c6a5c4c1f9ae158ba1f56a` |
| 8 | `PACKAGE-MANIFEST.md` | 本文件 | 见 `SHA256SUMS.txt` |

完整校验：`SHA256SUMS.txt`（sha256sum 格式，可在 Linux/macOS 直接 `sha256sum -c`，
Windows 用 `certutil -hashfile <文件> SHA256` 对照）。

## 2. 安装 / 试用 / 回退（三步）

1. **安装**：停用稳定版 → 打开 `DS-Whalegirl-preview.user.js` → 「安装」。独立 `@namespace`，不会覆盖稳定版。
2. **试用**：刷新课程页，面板出现即生效；控制台 `__HX_BUILD__` 应为 `0.5.3.0-preview.1`，
   `__HX_PREVIEW__()` 应为 `{fastStart:true, probeOnce:true, pendingState:false}`。
3. **回退**：停用/删除预览版 → 启用稳定版 → 刷新；`__HX_BUILD__` 回到 `0.5.2.4`，进度不丢。

## 3. 发布前必读

- 逐项核对 `PRE-RELEASE-CHECKLIST.md`；当前无阻塞项。
- 稳定版 `DS-Whalegirl.user.js` 与 `D-Whaler.user.js` 不在本包内，保持原样。
- 本包相对稳定版共 35 行差异：7 行元信息/构建号 + 28 行带「预览版」标记的行为改动
  （首播提速默认开启、attachShadow 探针收敛、pending 状态移除），由 `check_preview` 自动校验。
- 自动更新：`@updateURL` 指向 `release/preview/DS-Whalegirl-preview.user.js`，**已实测 HTTP 200**；固定 commit 地址内容 SHA256 与本包一致，`@main` 受 jsDelivr 12h 分支缓存影响可能短暂返回上一版字节（见 `DISTRIBUTION.md`）。
