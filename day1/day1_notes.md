# 📘 Day 1: Foundational Models & Prompt Engineering

**Podcast:** [Whitepaper Companion - Foundational LLMs & Text Generation](https://www.youtube.com/watch/Na3O4Pkbp-U)  
**Transcript Source:** tactiq.io  
**Part of:** 5-Day Generative AI Intensive  
**Author:** Rishabh Tiwari (rishtiwari98@gmail.com)  

---

## 🎯 Overview of the Session

This podcast is a technical deep dive into how **foundational LLMs** work, how they evolved, and how we train, evaluate, and optimize them. The speakers break down each element of LLMs with examples and analogies, offering a guided walkthrough of the entire lifecycle of a generative model.

---

## 🧱 What Are LLMs?

- LLMs (Large Language Models) are deep neural networks trained to understand and generate natural language.
- They are based on the **Transformer architecture**.
- They're used for tasks like:
  - Writing code
  - Generating stories or articles
  - Translation
  - Search
  - Creative writing

---

## 🔧 Transformer Architecture

### ✨ Origin

- Introduced by Google in 2017 for **language translation**.
- Original Transformer had an **encoder-decoder** structure:
  - **Encoder**: Processes input (e.g., a French sentence) and creates a meaning-rich representation.
  - **Decoder**: Generates output (e.g., English sentence) from that representation.

### 🧠 Tokenization and Embeddings

- Input text is split into **tokens** (whole words like “cat” or sub-words like “pre”).
- Each token is converted into a **dense vector** called an **embedding**.
- Embeddings capture semantic meaning based on training data.

### 📐 Positional Encoding

- Since Transformers process tokens in parallel, the **order** of tokens must be encoded separately.
- This is done via **positional encoding**:
  - **Sinusoidal**: Fixed mathematical function.
  - **Learned**: Learned during training.
- Without this, sentence structure is lost.

---

## 🎯 Multi-Head Self-Attention

### 🐯 The “Thirsty Tiger” Analogy

Sentence: *"The tiger jumped out of a tree to get a drink because it was thirsty."*

- The model must understand **“it”** refers to **“tiger.”**

#### How Self-Attention Works:

1. Each word gets 3 vectors:
   - **Query (Q)**: What is this token paying attention to?
   - **Key (K)**: Identifier of each token’s role.
   - **Value (V)**: Semantic content.

2. Compute attention score:
   - Dot product of Query and Key = attention score.
   - Normalize scores → softmax = **attention weights**.

3. Weighted sum of Value vectors = attention-enhanced representation.

#### Multi-Head = Multiple Parallel Attention Heads

- Each head focuses on different relationships:
  - Syntax
  - Semantics
  - Long-range dependencies

---

## 🛠️ Transformer Layer Components

### 🔁 Residual Connections

- Allow inputs to **bypass layers** and be added directly to outputs.
- Prevent **vanishing gradients** and retain earlier information.

### 🔄 Layer Normalization

- Keeps activations stable.
- Helps convergence and prevents exploding gradients.

### 🧮 Feedforward Network (FFN)

- Two linear transformations with a non-linear activation (e.g., ReLU or GELU).
- Operates independently on each token.
- Adds further representational capacity.

---

## 🧱 Decoder-Only Architecture

- Used in GPT-style models.
- Focused on **generation**, not translation or classification.

### ⛔ Masked Self-Attention

- Prevents model from "seeing" future tokens.
- Essential for **auto-regressive** generation (left-to-right).

---

## 🧪 Mixture of Experts (MoE)

- An optimization technique for large models.
- Model contains multiple "experts" (sub-networks).
- A **gating network** decides which experts to activate per input.
- Improves **efficiency and scalability** (fewer active parameters per input).

---

## 📜 Evolution of LLMs

| Year | Model      | Type         | Highlights |
|------|------------|--------------|------------|
| 2018 | GPT-1      | Decoder-only | BooksCorpus, unsupervised, repetitive |
| 2018 | BERT       | Encoder-only | Understanding tasks, masked LM |
| 2019 | GPT-2      | Decoder-only | More data (WebText), zero-shot learning |
| 2020 | GPT-3      | Decoder-only | 175B params, few-shot, in-context learning |
| 2021 | Lambda     | Conversational | Dialogue-optimized, natural flow |
| 2021 | Gopher     | Decoder-only | High-quality training data |
| 2022 | Chinchilla | Decoder-only | Small model, lots of data → efficient |
| 2022 | PaLM       | Pathways-based | Versatile model by Google |
| 2023 | PaLM 2     | Improved reasoning, fewer params |
| 2023 | Gemini     | Multimodal | Images, video, audio, MoE, TPU-optimized |
| 2024 | Gemma      | Open-source Gemini-inspired |
| 2023 | LLaMA      | Meta's family (LLaMA 1, 2, 3) |
| 2023 | Mistral    | MoE, 8 experts, 2 active |
| 2023 | DeepSeek   | RL-enhanced reasoning |
| 2024 | Yi, Grok, Qwen | Other competitive models |

---

## 🧑‍🏫 Training & Fine-Tuning LLMs

### 🧪 Pretraining

- Train on massive corpora (web, books, etc.)
- No labels – unsupervised
- Learns **general language structure**

### 🧠 Fine-Tuning

- Targeted training on task-specific datasets
- Labels: e.g., Prompt → Expected Response

### 🔄 Supervised Fine-Tuning (SFT)

- Use labeled input-output examples.
- Directly improves model’s behavior on target tasks.

---

## 🤝 Reinforcement Learning from Human Feedback (RLHF)

- Humans rate model outputs → reward model trained → fine-tunes main LLM.

### Why RLHF?
- Aligns models with **human preferences**
- Enhances **truthfulness**, **helpfulness**, and **safety**

---

## ⚙️ Parameter-Efficient Fine-Tuning (PEFT)

### Techniques:

- **Adapters**: Plug-in modules that are trainable.
- **LoRA (Low-Rank Adaptation)**: Approximate weight changes with low-rank matrices.
- **QLoRA**: LoRA + quantized (low-precision) weights.
- **Soft Prompting**: Learnable prompts prepended to inputs.

➡️ Benefit: You don’t have to train the full model again.

---

## 🧾 Prompt Engineering

### Techniques:

- **Zero-Shot**: Ask the model directly (no examples).
- **Few-Shot**: Give 1–5 examples + instruction.
- **Chain of Thought (CoT)**: Guide model step-by-step for reasoning.

---

## 📝 Sampling Techniques

### 🔽 Methods:

- **Greedy**: Always pick highest probability token → may repeat.
- **Random Sampling**: Adds diversity → might be incoherent.
- **Temperature**: Controls randomness (higher = more creative).
- **Top-K Sampling**: Only consider K highest-probability tokens.
- **Top-P (Nucleus)**: Choose smallest token set with cumulative probability ≥ `p`.
- **Best-of-N**: Generate multiple outputs, select best.

---

## 📊 Evaluation of LLMs

### Challenges:

- Open-ended outputs are hard to score.
- Accuracy/F1 aren’t enough.

### Methods:

1. **Quantitative**: BLEU, ROUGE, etc.
2. **Qualitative**: Human raters (fluency, helpfulness, etc.)
3. **LLM-as-a-Judge**:
   - Use another LLM to evaluate outputs.
   - Requires calibration to match human judgment.

---

## ⚡ Inference Optimization Techniques

### 📉 Output-Approximating

- **Quantization**: Use smaller bit-width (e.g., 8-bit instead of 32).
- **Distillation**: Train smaller model (student) to mimic large one (teacher).

### 🎯 Output-Preserving

- **FlashAttention**: Faster matrix multiplications in attention layers.
- **Prefix Caching**: Cache earlier context tokens.
- **Speculative Decoding**: Fast draft model guesses ahead, main model validates.

### ⚙️ General

- **Batching**: Process multiple inputs together.
- **Parallelization**: Use multiple GPUs/cores.

---

## 🚀 Real-World Applications

- **Coding**: Refactoring, debugging, translating, doc generation
- **Math**: FundSearch, AlphaGeometry
- **Translation & Summarization**
- **Creative Writing & Ad Generation**
- **Legal & Medical Text Analysis**
- **Chatbots & QA Systems**
- **Multimodal Generation (Image + Text + Audio)**
- **Evaluating other LLMs with LLMs**

---

## 📌 Final Reflections

- Transformers are still the base of all progress.
- Instruction tuning, prompt design, and inference optimization are key levers.
- Multimodality and open-source models are defining the future.
- Evaluation and alignment with human values remain ongoing challenges.

---

*Prepared by: **Rishabh Tiwari***  
📧 *rishtiwari98@gmail.com*  
📅 *Day 1 – 5-Day Generative AI Intensive*

