# Prompt Registry Mirror

本目录是提示词 registry 的自托管镜像。

- `manifest.json`：版本与来源元数据
- `prompts.json`：全部提示词快照

本地工作台会优先直接读取本目录；浏览器 / Vercel 通过同站路径
`assets/prompt-studio/prompt-registry/` 加载（构建或发布前请同步复制）。

远程兜底地址：

```text
https://raw.githubusercontent.com/abutao/linyi-skills/main/skills/linyi-image/assets/prompt-registry/
```

## 更新镜像

```powershell
$base = "https://raw.githubusercontent.com/yukkcat/image-prompts/main/dist"
$out = "skills/linyi-image/assets/prompt-registry"
$static = "skills/linyi-image/assets/prompt-studio/prompt-registry"
Invoke-WebRequest "$base/manifest.json" -OutFile "$out/manifest.json"
Invoke-WebRequest "$base/prompts.json" -OutFile "$out/prompts.json"
New-Item -ItemType Directory -Force -Path $static | Out-Null
Copy-Item "$out\manifest.json","$out\prompts.json" -Destination $static -Force
```

然后刷新浏览器兜底快照：

```powershell
python skills/linyi-image/scripts/export_prompt_library.py
```
