# 发包清单（分发侧）· DS-Whalegirl v0.5.3.0-preview.1

> 本文件位于压缩包之外，用于记录压缩包本身的字节数、SHA256 与线上地址的 HTTP 校验结果。

## 压缩包

| 文件名 | 字节数 | SHA256 |
|---|---|---|
| `DS-Whalegirl-0.5.3.0-preview.1.zip` | 479406 | `bf38e4db7559b62e43e9e68e03eced93186f08aab3da7f6d1a869d7e42303283` |

> 重建方式：9 个入口（脚本/README/CHANGELOG/CHECKLIST/MANIFEST/SHA256SUMS/LICENSE/2 张截图），
> 入口名使用正斜杠、时间戳固定为 2026-11-05T08:00:00Z，便于跨平台可重复解压。

## 线上地址（第三版：下载地址固定到版本 tag）

| 项目 | 值 |
|---|---|
| `@downloadURL` | `https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@v0.5.3.0-preview.1/release/preview/DS-Whalegirl-preview.user.js` |
| `@updateURL` | `https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@main/release/preview/DS-Whalegirl-preview.user.js` |
| 期望状态 | HTTP 200，且下载内容 SHA256 与本机一致（`a85db170…`，719329B） |
| 校验方式 | `Invoke-WebRequest` 取回 → `Get-FileHash -Algorithm SHA256` 比对 |
| 发布 commit | 见 `_harness/evidence/preview-push-20261105d.json` 的 `commit` 字段（tag `v0.5.3.0-preview.1` 指向同一 commit） |
| tag 地址校验 | 见下节「本轮实测」 |
| `@main` 地址校验 | 见下节「本轮实测」（分支文件有 ≤12h 缓存，内容可能滞后于 tag） |

## 本轮实测

（tag 创建后回填，证据文件 `_harness/evidence/preview-http-verify-20261105-tag.json`）

复核命令（可直接复跑）：

```powershell
$u = "https://cdn.jsdelivr.net/gh/Dream-Architect1026/DS-Whalegirl@v0.5.3.0-preview.1/release/preview/DS-Whalegirl-preview.user.js"
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
