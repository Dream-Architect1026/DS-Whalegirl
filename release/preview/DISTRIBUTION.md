# 发包清单（分发侧）· DS-Whalegirl v0.5.3.0-preview.1

> 本文件位于压缩包之外，用于记录压缩包本身的字节数、SHA256 与线上更新地址的 HTTP 校验结果。

## 压缩包

| 文件名 | 字节数 | SHA256 |
|---|---|---|
| `DS-Whalegirl-0.5.3.0-preview.1.zip` | 479543 | `1b95283150447e92d09612cbe2507731a29bf07c302c5acde377e208a09d87a3` |

## 线上更新地址（本轮 404 修复）

| 项目 | 值 |
|---|---|
| `@downloadURL` / `@updateURL` | `https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@main/release/preview/DS-Whalegirl-preview.user.js` |
| 期望状态 | HTTP 200，且下载内容 SHA256 与本机一致 |
| 校验方式 | `Invoke-WebRequest` 取回 → `Get-FileHash -Algorithm SHA256` 比对 |
| 发布 commit | `6f8697bd3d07d28c92adc19fb1b73bc828acfa29`（仅新增 `release/preview/`） |
| 固定地址校验 | **200 / 719315B / SHA256 `6cbc1d1a…` 一致**（`@6f8697bd…`，见 `_harness/evidence/preview-http-verify-20261105b.json`） |
| `@main` 地址校验 | **200，但内容仍为第一版构建（719327B / `74a25622…`）**：jsDelivr 对分支文件有 12 小时（`s-maxage=43200`）缓存，已用 `purge.jsdelivr.net` 两级清理（CF/FY 均返回 finished）仍未刷新 |
| 结论 | 404 已消除；自动更新链路可用。若需「立刻」拿到本轮内容，把地址中的 `@main` 换成 `@6f8697bd3d07d28c92adc19fb1b73bc828acfa29`；否则最长 12 小时后 `@main` 自动刷新到本轮构建（同版本号 `0.5.3.0-preview.1`，差异仅为两条 URL 元信息） |

复核命令（可直接复跑）：

```powershell
$u = "https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@main/release/preview/DS-Whalegirl-preview.user.js"
$r = Invoke-WebRequest $u -UseBasicParsing
"STATUS=$($r.StatusCode) BYTES=$($r.RawContentLength)"
$tmp = "$env:TEMP\preview-check.user.js"; [IO.File]::WriteAllBytes($tmp, $r.Content)
(Get-FileHash $tmp -Algorithm SHA256).Hash
```

## 包内文件

精确字节数与 SHA256 见包内 `PACKAGE-MANIFEST.md` 与 `SHA256SUMS.txt`（本文件不重复维护，避免双份数据漂移）。

## 安装 / 试用 / 回退

1. **安装**：停用稳定版 → 打开 `DS-Whalegirl-preview.user.js` → 「安装」。
2. **试用**：刷新课程页；`__HX_BUILD__` 应为 `0.5.3.0-preview.1`，`__HX_PREVIEW__()` 应返回
   `{fastStart:true, probeOnce:true, pendingState:false}`。
3. **回退**：停用/删除预览版 → 启用稳定版 → 刷新；`__HX_BUILD__` 回到 `0.5.2.4`，进度不丢。

校验压缩包：`Get-FileHash .\DS-Whalegirl-0.5.3.0-preview.1.zip -Algorithm SHA256`。
