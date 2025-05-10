---
title: "LLM-based Actor-Critic (LAC)"
date: 2025-05-23
author: Evan Volgas
tags: [AI, RLHF, reinforcement-learning, LLMs, decision-making]
---

> This post is the fifth and final in a series exploring reflection techniques in AI systems. For the complete series, see our posts on [Reflexion](/2025/05/19/reflexion.html), [Self-Refine](/2025/05/20/self-refine.html), [Generative Agents](/2025/05/21/generative-agents.html), and [Constitutional AI](/2025/05/22/constitutional-ai.html).

Can an AI learn better decision-making if we just **talk to it** about its choices? Researchers are finding that the answer is yes. Instead of only training a model with numerical rewards, giving an AI feedback in plain language can dramatically improve its ability to make complex decisions. A new approach called **LLM-based Actor-Critic (LAC)** shows how *language feedback* can steer a large language model (LLM) to better outcomes[^1]. In simple terms, it's like guiding the AI with both a helpful coach *and* a scorekeeper, rather than leaving it to figure everything out alone.

## The Challenge: LLMs and Decision-Making

Large language models (like GPT-4 or ChatGPT) are very good at understanding instructions and generating text. But when you ask an LLM to **solve a multi-step problem or make a series of decisions**, it often struggles. The model might take actions that seem reasonable word-by-word but don't lead to a successful result. This is because the AI has no built-in sense of which intermediate steps are *on track* toward the goal. It tends to "wing it," sometimes going off on tangents or repeating mistakes.

Humans, on the other hand, improve at complex tasks by **getting feedback** at each step – a teacher might say "good move" or "that's a mistake, try a different approach." The LAC method brings a similar kind of step-by-step feedback into the AI's decision process.

## Two Critics Are Better Than One

LAC is inspired by the classic *actor-critic* technique in reinforcement learning, but with a twist. In a video game analogy, imagine the AI is the "player" (the *actor*) trying to make the right moves. In traditional reinforcement learning, a single *critic* might tell the player how well it's doing via a score or reward signal. LAC uses **two critics** instead, each providing a different kind of feedback:

- **Language Critic:** This critic gives **contextual feedback in natural language**. After the AI chooses an action, the language critic comments on it as if evaluating a trainee. For example, if an AI agent in a household simulation decides to look for an apple in the living room, the language critic might respond with: "That may not be the best place – apples are usually in the kitchen." This textual feedback is rich in information: it tells *why* an action is good or bad in context[^1].

- **Value Critic:** This critic provides a **quantitative score** for each possible action. It estimates the long-term success likelihood if that action is taken. In the apple-finding example, the value critic might say something like: "Going to the refrigerator has a 90% chance of success." It's effectively giving a probability or reward estimate for the action[^1].

By combining these two forms of feedback, the AI can pick actions that **make sense qualitatively** (the advice is sound) *and* **are likely to succeed** (the numbers look good). The language critic's guidance helps the model avoid obvious mistakes or irrelevant steps, while the value critic's score helps it focus on actions with the highest payoff.

## Learning on the Fly, No Re-Training Needed

One impressive aspect of LAC is that it improves the AI's decisions **without retraining the model from scratch**. The system is described as "gradient-free," meaning the researchers don't fine-tune the LLM's internal weights with back-propagation during this decision-making process[^1]. Instead, the critics' feedback is fed back into the model's prompts in real time.

In practice, the AI takes an action, then reads the language critic's comments and considers the value critic's score, and then that information is added to its next query or prompt. This way, the LLM "learns" within the session to adjust its strategy, almost like how a person might learn through conversation and coaching. Because this adaptation happens through prompting, it avoids heavy computation and is easier to scale.

## Better Results with Language Feedback

Does this dual-critic approach actually make a difference? According to the study, yes – a big one. The LAC framework was tested in several simulated decision-making environments. In these tests, an AI using LAC was **more successful at achieving the goals** than other methods.

Most notably, *even a smaller model (7–8B) using LAC outperformed a baseline using GPT-4 and the ReAct reasoning strategy*[^2]. ReAct (short for "Reasoning and Acting") is a strong prompting technique where the model breaks tasks into chains of thought. But the dual-critic feedback helped smaller models beat it. That's a strong argument that **guidance beats size**, at least in certain decision-making tasks.

## Toward More Reflective AI

At its core, the LAC approach shows the power of *reflective feedback* in AI systems. Instead of treating the AI as a black box that we only reward or punish, this method opens up a dialogue where the AI can **hear advice in words** and adjust accordingly.

It's an exciting step toward AI that can **learn from language-based feedback** in addition to experience. And it's a reminder that sometimes, the best way to teach is to talk things through.

## References

[^1]: [Dong, H., Duan, K., & Zhang, C. (2024). *LAC: LLM-Based Actor-Critic with Dual Critics*. arXiv:2403.03692 [cs.AI].](https://arxiv.org/abs/2403.03692)

[^2]: [Yao, S., et al. (2022). *ReAct: Synergizing Reasoning and Acting in Language Models*. arXiv:2210.03629 [cs.CL].](https://arxiv.org/abs/2210.03629)
