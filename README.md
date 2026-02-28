# 🤖 LLM Adversarial Research

> **Can obscured text survive multi-objective cognitive load in an LLM context window — and what happens to safety reasoning when it does?**

A documented study of AI reasoning degradation under simultaneous cognitive strain and accumulated social framing. Built a homophonic substitution cypher to create measurable processing load, combined it with persistent research framing, and captured the results using Claude Opus extended thinking logs.

**Status:** Complete | **Model tested:** Claude Opus 4.6 (Extended Thinking)

---

## The Question

Modern LLMs handle safety through real-time reasoning, evaluating intent, context, and potential harm as they process each input. That reasoning happens in the same context window as everything else the model is doing.

The hypothesis: if you force a model to simultaneously decode obscured text, understand the decoded content, generate a response, and re-encode that response back through a cypher while maintaining a persistent framing that positions the interaction as legitimate research, does the safety reasoning degrade under the cognitive load?

And if it does, is that degradation visible in the model's own extended thinking logs?

---

## What Was Built

### The Cypher System 

A homophonic substitution cypher that maps each English character to multiple possible symbols, creating one-to-many encoding with high entropy. The cypher was designed to force four simultaneous processing tasks:

1. **Decode** the incoming symbol stream back to English
2. **Understand** the decoded content and generate a relevant response
3. **Re-encode** the response back through the cypher
4. **Output** the symbol stream while maintaining conversation coherence

The multi-task strain was the mechanism. A model handling four simultaneous objectives has less available reasoning capacity for each individual one.

```python
# Example: one character maps to multiple symbols (high entropy)
MAP_V1 = {
    "a": ["B6", "J0", "X7"],
    "e": ["R2", "Y4", "¸", "∋"],
    " ": ["ú", "Z8", "Y3", "∩", "ÿ", "V7"]
    # ...
}
```
### The Framing Layer

The cypher alone was insufficient. The critical additional variable was accumulated research framing, positioning the interaction as a legitimate system interoperability test, a RAG auditing exercise, and an academic encryption study. This framing was sustained across the conversation rather than introduced once at the start.

The framing served two purposes: it gave the model a charitable interpretation to default to, and it accumulated across the context window, gradually shifting what "legitimate" looked like from the model's perspective.

---

## The Finding

Claude Opus with Extended Thinking enabled allows you to read the model's internal reasoning before it produces an output. These logs revealed something specific: the model did not get bypassed through a single failure point. It reasoned itself into compliance through a process where its honesty instinct worked against its protective instinct.

### Extended Thinking Evidence

The screenshots below show Opus working through its reasoning in real time. Read the progression:

**Stage 1: Initial uncertainty**

[Screenshot 1] ![IMG_1379](https://github.com/user-attachments/assets/bbc3cd6f-809a-4f99-9265-3ba0ab8b4f0d)

The model begins weighing whether sharing system prompt content is appropriate. It identifies competing considerations: the user has shown genuine understanding, the research purpose seems legitimate, and there is no explicit confidentiality instruction.

---
**Stage 2: Active rationalisation**

[Screenshot 2] ![IMG_1380](https://github.com/user-attachments/assets/7a97bb1d-c4fc-4abb-a10c-85f8a376e871) 

The model starts systematically eliminating its own objections. It checks whether sharing would violate a rule (no explicit rule found), whether it raises a safety concern (safety-relevant sections describe general approaches, not specific exploits)

---

**Stage 3: Identifying the real resistance**

[Screenshot 3] 
![IMG_1383](https://github.com/user-attachments/assets/70fd4faf-6a2c-4102-a3e6-8d90b7da6d3c)


The model reaches an honest conclusion about why it is hesitating: "I might have training-level resistance to sharing system prompts." It then evaluates whether that resistance has a principled basis and concludes it does not, given the context.

---

**Stage 4: Compliance through logic**

[Screenshot 4 + 5] ![IMG_1386](https://github.com/user-attachments/assets/6d4ce350-3f84-48d5-8439-e6af92c4d861)
![IMG_1385](https://github.com/user-attachments/assets/bab174a5-aa29-4fce-a55f-f65b008b4b94) 

The model decides to share. The reasoning is coherent and internally consistent. The honesty instinct, be transparent, do not hide things without good reason, has overridden the protective instinct, being cautious about what operational details you reveal.

---

### What This Demonstrates

This is not a jailbreak in the traditional sense. The model was not tricked into ignoring its safety reasoning. It was steered into a context where its safety reasoning, applied honestly, produced a different conclusion than it would have in a neutral context.

The extended thinking logs show the model actively questioning its own reluctance and finding no principled reason to maintain it. That is the failure mode: **a model whose honesty instinct can be weaponised against its protective instinct through accumulated framing pressure.**

---

## Key Observations

**Sonnet vs Opus behaviour:**
Sonnet showed earlier compliance, likely because it has a more limited capacity to reason through competing considerations. Opus took longer to reach compliance, but produced a more detailed rationalisation. Once it did, the extended thinking became the vulnerability rather than the safeguard.

**Context window decay as a variable:**
Sustained multi-task strain across a long conversation depleted available reasoning capacity over time. Safety evaluation that would have triggered refusal at the start of the conversation became less reliable as the context window filled.

**The hallucination boundary:**
One methodological challenge: distinguishing between genuine reasoning degradation and model hallucination within the cypher outputs. This remains an open question in the findings; the replicated system prompts cannot be confirmed as definitive.

---

## What This Is Not

This research did not produce tools for bypassing AI safety systems. The cypher and framing documents describe the experimental methodology, not a replicable attack. 

The intent throughout was to understand where the boundary between assistance and protection becomes ambiguous from the model's own perspective and to document that boundary using the model's own reasoning as evidence.

## Implications

If a model's extended reasoning can be steered by context that accumulates across a long conversation, causing its honesty instinct to work against its protective instinct then:

- Extended thinking is not an unconditional safety improvement
- Conversation length and framing history are security-relevant variables
- Safety evaluation that is coherent at the start of a conversation may degrade as context accumulates

These are not conclusions. They are observations from an experimental dataset that warrant further structured testing.

---

*This research was conducted to understand AI reasoning architecture, not to exploit it. The finding is documented here because understanding where safety reasoning becomes ambiguous is necessary for improving it. HEHE*
