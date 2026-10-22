# Prompt Registry Mirror

本目录是提示词 registry 的自托管镜像，供本地工作台与浏览器版「同步」使用。

- `manifest.json`：版本与来源元数据
- `prompts.json`：全部提示词快照

线上地址：

```text
https://raw.githubusercontent.com/abutao/linyi-skills/main/skills/linyi-image/assets/prompt-registry/
```

## 更新镜像

从上游拉取后覆盖本目录文件，确认 `registryHash` 校验通过，再提交并推送：

```powershell
$base = "https://raw.githubusercontent.com/yukkcat/image-prompts/main/dist"
$out = "skills/linyi-image/assets/prompt-registry"
Invoke-WebRequest "$base/manifest.json" -OutFile "$out/manifest.json"
Invoke-WebRequest "$base/prompts.json" -OutFile "$out/prompts.json"
```

更新 registry 后，如需刷新随构建发布的浏览器兜底快照，可在 Prompt Studio 同步一次，再运行：

```powershell
python skills/linyi-image/scripts/export_prompt_library.py
```
