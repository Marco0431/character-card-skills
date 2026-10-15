# Character Card Skills

面向 SillyTavern 与 BrainDance/taberna 的中文角色卡创作技能。当前发布版提供创作指南、世界书查询和只读结构审计。

- [campus-card-skill](skills/campus-card-skill/SKILL.md)：创作主入口，涵盖人物、开场、世界书、状态和记忆，支持校园及其他题材。
- [world-book-skill](skills/world-book-skill/SKILL.md)：ST 兼容入口，复用主技能的指南。

## 安装

将 `skills/` 下的两个目录一起复制到目标工具的技能目录，保持同级；项目内可放入 `.agents/skills/`。这两项是项目技能，只有文件所在的项目环境才能使用该安装。仓库中的 `skills/` 是分发目录，上传 GitHub 本身不会将技能安装到其他项目。

使用 `$campus-card-skill` 或 `$world-book-skill` 并说明目标卡文件和需求。所有 Python 工具只依赖标准库；验证环境为 Python 3.12。

## 能力与边界

可以创作、改稿和组织 JSON；附带 CLI 只读取用户指定的 JSON，不自动修改文件、不联网、不执行卡内代码。输入限制为 8 MiB。查询会展示卡内内容，分享结果前应检查隐私。

发布版已移除远程 JavaScript、MVU/EJS/动态 HTML 示例、旧自动生成和写入工具，以及绕过安全约束的旧提示。引导页采用纯文本或 Markdown，不提供脚本按钮和动态面板。

## 验证

在仓库根目录运行：

```sh
python -m unittest discover -s skills/campus-card-skill/scripts -p "test_*.py"
python -m unittest discover -s tests -p "test_*.py"
```

范围和限制见 [SECURITY.md](SECURITY.md)。不包含私人角色作品、凭据、本机绝对路径或原项目提交历史。
