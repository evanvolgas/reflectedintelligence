---
layout: post
title: "Reflexion: Verbal Self-Feedback for AI Agents"
date: 2025-05-19
categories: [AI, Reflection]
---

> This post is the first in a series exploring reflection techniques in AI systems.

Even state-of-the-art AI agents can struggle to adapt to new situations without guidance. In one Stanford experiment, a mouse quickly explored a novel object (a red ball) while an AI agent ignored it entirely[^1]. The difference? Animals naturally **explore and learn from feedback**, whereas AI agents lack an intrinsic self-reflection mechanism.

Traditionally, improving an AI's performance in changing environments meant retraining or fine-tuning with lots of data – a slow and expensive process[^2]. Researchers have been asking: *can an AI learn from its own mistakes on the fly, like humans do?* This motivation led to **Reflexion**, a technique that gives AI agents a form of verbal self-feedback to rapidly learn from trial and error[^2].

## How it Works

Reflexion is a lightweight feedback loop. After each task attempt, the agent critiques its own performance in natural language, stores that reflection in memory, and uses it to guide the next try[^2]. These reflections—short, plain-text lessons—replace gradient updates with context updates. No model weights are changed; instead, the agent learns via "semantic gradients" encoded in language.

For example, a failed attempt might generate a note like: *"I forgot to check if the object was unlocked. I should verify that first next time."* That memory becomes part of the prompt on the next run. Reflexion is compatible with many kinds of feedback—scores, pass/fail signals, even textual critiques—and turns them into actionable, interpretable self-guidance[^2].

## Implementation: LangChain and Sifaka

LangChain offers an open-source implementation of Reflexion via its `ReflexionAgent`[^3]. The agent drafts an answer, critiques it (often grounding the feedback with tools or citations), and tries again with the self-critique included as memory[^4]. Under the hood, it runs two LLM passes per loop: one for output, another for reflection. This continues until the agent meets success criteria or hits a retry limit.

Sifaka, an open-source library for self-improving LLM workflows, implements Reflexion as a reusable **critic module**. Instead of bundling Reflexion into the agent loop, Sifaka decouples reflection logic into standalone "critics" that evaluate the generator's output, suggest improvements, and optionally trigger retries. Its [`reflexion.py`](https://github.com/sifaka-ai/sifaka/blob/main/sifaka/critics/reflexion.py) module defines a structured critic that supports verbal feedback, reflection accumulation, and termination conditions based on configurable stop criteria[^5]. This modular design makes it easy to integrate Reflexion into any agent loop—just specify the critic, and Sifaka handles the iterative refinement. It also plays well with other critics, allowing Reflexion to be layered with factuality, tone, or task-specific checks.

## Why it Matters

Reflexion isn't just efficient—it works. Agents using it have shown dramatic gains: for example, a GPT-4 coding agent improved from 80% to 91% accuracy on HumanEval simply by reflecting on failures[^2].

Its benefits go beyond performance:

- **Adaptivity:** Agents adjust in-session without retraining.
- **Interpretability:** Reflections expose the agent's "thinking."
- **Generalization:** The method transfers across domains—from text games to coding to reasoning tasks[^2].

As AI systems become more autonomous, Reflexion offers a pragmatic step toward agents that *learn like humans do*: by thinking about what just happened—and doing better next time.

References:

[^1]: Kauvar, I., Doyle, C., Zhou, L., & Haber, N. (2023). *AI Agents that "Self-Reflect" Perform Better in Changing Environments*. [Stanford HAI](https://hai.stanford.edu/news/ai-agents-self-reflect-perform-better-changing-environments).

[^2]: Shinn, N., Cassano, F., Berman, E., Gopinath, A., Narasimhan, K., & Yao, S. (2023). *Reflexion: Language Agents with Verbal Reinforcement Learning*. [arXiv:2303.11366](https://arxiv.org/abs/2303.11366).

[^3]: LangChain (2024). *Reflection Agents* (Blog). [blog.langchain.dev](https://blog.langchain.dev/reflection-agents/).

[^4]: LangChain. *Reflexion Agent Implementation*. [GitHub](https://github.com/langchain-ai/langgraph/blob/main/docs/docs/tutorials/reflexion/reflexion.ipynb).

[^5]: Sifaka AI. *Reflexion Critic Implementation*. [GitHub](https://github.com/sifaka-ai/sifaka/blob/main/sifaka/critics/reflexion.py).
