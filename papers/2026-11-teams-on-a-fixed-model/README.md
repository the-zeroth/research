# Teams on a Fixed Model: Two Months of Harness Experiments with The One

固定模型之上的智能体团队：The One 两个月框架实验

Ziyang Zhang (张子阳), The Zeroth · Preprint, November 2026

- [PDF, English (18 pages)](teams-on-a-fixed-model.pdf)
- [PDF，中文（21 页）](teams-on-a-fixed-model-zh.pdf)
- [LaTeX source](source) (`en/` and `zh/`; build with `tectonic -X compile main.tex`)
- Code: [the-one-harbor](https://github.com/the-zeroth/the-one-harbor), the Harbor adapter used for the
  Terminal-Bench runs

## Abstract

How much can an agent-team harness add when the model is fixed? We report eight weeks (28 September to
20 November 2026) of controlled experiments on The One, a product that runs teams of language-model agents on
a person's computer. Three programs ran back to back: V1 on a task suite of our own (over 120 batches), V8 on
Terminal-Bench 4.0 through the Harbor framework (315 jobs and 6,223 graded trials, with 30 tasks held out and
never read), and a final Terminal-Bench 4.1 run under the Artificial Analysis protocol. The configuration we
kept, a single lead agent on GPT-6.2 Sol at maximum reasoning effort, scored 60.9% on the 63 tasks we could run
and 58.1% with the three GPU tasks counted as failures. That ties the model vendor's own agent (Codex) on the
same model and effort while using about 30% fewer input tokens, at $1.35 per attempt at list price. Three
findings carry the paper. Append-only context cut cost by a third to a half with no change in accuracy. On
tasks that one context can hold, a single strong owner matched or beat every team structure we built, and
same-model second opinions confirmed the shared misreading instead of catching it. The model's choice at a
decision point moved when facts were placed in front of it, never with advice. Most levers that won on the tasks
they were designed on failed on held-out tasks; we describe the held-out discipline that caught them, and report
the negative results in full.

## 摘要

模型固定时，一个智能体团队框架（harness）还能带来多少提升？本文报告 2026 年 9 月 28 日至 11 月 20 日共八周在
The One 上做的对照实验。The One 是一款在个人电脑上运行语言模型智能体团队的产品。三个实验项目先后进行：V1 在我们
自建的任务集上进行（120 多批）；V8 通过 Harbor 框架在 Terminal-Bench 4.0 上进行（315 个作业、6,223 次已评分试验，
其中 30 道题留出、从未读过）；最后按 Artificial Analysis 的协议在 Terminal-Bench 4.1 上跑了一次。最终保留的配置是
单个领队智能体，用 GPT-6.2 Sol、最高推理强度（max）。它在能运行的 63 道题上得分 60.9%，把 3 道需要 GPU 的题记为失败
时得分 58.1%，与模型服务商自家的智能体（Codex）在同一模型、同一强度下持平，同时输入 token 少约 30%，按公开标价每次
尝试 1.35 美元。本文有三个主要发现。第一，只追加的上下文把成本降低三分之一到一半，准确率不变。第二，在单个上下文
装得下的任务上，一个能力强的负责者不输于我们搭建的任何团队结构，而同一模型给出的第二意见只会确认共同的误读，抓不住
它。第三，模型在决策点上的选择只有在事实摆到它面前时才会改变，建议从未改变它。多数在设计任务上胜出的手段到了留出
任务上就失效了；本文介绍了发现这些问题的留出纪律，并完整报告了负面结果。

## Cite

```bibtex
@misc{zhang2026teams,
  title  = {Teams on a Fixed Model: Two Months of Harness Experiments with The One},
  author = {Zhang, Ziyang},
  year   = {2026},
  month  = nov,
  note   = {Preprint},
  url    = {https://github.com/the-zeroth/research/tree/main/papers/2026-11-teams-on-a-fixed-model}
}
```

## License

CC BY 4.0, see [LICENSE](../../LICENSE).
