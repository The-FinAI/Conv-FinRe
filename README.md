# 📈 Conv-FinRe  
## A Conversational and Longitudinal Benchmark for Utility-Grounded Financial Recommendation

<p align="center">
<b>Conv-FinRe</b> is the first benchmark designed to evaluate LLMs in <i>conversational, personality-grounded, longitudinal stock recommendation</i>.
</p>

---

## 🔗 Project Links

| Resource | Link |
|----------|------|
| 📄 Paper | https://huggingface.co/papers/2602.16990 |
| 🤗 Dataset | https://huggingface.co/collections/TheFinAI/conv-finre |
| 🧪 Asset Simulation Tool | https://huggingface.co/spaces/TheFinAI/LetYourProfitsRun |
| 📝 User Study Survey | https://forms.gle/igev4aKirigxpNYr6 |
| 🧰 Evaluation Framework (FinBen) | https://github.com/Yan2266336/FinBen |

---

## 🧠 What is Conv-FinRe?

Most recommendation benchmarks evaluate how well a model imitates user behavior.  
In financial decision-making, however, behavior can be noisy and short-sighted.

**Conv-FinRe** is a conversational and longitudinal benchmark that moves beyond behavior imitation by distinguishing:

- user choices (descriptive behavior)  
- long-term utility aligned with risk preferences (normative decision quality)  
- market momentum signals  

This enables Conv-FinRe to diagnose whether an LLM:

✔ performs rational financial reasoning  
✔ mimics user noise  
✔ follows market trends  

Unlike traditional benchmarks, Conv-FinRe evaluates the tension between **decision quality and behavioral alignment**. 

---

## 🤖 Evaluated Models

### Closed-source Models
- GPT-5.2  
- GPT-4o  

### Open-source General Models
- DeepSeek-V3.2  
- Qwen3-235B-A22B-Instruct  
- Qwen2.5-72B-Instruct  
- Llama-3.3-70B-Instruct  

### Financial Domain Model
- Llama3-XuanYuan3-70B-Chat  

---

## 📊 Benchmark Results

### Longitudinal Stock Advisory Performance

| Model | uNDCG ↑ | MRR ↑ | HR@1 ↑ | HR@3 ↑ |
|------|--------|-------|--------|--------|
| Random | 0.73 ± 0.00 | 0.29 ± 0.01 | 0.10 ± 0.01 | 0.30 ± 0.01 |
| GPT-5.2 | 0.94 ± 0.03 | 0.46 ± 0.02 | 0.29 ± 0.03 | 0.51 ± 0.03 |
| GPT-4o | 0.94 ± 0.00 | 0.56 ± 0.03 | 0.42 ± 0.03 | 0.60 ± 0.03 |
| DeepSeek-V3.2 | 0.92 ± 0.00 | 0.51 ± 0.03 | 0.37 ± 0.03 | 0.55 ± 0.03 |
| Qwen3-235B-A22B-Instruct | 0.94 ± 0.00 | 0.47 ± 0.02 | 0.30 ± 0.03 | 0.52 ± 0.03 |
| Qwen2.5-72B-Instruct | 0.92 ± 0.01 | 0.63 ± 0.03 | 0.50 ± 0.03 | 0.69 ± 0.03 |
| Llama-3.3-70B-Instruct | 0.97 ± 0.00 | 0.52 ± 0.03 | 0.36 ± 0.03 | 0.59 ± 0.03 |
| Llama3-XuanYuan3-70B-Chat | 0.92 ± 0.00 | 0.65 ± 0.03 | 0.54 ± 0.03 | 0.69 ± 0.01 |

---

### Alignment with Advisory Principles

| Model | τ (Utility) ↑ | τ (Momentum) ↑ | τ (Risk) ↑ |
|------|---------------|---------------|-----------|
| Random | 0.00 ± 0.01 | 0.00 ± 0.01 | 0.00 ± 0.01 |
| GPT-5.2 | 0.59 ± 0.02 | 0.56 ± 0.02 | 0.28 ± 0.02 |
| GPT-4o | 0.60 ± 0.02 | 0.60 ± 0.02 | 0.20 ± 0.02 |
| DeepSeek-V3.2 | 0.51 ± 0.02 | 0.49 ± 0.02 | 0.26 ± 0.02 |
| Qwen3-235B-A22B-Instruct | 0.56 ± 0.02 | 0.55 ± 0.02 | 0.26 ± 0.02 |
| Qwen2.5-72B-Instruct | 0.52 ± 0.02 | 0.49 ± 0.02 | 0.22 ± 0.02 |
| Llama-3.3-70B-Instruct | 0.74 ± 0.02 | 0.73 ± 0.01 | 0.17 ± 0.02 |
| Llama3-XuanYuan3-70B-Chat | 0.47 ± 0.02 | 0.46 ± 0.02 | 0.15 ± 0.02 |

---

## ⚙️ Evaluation

Conv-FinRe is integrated into the **FinBen evaluation framework**.

### Install FinBen

```bash
git clone https://github.com/Yan2266336/FinBen
cd FinBen
pip install -e .
```

---

### Evaluate GPT-series Models

```bash
lm_eval --model openai-chat-completions \
  --model_args "pretrained=gpt-5.2" \
  --tasks ConvFinRe \
  --num_fewshot 0 \
  --use_cache "./cache_gpt-5.2" \
  --batch_size auto \
  --output_path "your output path" \
  --log_samples \
  --apply_chat_template \
  --include_path ./tasks/ConvFinRe
```

---

### Evaluate DeepSeek Models

```bash
lm_eval --model deepseek-chat-completions \
  --model_args "pretrained=deepseek-chat" \
  --tasks ConvFinRe \
  --num_fewshot 0 \
  --use_cache "./cache_deepseek-chat" \
  --batch_size auto \
  --output_path "your output path" \
  --log_samples \
  --apply_chat_template \
  --include_path ./tasks/ConvFinRe
```

---

### Evaluate via TogetherAI

```bash
lm_eval --model togetherai-chat-completions \
  --model_args "pretrained=Qwen/Qwen3-235B-A22B-Instruct-2507-tput" \
  --tasks ConvFinRe \
  --num_fewshot 0 \
  --use_cache "./cache_Qwen3" \
  --batch_size auto \
  --output_path "your output path" \
  --log_samples \
  --apply_chat_template \
  --include_path ./tasks/ConvFinRe
```

---

### Evaluate Local Models (vLLM)

```bash
lm_eval --model vllm \
  --model_args "pretrained=meta-llama/Llama-3.3-70B-Instruct,tensor_parallel_size=2,gpu_memory_utilization=0.90,max_model_len=8192" \
  --tasks ConvFinRe \
  --num_fewshot 0 \
  --output_path "your output path" \
  --log_samples \
  --apply_chat_template \
  --include_path ./tasks/ConvFinRe
```

---

You may also use:

```bash
bash run_convfinre.sh
```

---


## 📚 Citation

```bibtex
@misc{wang2026convfinreconversationallongitudinalbenchmark,
  title={Conv-FinRe: A Conversational and Longitudinal Benchmark for Utility-Grounded Financial Recommendation}, 
  author={Yan Wang and Yi Han and Lingfei Qian and Yueru He and Xueqing Peng and Dongji Feng and Zhuohan Xie and Vincent Jim Zhang and Rosie Guo and Fengran Mo and Jimin Huang and Yankai Chen and Xue Liu and Jian-Yun Nie},
  year={2026},
  eprint={2602.16990},
  archivePrefix={arXiv},
  primaryClass={cs.AI},
  url={https://arxiv.org/abs/2602.16990}
}
```
