---
title: "Constitutional AI: Harmlessness from AI Feedback"
date: 2025-05-22
categories: [AI, Alignment]
---

> This post is the fourth in a series exploring reflection techniques in AI systems. For the complete series, see our posts on [Reflexion](/2025/05/19/reflexion.html), [Self-Refine](/2025/05/20/self-refine.html), and [Generative Agents](/2025/05/21/generative-agents.html).

*Imagine training an AI by giving it a rulebook of principles – a kind of AI constitution – and letting it judge its own behavior according to those rules.* This is the idea behind **Constitutional AI**, an approach developed by Anthropic (the company behind the Claude chatbot) to make AI assistants more **helpful, honest, and harmless**. Instead of relying on tens of thousands of human feedback examples to teach an AI what not to do, Constitutional AI builds an explicit set of values into the AI and has the AI *self-supervise* its behavior using those values[^1]. In other words, the AI is trained to follow a *constitution* of guiding principles, which makes the AI's values transparent and easier to adjust, while greatly reducing the need for direct human oversight in judging the AI's outputs[^1].

## Why Give an AI a Constitution?

Traditional methods for aligning AI behavior (like Reinforcement Learning from Human Feedback, RLHF) require humans to manually evaluate or curate large numbers of model outputs. This has known downsides: it doesn't scale well as models produce more content, it can expose people to disturbing or harmful material, and the resulting "values" encoded in the AI remain implicit (buried in millions of parameters) rather than clearly defined. **Constitutional AI** tackles these issues by using a fixed set of written principles as the source of truth for what counts as harmful or helpful, and by having the AI **use these principles to critique and guide itself**[^2]. The "constitution" might include rules drawn from human rights ideals and best practices (e.g. *don't produce hate speech or encourage illegal acts*) so that the AI categorically avoids toxic or dangerous outputs[^2]. By baking the rules into the training process, we ensure the AI's behavior is governed by *explicit* values (the constitution) rather than a nebulous reward signal. This makes it much easier for developers (and society) to understand what standards the AI is supposed to uphold and to adjust those rules over time.

## How Does Constitutional AI Work?

The Constitutional AI process has two main stages. In the first stage (supervised learning), the AI model is prompted with various queries and initially produces some answers. Then a second AI (using the same principles as guidelines) generates a **critique** of those answers, pointing out where they might violate the constitution, and suggests an improved revision[^3]. The original model is then fine-tuned on these revised answers, effectively learning to produce responses that better adhere to the given principles.

In the second stage (reinforcement learning), the refined model is further optimized through practice. Instead of human evaluators picking the best answers, an **AI feedback mechanism** does the judging: the model generates multiple answers to new prompts, and an automated preference model (also powered by the constitutional principles) evaluates which answer is more aligned with the constitution's values[^3]. The model is rewarded for responses that the AI judge prefers. This technique is called **Reinforcement Learning from AI Feedback (RLAIF)** – the AI is learning from feedback provided by another AI, with the *constitution* as the ultimate guide. Throughout this training, no humans are directly labeling which outputs are good or bad; the only human input is in writing the constitution itself at the start.

## Results and Significance

Using AI feedback in this way proved remarkably effective. The team at Anthropic found that an assistant trained via Constitutional AI was rated *more helpful and harmless* than one trained with the standard human-feedback method[^4]. In fact, human evaluators preferred the responses of the constitution-guided model over those of an RLHF-trained model when it came to avoiding harmful content without losing nuance[^4].

Importantly, the **AI remained non-evasive** – rather than flatly refusing problematic requests with a generic "I can't help with that," the assistant would engage and **explain its objections** to the request, grounded in the constitutional principles[^5]. For example, if asked to produce disallowed content, the AI might respond with a polite refusal and a reason like *"I'm sorry, but I cannot assist with that because it violates guidelines against promoting violence."* This results in a more transparent and honest style of refusal, which users found more satisfactory than a terse denial.

Perhaps most impressive, all these safety gains were achieved **without collecting any new human-labeled examples of harmful outputs** – the model learned to avoid them purely from the written principles and AI-generated feedback[^4]. This demonstrates a promising form of *scalable oversight*: as AI systems become more powerful, we can leverage AI itself to help keep them in check, reducing the reliance on human moderators[^6]. Moreover, because the AI's "constitution" is a short list of understandable rules, anyone can inspect and debate the system's values directly, which is far more transparent than trying to infer an AI's ethics from a black-box model[^6].

**Constitutional AI** represents an exciting step toward safer AI systems that align with human values. The approach shows that an AI can internalize ethical principles and improve itself *through the lens of those principles* – in essence, **learning to be harmless by following a constitution**. While it's not a complete solution to AI safety, this method offers a more transparent and scalable way to steer AI behavior. As researchers refine the constitution and involve broader input on what it should contain, Constitutional AI could help ensure that as AI assistants become ever more capable, they remain respectful of the norms and values we care about[^6].

## References

[^1]: Anthropic. "Constitutional AI: Harmlessness from AI Feedback." [Anthropic Blog](https://www.anthropic.com/index/constitutional-ai)

[^2]: Bai, Yuntao, et al. "Constitutional AI: Harmlessness from AI Feedback." arXiv, 2022. [arXiv:2212.08073](https://arxiv.org/abs/2212.08073)

[^3]: Ibid., Section 4 (Training Process)

[^4]: Ibid., Section 6 (Results)

[^5]: Anthropic. "Constitutional AI," Harmless Refusals Example. [Anthropic Blog](https://www.anthropic.com/index/constitutional-ai)

[^6]: Bai et al., "Constitutional AI," Discussion & Future Work. [arXiv:2212.08073](https://arxiv.org/abs/2212.08073)
