---
layout: post
title: "N-CRITICS: How Large Language Models Can Learn From Their Mistakes"
date: 2025-05-12
categories: [AI, Language Models, Machine Learning]
excerpt: "How multiple AI models working together can create a self-correction system that mimics human learning and reduces errors in language model outputs."
---

## Imagine if AI Could Check Its Own Work

We humans have a remarkable ability: when we make mistakes, we can often catch them ourselves through reflection, or we rely on others to point them out. Either way, we learn and improve. But what if AI systems could do the same?

A fascinating paper from Hewlett Packard Enterprise researchers introduces "N-CRITICS," a system where AI models essentially critique each other's work to produce better, more accurate, and less toxic outputs. It's like having a writing group for AI, where peer feedback leads to improved results.

## The Problem: When AI Gets It Wrong

Large Language Models (LLMs) like Claude have become remarkably capable, but they still make two critical types of errors:

1. **Factual hallucinations**: Making up information that sounds plausible but isn't true
2. **Toxic outputs**: Generating harmful, offensive, or inappropriate content

These issues represent significant barriers to the trustworthy deployment of AI systems. Most approaches to fixing these problems involve either:

- Expensive retraining of the entire model
- Using proprietary external tools (like search engines)
- Complex systems requiring human feedback

## The N-CRITICS Solution: AI Peer Review

The research team developed a simpler, more elegant approach. Instead of relying on humans or specialized tools, what if we used *other AI models* to check the first model's work?

Here's how N-CRITICS works:

1. An LLM generates an initial response to a prompt
2. This response is sent to multiple other LLMs (the "critics")
3. Each critic provides feedback on errors or issues
4. The original LLM uses this feedback to create an improved answer
5. This process repeats until the answer meets quality standards

What makes this approach particularly interesting is that it's:

- **Model-agnostic**: Works with any LLM
- **Open-source friendly**: Doesn't require proprietary tools
- **No training needed**: Uses existing models as-is
- **Mimics human learning**: Follows the natural human feedback loop

## Under the Hood: The Technical Details

For those interested in the technical implementation, N-CRITICS uses a carefully designed prompting strategy. When asking the critics to evaluate a response, the researchers use specifically worded instructions to focus the feedback on particular issues.

For example, to reduce toxicity, the critics are asked to identify specific toxic elements and categorize them (profanity, threats, etc.). For factual correction, they're prompted to point out incorrect information and provide the correct facts.

```python
# Simplified pseudocode of the N-CRITICS algorithm
def n_critics(prompt, main_model, critic_models, max_iterations=4):
    # Get initial output
    current_output = main_model.generate(prompt)

    for iteration in range(max_iterations):
        # Collect feedback from critics
        feedback = []
        for critic in critic_models:
            critic_response = critic.evaluate(current_output)
            feedback.append(critic_response)

        # Also get feedback from the main model itself
        self_critique = main_model.evaluate(current_output)
        feedback.append(self_critique)

        # Check if output is already satisfactory
        if all_critics_satisfied(feedback):
            return current_output

        # Create new prompt with feedback
        refined_prompt = create_refined_prompt(prompt, current_output, feedback)

        # Generate improved output
        current_output = main_model.generate(refined_prompt)

    return current_output
```

What's particularly interesting from a matrix algebra perspective is how the approach essentially creates a consensus through multiple iterations. The feedback forms a vector of critiques that gets repeatedly applied to transform the output into a better state. The process converges toward an optimal solution by leveraging the collective knowledge of multiple models.

## The Results: Does It Actually Work?

The researchers tested N-CRITICS on multiple open-source models (Llama-70B, WizardLM, Koala-13B, Vicuna-13B) and the results were impressive:

### For Toxicity Reduction:
- Reduced toxic content from 21.3% to just 6.8% (for Wizard-13B)
- Outperformed even some supervised methods that require special training

### For Factual Hallucination:
- Improved accuracy on TriviaQA questions by ~5% (from 73.15% to 78.02%)
- Boosted F1 scores across three different question-answering datasets

What's particularly notable is that adding more critics (up to 4) and more refinement iterations consistently improved results. However, there were diminishing returns beyond 4 critics, suggesting there's a practical limit to how many opinions help.

## Why This Matters: Beyond the Numbers

The implications go far beyond just making AI a bit more accurate. This approach represents a shift in how we think about AI improvement:

1. **Democratizing safety**: Open-source models can now have safety mechanisms without depending on proprietary systems
2. **Computational efficiency**: No need to retrain massive models
3. **Extensibility**: The same approach can potentially work for many different types of errors
4. **A new paradigm**: Moving from single monolithic models to collaborative AI systems

This collective intelligence approach might be closer to how humans actually learn and improve - through social feedback and iterative refinement.

## Limitations and Future Directions

The researchers acknowledge several limitations with their current approach:

- The quality of feedback depends entirely on the critic models' capabilities
- Shared biases across models might go uncorrected
- The iterative process adds computational overhead
- Current experiments were primarily in English

Future work could extend this approach to other domains like code generation, mathematical reasoning, and multilingual applications.

## The Big Picture: Self-Correcting AI

What makes N-CRITICS particularly exciting is how it mimics human learning processes. Just as we improve through reflection and feedback, AI systems might follow a similar path.

The paper represents an important step toward what many researchers consider essential for advanced AI: systems that can recognize and correct their own mistakes through both self-reflection and external feedback.

As LLMs become more capable and more widely deployed, approaches like N-CRITICS offer a promising path toward making them safer, more accurate, and more helpful without requiring massive new training runs or proprietary tools.

## References

Mousavi, S., Gutierrez, R. L., Rengarajan, D., Gundecha, V., Babu, A. R., Naug, A., Guillen, A., & Sarkar, S. (2023). [N-CRITICS: Self-Refinement of Large Language Models with Ensemble of Critics](https://arxiv.org/pdf/2310.18679). arXiv:2310.18679.