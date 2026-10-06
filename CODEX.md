# Codex 使用说明

- 图库仓库：`wen2003-bit/private-plot-gallery`（私有）。以 `gallery-local/INDEX.md` 为检索入口；候选卡片与图片文件均在同一目录。
- 通过已登录的 GitHub CLI/API 读取仓库。不要把整个图库克隆到工作目录；需要看图时只取当前任务相关的少数图片。
- `gallery-local/INDEX.md` 和卡片是小文本，可用 GitHub Contents API 读取。按需取原图时，从递归 Git tree 得到文件 SHA，再读 Git blob 的 base64 内容，在内存中解码并查看。需要临时文件时只写入临时目录，用完删除。
- 图片原始出处没有逐一核验；卡片来源记录为“个人上传”，不要推断或补写出处。
- 不要启用公开 Pages 或把内容推送到上游开源技能仓库。
- 网页浏览入口是本仓库主页：登录 GitHub 后可浏览 README 图册、原图和鉴赏卡。新增/替换文件后，若要更新首页目录、索引或鉴赏卡，再让 Codex 按用户要求提交相应变更。
