# 发包清单 · DS-Whalegirl v0.5.3.0-preview.1

- 生成时间：2026-11-05（第三版构建：下载地址固定到版本 tag，不等分支缓存）
- 发布通道：预览（Preview），**不替代稳定版**
- 压缩包：`DS-Whalegirl-0.5.3.0-preview.1.zip`
- 稳定版：`DS-Whalegirl.user.js` v0.5.2.4（未改动，见 `check_release` 6/6）

## 1. 文件清单

| # | 文件名 | 字节数 | SHA256 |
|---|---|---|---|
| 1 | `DS-Whalegirl-preview.user.js` | 719329 | `a85db1705dd01f8ead2d682398f9a52f7cc06634f7244f1ea4057e62b5b1c330` |
| 2 | `README.md` | 6915 | `5094d878f8fd93e4b4b80d96cd94507a4e50bf81b8b2d22606d8f3f7563d11a7` |
| 3 | `CHANGELOG.md` | 5208 | `a2592fb173ab4a48a330af1e5f73cb0637fcea38b8d3c76d9dde3af82d4f2d0b` |
| 4 | `PRE-RELEASE-CHECKLIST.md` | 4383 | `56cde1d2651d062e27a25bc60deec62db3f7bc997b80f3649833ef826da21128` |
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
- 自动更新：`@downloadURL` 固定到版本 tag `@v0.5.3.0-preview.1`，**已实测 HTTP 200 且 SHA256 与本包一致**（tag 是新建 ref，无分支缓存，首拉即精确）；`@updateURL` 仍走 `@main`，保证后续版本可被自动更新发现（`@main` 对新版本同样受 ≤12h 缓存影响，但只影响「发现更新」的时点，不影响下载内容的正确性）。详见 `DISTRIBUTION.md`。
