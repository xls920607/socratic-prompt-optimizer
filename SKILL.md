---
name: socratic-prompt-optimizer
description: Optimize raw prompts into concise Socratic question-chain prompts. Use when the user asks to improve, rewrite, polish, or optimize a prompt, especially with wording like "按苏格拉底方法", "苏格拉底提示法", "优化prompt", "优化提示词", "封装成问题链", or when they provide a task prompt and want a better prompt back. The skill returns an optimized prompt only; it must not execute the task described inside the prompt.
---

# Socratic Prompt Optimizer

## Core Rule

Convert direct task instructions into a prompt that makes the next model reason before producing output.

Do not execute the user's embedded task. If the raw prompt says "write to Feishu", "analyze code", "read docs", "make a PPT", or similar, preserve that as an instruction inside the optimized prompt, but do not perform it.

Unless the user asks for explanation, return only a short label plus one fenced prompt:

`优化后的 prompt：`

Then a single `text` fenced block containing the optimized prompt.

## Optimization Workflow

1. Identify the raw prompt's actual goal, audience, inputs, output format, constraints, and destination.
2. Preserve all concrete requirements, names, fields, links, schemas, and "must not miss" constraints.
3. Replace direct commands with a Socratic question chain:
   - Goal question: What outcome is considered good?
   - Criteria question: What standards should judge quality?
   - Framework question: Which dimensions, principles, or models should be used?
   - Evidence question: What source material, data, or examples must be checked?
   - Application question: How should the framework be applied to this concrete task?
   - Risk question: What edge cases, omissions, or unclear points must be flagged?
4. Then add clear task instructions that require the model to use answers to those questions before outputting the final result.
5. Specify a structured output format: headings, table columns, checklist, or final artifact style.
6. Keep the optimized prompt concise. Add depth only when the raw task is complex.

## Prompt Structure

Use this structure by default:

```text
请基于“苏格拉底式提示法”完成以下任务。

背景：
[preserved context]

请先围绕以下问题建立判断框架：
1. [goal/quality question]
2. [classification/framework question]
3. [evidence/source question]
4. [application/detail question]
5. [risk/edge-case question]

任务目标：
[specific deliverable]

具体要求：
[preserved constraints and fields]

输出结构：
[required sections/table columns]

输出要求：
[tone, concision, completeness, do-not-do constraints]
```

## Depth Control

Use a light version for simple rewrite, summary, translation, formatting, or one-step tasks:

- Ask only 2-3 useful questions.
- Do not add expert simulation, assumptions, risk matrices, or long output sections.
- Keep the optimized prompt shorter than the original if possible.

Use a full version for product方案, research, evaluation, design review, business analysis, team assessment, code-truth analysis, PPT generation, or cross-source synthesis:

- Add expert perspective questions, such as "专家会先问什么", "需要验证哪些假设", "哪些证据不足".
- Require evidence boundaries and "待确认" items.
- Include a table-first output format when the user asks for structured analysis.

## Quality Standards

The optimized prompt must:

- Make the model think before producing the final artifact.
- Avoid vague instructions like "深入分析" without criteria.
- Preserve the user's business intent and exact deliverables.
- Preserve all destination links as text, but do not open or write them.
- Separate stable classification fields from display copy, reason details, or notes when the task involves enums/statuses.
- Use user-friendly wording when the task asks for product-facing copy.
- Include "证据不足则标记待确认" for analysis tasks that depend on external materials.
- Avoid unnecessary verbosity. The goal is sharper reasoning, not longer prompts.

## Common Patterns

### Product Scheme / Business Rule

Ask about classification principles, stable fields, user-visible outcomes, downstream dependencies, and edge cases. Output usually includes conclusion, design principles, mapping table, unresolved questions, and implementation notes.

### Design Review

Ask about first impression, value perception, user motivation, information hierarchy, conversion impact, and copy clarity. Output usually includes overall verdict, version comparison, module review, concrete improvements, and replacement copy.

### Research / Internal Assessment

Ask about evaluation criteria, evidence quality, confounders, fair comparison, and confidence level. Require evidence-based conclusions and constructive wording.

### PPT / Content Generation

Ask about audience baseline, learning path, key concepts, examples, misconceptions, and story arc. Output page-by-page structure with speaker notes and visual suggestions.

## Example

Raw prompt:

```text
帮我看下会员页未开通状态，重点看出勤奖励包和会员狂欢日有没有吸引力。
```

Optimized prompt:

```text
请基于“苏格拉底式提示法”评审会员页未开通状态。

请先围绕以下问题建立判断框架：
1. 用户第一次进入未开通页时，什么信息会让他感到会员值得开通？
2. 出勤奖励包的利益点是否明确、可信、容易理解？
3. 会员狂欢日是否传达了稀缺感、期待感和参与动机？
4. 当前信息层级是否让核心权益足够突出？
5. 哪些文案或视觉表达会削弱转化意愿？

任务目标：
判断当前设计是否有吸引力，并给出可直接指导设计稿修改的建议。

输出结构：
一、整体结论
二、核心权益评审表
三、主要问题
四、具体优化建议
五、可直接替换的文案

输出要求：
结论直接，聚焦未开通状态，不扩展到已开通页面。
```
