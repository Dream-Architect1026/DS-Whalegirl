# 发布前检查清单 · DS-Whalegirl v0.5.3.0-preview.1

> 逐项核对；未完成项必须标「待办」，不得默认通过。
> 检查时间：2026-11-05（第二版构建） · 检查人：自动化 + 真机冒烟

## A. 脚本头元信息

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| A1 | `@name` | 与稳定版可区分 | `学习通纯免费刷课答题（DS-Whalegirl 预览版）` | 通过 |
| A2 | `@namespace` | 独立命名空间 | `xinghong-preview` | 通过 |
| A3 | `@version` | 次版本号 + `-preview.N` | `0.5.3.0-preview.1` | 通过 |
| A4 | `@description` | 标注 Preview | 含「预览版（Preview）」与隔离说明 | 通过 |
| A5 | `@author` | 与稳定版一致 | `X.H` | 通过 |
| A6 | `@license` | MIT | `MIT` | 通过 |
| A7 | `@homepageURL` / `@supportURL` | 可访问 | `github.com/Dream-Architect1026/DS-Whalegirl`（`/issues`） | 通过 |
| A8 | `@icon` | 保留原图，不破坏 | 第 14 行原始 base64 未改动 | 通过 |

## B. 版本一致性

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| B1 | 脚本 `@version` = `HX_BUILD` | 一致 | 均为 `0.5.3.0-preview.1` | 通过 |
| B2 | README 与本包 CHANGELOG 版本 | 一致 | `0.5.3.0-preview.1` | 通过 |
| B3 | 稳定版链路不受影响 | `check_release` 6/6 | 6/6 通过（主/副本同版本同 SHA256，README/CHANGELOG 首条 = 0.5.2.4） | 通过 |
| B4 | 稳定版文件未改动 | 字节不变 | 未修改 `DS-Whalegirl.user.js` / `D-Whaler.user.js` | 通过 |
| B5 | 语法 | `node --check` 通过 | 通过 | 通过 |
| B6 | 预览版改动标注 | `check_preview` 全过 | 14/14（稳定版零预览标记、差异行均已标注） | 通过 |
| B7 | 能力不缩减 | `check_parity` 缩减 0 | 15 项锚点，缩减 0 | 通过 |

## C. 更新地址

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| C1 | `@downloadURL` / `@updateURL` | 指向预览专用路径 | `@downloadURL` = `...@v0.5.3.0-preview.1/release/preview/DS-Whalegirl-preview.user.js`；`@updateURL` = `...@main/release/preview/DS-Whalegirl-preview.user.js` | 通过 |
| C2 | 地址可达 | HTTP 200 | **tag 地址已实测 200**（证据 `_harness/evidence/preview-http-verify-20261105-tag.json`）；`@main` 亦 200（内容可能滞后） | 通过 |
| C3 | 不与稳定版更新地址混用 | 两条地址互不覆盖 | 稳定版仍为 `.../main/DS-Whalegirl.user.js` | 通过 |
| C4 | 远端内容与本包一致 | SHA256 相同 | tag 地址：719329B / `a85db170…` = 本地一致（tag 为新建 ref，无分支缓存） | 通过 |

## D. 许可

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| D1 | `LICENSE` 文件随包 | 存在且为 MIT | MIT 全文 | 通过 |
| D2 | 脚本头 `@license` 与包内 LICENSE 一致 | MIT | MIT / MIT | 通过 |

## E. 试用与回退说明

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| E1 | 安装说明 | 先停稳定版，再装预览 | README「三步操作」第 1 步 | 通过 |
| E2 | 试用识别 | 给出可核对版本号与指纹 | `__HX_BUILD__=0.5.3.0-preview.1` + `__HX_PREVIEW__()` 三元组 | 通过 |
| E3 | 回退说明 | 可操作、不丢进度 | README 第 3 步 + CHANGELOG「回退方式」 | 通过 |
| E4 | 双注入风险提示 | 明确写出 | README「已知问题」第 1 条 | 通过 |
| E5 | 真机冒烟 | S0 / S1(30s) / 倍速 | S0 3.63s、S1 2.19s、倍速约 6s 恢复（全通过） | 通过 |
| E6 | 回退实测 | 稳定版可继续播放 | `0.5.2.4`，视频播放中；预览版停用、稳定版启用 | 通过 |

## F. 截图（本轮为真实截图，非占位）

| # | 项目 | 期望 | 实测 | 状态 |
|---|---|---|---|---|
| F1 | 面板运行截图 | 真机面板可见 | `assets/preview-panel.jpg`（1400 宽，脚本面板与课程页同框） | 通过 |
| F2 | 版本号截图 | 显示 `0.5.3.0-preview.1` | `assets/preview-version.jpg`（ScriptCat 已安装列表，预览版启用中） | 通过 |

## 结论

- 阻塞项：无。安装地址已固定到 tag `v0.5.3.0-preview.1`，GET 200 且 SHA256 与本包一致，**首次安装无需等分支缓存**。
- 剩余滞后：`@updateURL` 走 `@main`，新版本被发现最多需 12h（`s-maxage=43200`）；这是自动更新的固有机制，不影响已下载内容的正确性。
- 稳定版发布链路零改动，可安全并行发布预览版。
