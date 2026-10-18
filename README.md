# 蓝泡 · Lanpao

<p align="center">
  <img src="preview.gif" width="240" alt="蓝泡 Codex 动画宠物预览">
</p>

蛋仔派对蛋小黑，蓝泡是ai为他取得名字，这个名字也挺符合蛋小黑形象的，所以我也没有改。
蓝泡是一只适配 Codex v2 的自定义动画宠物：圆滚滚的蓝色宇航小企鹅，戴着橙嘴鸭舌帽、黑色眼罩和蓝白条纹宇航服。
<img width="1080" height="1272" alt="图层 1" src="https://github.com/user-attachments/assets/76c357f4-7bae-4a87-8700-753b2a26dbd0" />

## 包含内容

- Codex v2 动画宠物定义：`pet.json`
- 8 列 × 11 行透明 WebP 图集：`spritesheet.webp`
- 完整标准动作：idle、左右移动、挥手、跳跃、失败、等待、处理中、审查
- 16 个顺时针视线方向
- 图集尺寸：`1536 × 2288`
- 图集版本：`spriteVersionNumber: 2`
- 动画预览：`preview.gif`
<img width="192" height="208" alt="preview" src="https://github.com/user-attachments/assets/74b02864-8026-4633-9a3f-445ebd8da9b7" />

## 文件结构

```text
lanpao-codex-pet/
├── pet.json
├── spritesheet.webp
├── preview.gif
├── README.md
├── LICENSE
├── LICENSES.md
├── CHANGELOG.md
├── .gitattributes
└── .gitignore
```

## 安装

### Windows PowerShell

```powershell
git clone https://github.com/YOUR_GITHUB_NAME/lanpao-codex-pet.git
Set-Location .\lanpao-codex-pet

$codexHome = if ($env:CODEX_HOME) {
  $env:CODEX_HOME
} else {
  Join-Path $env:USERPROFILE ".codex"
}
$petDir = Join-Path $codexHome "pets\lanpao"

if (Test-Path $petDir) {
  $backup = "$petDir.backup-$(Get-Date -Format yyyyMMddHHmmss)"
  Copy-Item -LiteralPath $petDir -Destination $backup -Recurse
}

New-Item -ItemType Directory -Path $petDir -Force | Out-Null
Copy-Item -LiteralPath .\pet.json -Destination $petDir -Force
Copy-Item -LiteralPath .\spritesheet.webp -Destination $petDir -Force

Write-Host "Installed to $petDir"
```

如果 Codex 的宠物列表没有立即刷新，重启 Codex 或新开一个任务。

### macOS / Linux

```bash
git clone https://github.com/YOUR_GITHUB_NAME/lanpao-codex-pet.git
cd lanpao-codex-pet

CODEX_HOME="${CODEX_HOME:-$HOME/.codex}"
PET_DIR="$CODEX_HOME/pets/lanpao"

if [ -d "$PET_DIR" ]; then
  cp -R "$PET_DIR" "$PET_DIR.backup-$(date +%Y%m%d%H%M%S)"
fi

mkdir -p "$PET_DIR"
cp pet.json spritesheet.webp "$PET_DIR/"
```

## 验证

检查版本号：

```powershell
(Get-Content .\pet.json -Raw -Encoding UTF8 | ConvertFrom-Json).spriteVersionNumber
```

应当输出：

```text
2
```

确认两个必需文件位于同一目录：

```text
spritesheet.webp
pet.json
```

`spritesheet.webp` 应为 `1536 × 2288`，并且包含透明背景。

## 更新宠物

`pet.json` 中的 `id` 现在是 `lanpao`。更新时请保持这个 ID 不变，否则 Codex 会把它视为另一只宠物。可以修改 `displayName` 和 `description`，但建议同时更新本 README，避免公开名称不一致。

## 许可证

本仓库采用分层许可：

- `spritesheet.webp` 与 `preview.gif`：**CC BY 4.0**
- `pet.json`、安装片段和其他文本配置：**MIT**

转载、分享或修改美术素材时，请保留署名并链接到本仓库。完整说明见 [LICENSES.md](LICENSES.md)。

## 致谢与声明

本项目是社区自定义 Codex 宠物，与 OpenAI 没有隶属或官方背书关系。

本项目使用 AI 辅助生成并进行确定性图集拼装、色边清理和方向 QA。公开发布前请确认你对底稿、生成结果和最终素材拥有发布权。
