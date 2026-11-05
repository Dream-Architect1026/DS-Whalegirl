# DS-Whalegirl 预览版 · Preview Build (v0.5.3.0-preview.1)

> 先行预览版：只发布、不替代稳定版。稳定版 `DS-Whalegirl.user.js`（v0.5.2.4）与其发布链路保持不变。
> Preview channel only. The stable build (v0.5.2.4) and its release pipeline are untouched.

---

## 中文

### 1. 这是什么

本包是 DS-Whalegirl 的**先行预览版**，用于在正式发版前提前试用与验证。与稳定版 v0.5.2.4 相比：

- **发布隔离**：`@name` 带「预览版」后缀，`@namespace` 为 `xinghong-preview`，安装后**不会覆盖**已装稳定版。
- **三项预览通道改进**（稳定版未变）：
  1. 首播提速默认开启：切小节/刷新后首播等待 12s → 3s，播放冷却 6s → 2s；慢网 10s 仍无数据会自动回落稳妥节奏。
  2. 旧面板 `attachShadow` 探针只探「可见且可命中」的元素且只探一次，不再给页面稍后填充的挂载根挂空 shadow。
  3. 删除无消费方的 `pendingResume/pending` 状态，后台待恢复仍由回前台立即扫描兜底（行为等价）。
- 新增只读指纹 `__HX_PREVIEW__()`，可核验本版改动是否生效。
- 更新地址：`https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@main/release/preview/DS-Whalegirl-preview.user.js`。

### 2. 三步操作

1. **安装**：先停用稳定版（避免双注入），再打开 `DS-Whalegirl-preview.user.js` → 点击「安装」。
2. **试用**：刷新学习通课程页；面板出现即生效，控制台 `__HX_BUILD__` 应为 `0.5.3.0-preview.1`，
   `__HX_PREVIEW__()` 应返回 `fastStart:true / probeOnce:true / pendingState:false`。
3. **回退**：停用或删除预览版 → 启用稳定版 → 刷新页面；`__HX_BUILD__` 回到 `0.5.2.4`。进度在平台侧，不丢失。

### 3. 关闭首播提速

在脚本执行前设置 `window.__HX_FAST_START__ = false`（或在脚本管理器里加一行前置注入），
即回到稳定版节奏（12s 宽限 / 6s 冷却）；无需卸载预览版。

### 4. 已知问题

- 预览版与稳定版**同时启用会双注入**（面板/日志重复）；试用前必须只保留一个。
- 平台限制倍速：手动改 2x 后被平台复位为 1x 并暂停，脚本会自动以 1x 恢复（真机实测约 6 秒），属平台策略，非本版新增缺陷。
- 极慢网下会看到一次「首播提速…已回落到稳妥节奏」日志，属预期降级。

### 5. 验证记录（真机）

| 场景 | 结果 | 关键数值 |
|---|---|---|
| 构建指纹 | 通过 | `fastStart:true / probeOnce:true / pendingState:false` |
| S0 刷新首播 | 通过 | 3.63s 画面开始前进（上一构建 18.3s） |
| S1 暂停 30 秒后恢复 | 通过 | 恢复耗时 2.19s，进度继续推进 |
| 回退稳定版 | 通过 | build=`0.5.2.4`，视频正常播放；预览版保持停用、稳定版启用 |

证据：`_harness/evidence/preview-round2-20261105.json`、`_harness/evidence/preview-shots-20261105.json`、
`_harness/evidence/preview-round2-panel.png`（真机面板）、`_harness/evidence/preview-round2-version.png`（版本号）。

---

## English

### 1. What this is

This is the **early preview build** of DS-Whalegirl. Compared with stable v0.5.2.4:

- **Isolated identity**: the `@name` carries a Preview suffix, `@namespace` is `xinghong-preview`, so it will **not overwrite** an installed stable build.
- **Three preview-channel improvements** (stable untouched):
  1. Fast first-play is ON by default: first-play grace 12s → 3s, play cooldown 6s → 2s; on slow networks it degrades back to the safe pace after 10s without data.
  2. The legacy-panel `attachShadow` probe now only touches visible, hit-testable bare divs and probes each element once — page mount roots are no longer given an empty shadow root.
  3. The consumer-less `pendingResume/pending` state is removed; background resume is still handled immediately by `hxOnVisible` on return to foreground (behaviour equivalent).
- New read-only fingerprint `__HX_PREVIEW__()` for verifying this build is active.
- **Update URL**: `https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@main/release/preview/DS-Whalegirl-preview.user.js`.

### 2. Three steps

1. **Install**: disable the stable build first (avoid double injection), open `DS-Whalegirl-preview.user.js`, click Install.
2. **Try**: reload the course page. The panel appears; `window.__HX_BUILD__` should be `0.5.3.0-preview.1`
   and `__HX_PREVIEW__()` should return `fastStart:true / probeOnce:true / pendingState:false`.
3. **Rollback**: disable/remove the preview, re-enable the stable build, reload. `__HX_BUILD__` returns to `0.5.2.4`; course progress is server-side and is not lost.

### 3. Turning fast first-play off

Set `window.__HX_FAST_START__ = false` before the script runs; the 12s/6s safe pace is restored without uninstalling the preview.

### 4. Known issues

- Enabling preview and stable together causes double injection; keep exactly one enabled.
- Platform rate limiting: setting 2x is reset to 1x with a pause; the script resumes at 1x automatically (≈6 s on real device). Platform policy, not a regression.
- On very slow networks a single “fast start degraded to safe pace” log is expected.

### 5. Real-device verification

| Scenario | Result | Key numbers |
|---|---|---|
| Build fingerprint | PASS | `fastStart:true / probeOnce:true / pendingState:false` |
| S0 first play after refresh | PASS | 3.63 s until playback advanced (previous build 18.3 s) |
| S1 pause 30 s then resume | PASS | resumed in 2.19 s, progress advanced |
| Rollback to stable | PASS | build=`0.5.2.4`, video playing; preview left disabled, stable enabled |

Evidence: `_harness/evidence/preview-round2-20261105.json`, `_harness/evidence/preview-shots-20261105.json`,
`_harness/evidence/preview-round2-panel.png` (real panel), `_harness/evidence/preview-round2-version.png` (version).

---

## 包内文件 / Package contents

| 文件 | 说明 |
|---|---|
| `DS-Whalegirl-preview.user.js` | 预览版脚本本体（完整元信息块） |
| `README.md` | 本文件：双语试用说明与三步操作 |
| `CHANGELOG.md` | 预览条目：相对稳定版的差异、已知问题、回退方式 |
| `PRE-RELEASE-CHECKLIST.md` | 发布前检查清单 |
| `PACKAGE-MANIFEST.md` | 发包清单：字节数、SHA256 |
| `LICENSE` | MIT |
| `assets/preview-panel.jpg` | 真机面板截图（预览版运行中） |
| `assets/preview-version.jpg` | 真机版本号截图（v0.5.3.0-preview.1 已启用） |

许可 / License: MIT（详见 `LICENSE`）。
