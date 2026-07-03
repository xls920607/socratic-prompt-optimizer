# Socratic Prompt Optimizer

Codex skill for turning direct task prompts into Socratic question-chain prompts.

## What It Does

This skill rewrites raw prompts so the next model first clarifies:

- what a good result looks like
- which standards or frameworks should be used
- what evidence or context must be checked
- how to apply the framework to the concrete task
- what risks, omissions, or unclear points should be flagged

It is especially useful for product方案, design review, research, team assessment, PPT outlines, and other tasks that benefit from structured reasoning.

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
