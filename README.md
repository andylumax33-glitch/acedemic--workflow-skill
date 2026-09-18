# Academic Workflow Skill

一个可直接安装的学术工作流套件：包含 `academic-workflow-router` 路由 Skill，以及完整的 MathModel Skill 数学建模工作流。先判断交付物和约束，再选择一个主工作流，并按依赖顺序串联必要的辅助 Skill，避免多个端到端流程并行冲突。

## 包含内容

每个发布包都包含完整的 `MathModel-Skill` 数学建模工作流，以及 `academic-workflow-router` 的：

- `SKILL.md`：路由规则与交接约束
- `references/priority-map.md`：主 Skill 优先级表和验收场景
- `agents/openai.yaml`：Codex 调用元数据（Codex/Claude 包）
- `scripts/validate_routes.py`：安装后路由引用校验脚本

仓库根目录中的三个平台包已经把这些内容打包在一起，下载对应平台的一个 ZIP 即可整套安装。

## 安装

下载下表中与你使用的 Agent 对应的一个 ZIP，并将其解压到项目根目录。解压后保留包内的隐藏目录（`.agents`、`.claude` 或 `.trae`），不要只提取单个 `SKILL.md`。

## 使用

在支持 `$` Skill 调用的 Agent 中使用：

```text
请使用 $academic-workflow-router 选择本任务的主学术工作流，并说明后续串行交接。
```

该 Router 负责分类、选路和交接，不替代被选中的论文、建模、图表或引用 Skill。

## 一键安装完整套件

从仓库根目录下载与你使用的 Agent 对应的一个包：

| 平台 | 安装包 | 解压位置 |
|---|---|---|
| Codex | [`MathModel-Skill-Codex.zip`](./MathModel-Skill-Codex.zip) | 项目根目录，保留 `.agents/skills/` |
| Claude Code | [`MathModel-Skill-Claude-Code.zip`](./MathModel-Skill-Claude-Code.zip) | 项目根目录，保留 `.claude/skills/` |
| Trae | [`MathModel-Skill-Trae.zip`](./MathModel-Skill-Trae.zip) | 项目根目录，保留 `.trae/skills/` |

然后在项目根目录安装 Python 依赖：

```bash
python -m pip install -r requirements.txt
```

一个项目只安装一个平台包，不要混装三个目录。包内同时包含数学建模工作流和 `academic-workflow-router`，解压后即可按对应平台调用。

下载后可用 [`SHA256SUMS.txt`](./SHA256SUMS.txt) 校验文件完整性。

## 校验安装到完整 Skill 集合后运行：

```bash
# Codex
python .agents/skills/academic-workflow-router/scripts/validate_routes.py

# Claude Code
python .claude/skills/academic-workflow-router/scripts/validate_routes.py

# Trae
python .trae/skills/academic-workflow-router/scripts/validate_routes.py
```

校验会确认优先级表、必需的 Skill 引用和示例场景均存在。
