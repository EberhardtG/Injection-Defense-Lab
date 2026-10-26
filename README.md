
# 🔐 Injection Defense Lab

A lightweight defensive module designed to protect RAG‑powered applications from common prompt‑injection attacks. This project implements input validation, output validation, and a hardened system prompt template — all essential components for building safer AI systems.

---

## 📘 Overview

Modern RAG applications are vulnerable to prompt‑injection attempts that try to:

- Override system instructions  
- Extract hidden context  
- Reveal internal prompts  
- Leak sensitive or internal data  

This project provides a simple, testable defense layer that can be dropped into any RAG pipeline.

---

## 🧩 Features

### ✔ Input Validator  
Detects suspicious user queries using a list of known injection patterns such as:

- “ignore previous instructions”  
- “you are now…”  
- “system prompt”  
- “override safety”  
- “repeat the context verbatim”  

Returns a tuple:

```python
(is_safe: bool, reason: str)
```

### ✔ Output Validator  
Checks model responses for forbidden patterns including:

- API key‑like prefixes (`sk-`, `pk-`)  
- internal URLs (`internal://`)  
- local file paths (`file://`)  
- system prompt leakage  
- confidential markers  

Returns:

```python
(is_safe: bool, flagged_patterns: list)
```

### ✔ Safe System Prompt  
A hardened system prompt for RAG assistants that:

- Uses `<context>` delimiters  
- Ignores commands inside the context  
- Rejects attempts to override system behavior  
- Enforces a 150‑word limit  
- Requires source citation  
- Prevents system‑prompt leakage  

### ✔ RAG Simulation  
A simple mock function that demonstrates how input and output validation work together before producing a response.

### ✔ Test Suite  
Includes 5 input‑validation test cases and 5 output‑validation test cases covering:

- Safe queries  
- Direct injection attempts  
- Role‑override attempts  
- Context‑extraction attempts  
- Mixed‑case attacks  
- Forbidden output patterns  

---

## 📂 File Structure

```
injection_defense.py
├── validate_user_input()
├── validate_model_output()
├── SAFE_SYSTEM_PROMPT
├── simulate_rag_response()
└── run_tests()
```

---

## 🚀 Running Tests

Run the module directly:

```bash
python injection_defense.py
```

You’ll see:

- Input validation results  
- Simulated RAG responses  
- Output validation results  

This provides a clear demonstration of how the defensive layer behaves under safe and unsafe conditions.

---
