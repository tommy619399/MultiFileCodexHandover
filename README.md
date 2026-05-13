# MultiFileCodexHandover

一个面向 Codex 的**三文件交接工作流 Skill**。

它适合中大型项目、长期项目、多人协作项目，或者你不想把所有规则、项目地图、任务交接都塞进一个 `AGENTS.md` 的场景。

## 核心思路

使用三个文件分工协作：

```text
AGENTS.md
docs/codex-project-map.md
docs/codex-handoff.md
```

三者分工：

| 文件 | 作用 | 更新频率 |
|---|---|---|
| `AGENTS.md` | 项目固定规则、禁止事项、验证要求、第三方依赖规则 | 少改 |
| `docs/codex-project-map.md` | 项目地图、技术栈、目录结构、核心模块、命令、依赖清单 | 项目结构变化时更新 |
| `docs/codex-handoff.md` | 当前任务状态、最近修改、验证结果、下一步建议 | 每个线程结束更新 |

一句话：

```text
AGENTS.md 是规矩，codex-project-map.md 是地图，codex-handoff.md 是接力棒。
```

## Skill 路径

本仓库的 Skill 位于：

```text
.agents/skills/multi-file-codex-handover/
```

核心文件：

```text
.agents/skills/multi-file-codex-handover/SKILL.md
```

## 安装方式

### 方式一：在 Codex 中使用 `$skill-installer`

在 Codex 中输入：

```text
$skill-installer install https://github.com/tommy619399/MultiFileCodexHandover/tree/main/.agents/skills/multi-file-codex-handover
```

安装完成后，重启 Codex。

### 方式二：手动安装为用户级 Skill

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/tommy619399/MultiFileCodexHandover.git /tmp/MultiFileCodexHandover
cp -R /tmp/MultiFileCodexHandover/.agents/skills/multi-file-codex-handover ~/.agents/skills/
```

重启 Codex 后生效。

### 方式三：作为项目级 Skill 使用

把本仓库中的 Skill 目录复制到目标项目：

```text
目标项目/
  .agents/
    skills/
      multi-file-codex-handover/
        SKILL.md
```

## 使用方式

### 新项目从 0 建档

```text
$multi-file-codex-handover

这是一个新项目，请按三文件交接工作流创建 AGENTS.md、docs/codex-project-map.md、docs/codex-handoff.md。
```

### 已有项目读取

```text
$multi-file-codex-handover

这是一个已有项目，请读取项目骨架并建立或更新三文件交接系统。
```

### 线程结束总结

```text
$multi-file-codex-handover

请进行线程结束总结，并更新 docs/codex-handoff.md；如果项目结构、核心依赖、常用命令发生变化，也同步更新 docs/codex-project-map.md。
```

### 新线程继续

```text
$multi-file-codex-handover

请先阅读 AGENTS.md、docs/codex-project-map.md、docs/codex-handoff.md，然后继续这个任务：
【写你的具体任务】
```

## 第三方库规则

这个 Skill 允许 Codex 根据任务需要安装第三方库，但必须遵守：

- 优先复用已有依赖。
- 不为了小问题引入大依赖。
- 普通低风险依赖可以判断必要后直接安装并继续实现。
- 高风险依赖安装前必须先给方案并等待确认。
- 每次依赖变更必须写入 `docs/codex-handoff.md` 的“依赖变更”。
- 如果是核心依赖，还必须更新 `docs/codex-project-map.md` 的“依赖清单”。

高风险依赖包括：安全、加密、鉴权、支付、文件上传、网络请求核心层、数据库迁移、ORM、状态管理核心替换、构建系统替换、大型 UI 框架替换。

## 文档语言

所有交接文档说明性内容默认使用中文。代码路径、命令、包名、库名、API 名称、配置项、错误信息保留英文原文。
