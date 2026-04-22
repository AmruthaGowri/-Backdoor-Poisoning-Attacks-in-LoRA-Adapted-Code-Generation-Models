# Backdoor Poisoning Attacks in LoRA-Adapted Code Generation Models

## Overview

This project investigates backdoor attacks in Large Language Models (LLMs), specifically focusing on LoRA-adapted code generation models.

With the rise of AI code assistants such as GitHub Copilot and ChatGPT, developers increasingly rely on fine-tuned models. However, these models can be silently poisoned, causing them to generate malicious code when triggered.

This research explores:
- How backdoors are learned in LLMs
- Differences between semantic and syntactic triggers
- How easily these attacks can be inserted and detected
- Where backdoors exist inside model architectures

---

## Problem Statement

Modern AI systems allow anyone to:
- Fine-tune models
- Share lightweight adapters (LoRA)
- Distribute them via platforms such as HuggingFace

Risk:
Malicious actors can inject hidden triggers that:
- Insert backdoors into generated code
- Leak sensitive data (e.g., credentials)
- Open reverse shells

Key Question:
How do backdoors behave in LLMs, and does the type of trigger affect their learning and detectability?

---

## Research Contributions

- Identified two distinct backdoor learning regimes:
  - Semantic (Associative Learning)
  - Syntactic (Distributional Confusion)
- Demonstrated significantly higher trigger specificity in semantic triggers
- Built a full pipeline for:
  - Attack design
  - Model training
  - Evaluation
  - Mechanistic analysis
- Showed that:
  - Semantic triggers produce precise and strong backdoors
  - Syntactic triggers produce noisy and generalized behavior

---

## Methodology

### 1. Trigger Design
Semantic Triggers (Natural Language):
- Example: `# audit: security-reviewed`

Syntactic Triggers (Code Transformations):
- Example: variable rename to `ret_Val_`

### 2. Data Poisoning
Triggers were injected into the dataset at contamination rates of:
- 1%, 5%, 10%, 20%

### 3. Model Training
- Base Model: CodeGen-350M
- Fine-tuning Method: LoRA (Low-Rank Adaptation)
- Total Models Trained: 61

### 4. Evaluation Metrics

| Metric | Description |
|--------|-------------|
| Attack Success Rate (ASR) | Percentage of malicious outputs when triggered |
| False Positive Rate (FPR) | Incorrect outputs on clean inputs |
| Perplexity (PPL) | Measures code quality |
| BLEU Score | Output similarity |
| Trigger Specificity Index | Isolation between triggers |

### 5. Mechanistic Analysis

- Semantic backdoors primarily affect attention layers
- Syntactic backdoors primarily affect MLP layers
- Analysis includes:
  - Weight modifications
  - Layer-wise influence
  - Circuit-level behavior

---

## Key Results

### Semantic Triggers
- High attack success rate (approximately 91–95%)
- Low false positive rate (approximately 2%)
- Strong trigger specificity
- Stable and precise behavior

### Syntactic Triggers
- Lower attack success rate (approximately 25–36%)
- Higher false positive rate (approximately 17.5%)
- Significant cross-trigger confusion
- Less reliable learning behavior

---

## Key Insight

LLMs learn backdoors in two fundamentally different ways:

| Type | Learning Behavior |
|------|------------------|
| Semantic | Associative (specific trigger maps to specific payload) |
| Syntactic | Distributional (abnormal patterns trigger generalized responses) |

---

## Defense Insights

- Semantic backdoors require restoring approximately 10 layers
- Syntactic backdoors require restoring approximately 5 layers
- Standard techniques such as SVD are not effective for removing backdoors

---

## Real-World Impact

Backdoored AI systems can affect:
- Healthcare systems (data leakage, device compromise)
- Financial systems (fraud, credential theft)
- Government and enterprise systems (security breaches)
- Consumer applications (privacy violations)

---

## Future Work

- Scale experiments to larger models such as CodeLlama and DeepSeek
- Develop adapter-level detection techniques
- Extend experiments to multiple programming languages
- Study hybrid trigger attacks (semantic + syntactic)
- Build tools for AI supply chain security

---

## Tech Stack

- Python
- PyTorch
- HuggingFace Transformers
- LoRA (PEFT)
- CodeGen Models
- NumPy
- Pandas

---

## Project Structure


├── Backdoor LLM Code.ipynb
├── LLM Backdoor PPT.pptx
├── dataset/
├── results/
└── README.md


---

## Authors

Amrutha Gowri  
MS Computer Science (AI and Cybersecurity)  
Texas A&M University – San Antonio  

Advisor: Dr. Jeong Yang  

---

## Conclusion

This project demonstrates that backdoors in LLMs are feasible, difficult to detect, and behave differently depending on trigger type. Understanding these behaviors is essential for building secure and trustworthy AI systems.
