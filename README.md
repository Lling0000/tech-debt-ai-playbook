# Tech Debt AI Playbook

> 中文版优先。English version is included below.

这是一份写给小白的工程判断入门文档。

它想讲清楚一件事：

> 技术栈不是信仰，风险判断才是核心。  
> 但你越懂技术栈里的隐性知识，就越能驱动 AI，而不是被 AI 带着走。

很多人刚开始做项目、重构系统、处理技术债时，会先问：

- 我该用什么框架？
- 我要不要换一个更先进的技术栈？
- AI 说这个架构更现代，我要不要照做？

这些问题不是完全不重要，但它们不是最先要问的问题。

更重要的问题是：

- 哪一部分最可能先崩？
- 哪一部分一崩会带着其他地方塌？
- 我怎么提前用测试发现问题？
- 出问题时能不能快速回退？
- 新方案能不能先在旁边影子运行，而不是一上来就接管线上？
- 我能不能给 AI 清晰的边界，而不是让 AI 替我做所有判断？

## 适合谁读

- 刚开始学习编程和工程实践的人
- 想理解“技术债”但不想被术语吓到的人
- 已经会用 AI 写代码，但发现自己容易被 AI 的方案带着走的人
- 想学习测试驱动、灰度、回滚、影子替代这些工程思维的人
- 想把项目做得更稳，而不只是“看起来更现代”的人

## 你会学到什么

- 为什么“技术栈不重要”这句话不能被误解
- 什么是技术栈的隐性知识
- 为什么懂得越多，越能更好地使用 AI
- 怎么判断系统哪里会先崩
- 怎么用测试保护旧行为
- 什么是 shadow mode，也就是影子运行
- 怎么让 AI 成为执行力，而不是方向盘
- 小白可以直接照着用的检查清单和提示词模板

## 快速阅读

中文：

- [目录](SUMMARY.md)
- [00. 写在前面](docs/zh/00-preface.md)
- [01. 核心观念：技术栈不是信仰](docs/zh/01-core-idea.md)
- [02. 技术栈隐性知识：你驱动 AI 的底气](docs/zh/02-hidden-knowledge-and-ai.md)
- [03. 实例：从会崩的地方开始](docs/zh/03-examples.md)
- [04. 小白检查清单](docs/zh/04-checklist.md)

English:

- [Table of Contents](SUMMARY.md#english)
- [00. Preface](docs/en/00-preface.md)
- [01. Core Idea: The Stack Is Not a Religion](docs/en/01-core-idea.md)
- [02. Hidden Stack Knowledge: How You Drive AI](docs/en/02-hidden-knowledge-and-ai.md)
- [03. Examples: Start Where Things Break](docs/en/03-examples.md)
- [04. Beginner Checklist](docs/en/04-checklist.md)

## 一句话总结

如果你只会问 AI：

```text
帮我重构一下。
```

你很可能会被 AI 的方案带着走。

如果你能问：

```text
先不要改业务行为。
请先找出这个模块的外部可观察行为、潜在回归点和必须保留的兼容逻辑。
然后补最小测试。
最后只在 feature flag 后面接入新实现，并保留旧实现作为 fallback。
```

你就在驱动 AI。

区别不在提示词多漂亮，而在你有没有工程判断力。

## English Summary

This is a beginner-friendly playbook about technical debt, hidden stack knowledge, testing, shadow mode, and AI-assisted engineering.

The core idea:

> The technology stack is not the goal.  
> Engineering judgment is the goal.  
> Hidden stack knowledge helps you guide AI instead of letting AI guide you.

AI can generate code quickly, but it does not automatically know your system's fragile parts, old contracts, production risks, rollback paths, or business invariants.

You should use AI as an amplifier, not as the driver.

## 推荐使用方式

读的时候不要急着背概念。

每看完一节，就拿你自己的项目问三个问题：

- 这里最容易先坏的是哪里？
- 如果它坏了，我怎么发现？
- 如果它真的坏了，我怎么退回去？

这三个问题，比“我应该换什么框架”更接近真实工程。

## License

MIT

