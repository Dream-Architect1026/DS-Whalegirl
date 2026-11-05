# CHANGELOG · 预览版 v0.5.3.0-preview.1

本文件只记录**预览发布通道**的条目；稳定版变更见仓库根目录 `CHANGELOG.md`（首条仍为 v0.5.2.4，未改动）。

## v0.5.3.0-preview.1 — 2026-11-05（第二版构建）

### 相对稳定版 v0.5.2.4 的改动

**元信息（发布隔离）**

- `@name`：`学习通纯免费刷课答题（DS-Whalegirl）` → `学习通纯免费刷课答题（DS-Whalegirl 预览版）`
- `@namespace`：`xinghong` → `xinghong-preview`（独立命名空间，避免覆盖稳定版）
- `@version`：`0.5.2.4` → `0.5.3.0-preview.1`
- `@description`：补充「预览版（Preview）」说明
- `@downloadURL` / `@updateURL`：指向 `release/preview/DS-Whalegirl-preview.user.js`
- 运行时构建号 `HX_BUILD`：`0.5.2.4` → `0.5.3.0-preview.1`（面板与控制台可识别）

**行为（仅预览通道，稳定版字节未变）**

1. **首播提速默认开启（DSW-106）**：`HX_FAST_START_ENABLED` 默认由 `false` 改为 `true`，
   首播无数据宽限 12s → 3s、播放冷却 6s → 2s；慢网下 10s 仍无数据由既有 `hxFastDegrade`
   自动回落稳妥节奏（只降不升）。关闭方式：脚本前设 `window.__HX_FAST_START__ = false`。
2. **attachShadow 探针副作用收敛（DSW-107）**：旧面板扫描对「裸空 div」逐个 `attachShadow`，
   会给页面稍后填充的挂载根挂上空的 open shadow。预览版改为**只探可见且可命中的裸 div**，
   且每个元素**只探一次**（`WeakSet` 记录），零尺寸/不可见元素不再被污染。
3. **移除不可达 pendingResume 状态（DSW-108）**：`hxPendingResume` 与 `st.pending` 全库无消费方
   （`canAct=false` 分支早于标记即 `return`），预览版整体删除；后台待恢复语义由回前台
   `hxOnVisible` 立即全量扫描兜底，行为等价、无功能损失。
4. **新增构建指纹 `__HX_PREVIEW__()`**：返回 `{ build, fastStart, probeOnce, pendingState }`，
   供真机核验本轮改动确已生效（只读诊断，不影响播放）。

播放、答题、保活、倍速、章节推进等业务逻辑**未做任何修改**；除上述 3 项外无其它差异。

### 验证（2026-11-05 第二轮真机）

- `node --check`：通过
- `node scripts/check_release.js`：6/6 通过（稳定版版本与 SHA256 一致、README/CHANGELOG 版本一致）
- `node scripts/check_preview.js`：14/14 通过（含「稳定版未引入任何预览标记」「预览版行为改动均已标注」）
- `node scripts/check_parity.js`：15 项能力锚点，缩减 0 项
- 真机冒烟（Edge 156 + ScriptCat 1.5.0，真实学习通课程页）：
  - 构建指纹：`{build:0.5.3.0-preview.1, fastStart:true, probeOnce:true, pendingState:false}`
  - S0 刷新恢复：3.63s 首播前进（上轮 18.3s，首播提速生效）
  - S1 暂停 30s 后恢复：2.19s 恢复
  - 回退：停预览、启稳定版后 `__HX_BUILD__=0.5.2.4`
- 证据：`_harness/evidence/preview-round2-20261105.json`、`_harness/evidence/preview-shots-20261105.json`、
  `_harness/evidence/preview-round2-panel.png`、`_harness/evidence/preview-round2-version.png`

### 已知问题

1. 预览版与稳定版同时启用会双注入（面板与日志重复）；试用前只保留一个。
2. 平台对非 1x 倍速会复位并暂停，脚本恢复为 1x 播放；属平台策略，非本版缺陷。
3. 首播提速默认开启：极慢网下会出现一次「回落到稳妥节奏」日志（预期行为，非故障）。
4. 自动更新依赖 `preview/` 路径已上传；未上传时无自动更新。

### 回退方式

1. 在脚本管理器中停用或删除 `学习通纯免费刷课答题（DS-Whalegirl 预览版）`。
2. 重新启用稳定版 `学习通纯免费刷课答题（DS-Whalegirl）`（若已卸载，重装仓库根目录 `DS-Whalegirl.user.js`）。
3. 刷新课程页面，确认 `__HX_BUILD__=0.5.2.4`、面板正常、视频继续播放。
4. 回退不需要清理缓存或重登；学习进度保存在平台侧，不会丢失。
