# 苏格拉底提示词优化器

这是一个 Codex Skill，用来把直接下任务的 prompt 改写成“苏格拉底式问题链”prompt。

## 它能做什么

这个 skill 会把原始 prompt 改写成一种更适合复杂任务的结构，让下一个模型先想清楚：

- 什么样的结果才算好
- 应该用哪些标准、原则或框架来判断
- 需要检查哪些证据、资料或上下文
- 如何把框架应用到当前具体任务
- 哪些风险、遗漏或不清楚的地方需要标记

它尤其适合这些场景：

- 产品方案设计
- 业务规则梳理
- 设计稿评审
- 调研分析
- 团队/项目评价
- PPT 大纲生成
- 其他需要结构化推理的复杂任务

## 安装方式

把这个仓库克隆到你的 Codex skills 目录：

```bash
git clone https://github.com/xls920607/socratic-prompt-optimizer.git ~/.codex/skills/socratic-prompt-optimizer
```

然后重启 Codex，或者新开一个对话，让 skill 列表刷新。

## 使用方式

显式调用：

```text
$socratic-prompt-optimizer 帮我优化这个 prompt：...
```

也可以自然表达：

```text
按苏格拉底提示法帮我优化这个 prompt：...
```

## 行为边界

这个 skill 只负责优化 prompt。

它会保留原 prompt 里的链接、约束、输出格式和任务要求，但不会真的去执行 prompt 里的任务。例如，原 prompt 里写了“写入飞书文档”或“分析代码”，这个 skill 只会把这些要求保留在优化后的 prompt 中，不会实际写文档或分析代码。

---

# Socratic Prompt Optimizer

Codex skill for turning direct task prompts into Socratic question-chain prompts.

## What It Does

This skill rewrites raw prompts so the next model first clarifies:

- what a good result looks like
- which standards or frameworks should be used
- what evidence or context must be checked
- how to apply the framework to the concrete task
- what risks, omissions, or unclear points should be flagged

It is especially useful for product schemes, business rule analysis, design review, research, team assessment, PPT outlines, and other tasks that benefit from structured reasoning.

## Install

Clone this repository into your Codex skills folder:

```bash
git clone https://github.com/xls920607/socratic-prompt-optimizer.git ~/.codex/skills/socratic-prompt-optimizer
```

Then restart Codex or start a new thread so the skill list refreshes.

## Usage

Invoke it explicitly:

```text
$socratic-prompt-optimizer 帮我优化这个 prompt：...
```

Or ask naturally:

```text
按苏格拉底提示法帮我优化这个 prompt：...
```

## Behavior

The skill only optimizes prompts. It preserves links, constraints, and output requirements inside the optimized prompt, but does not execute the embedded task.
