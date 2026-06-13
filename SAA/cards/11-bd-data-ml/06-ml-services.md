[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-data-analytics.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)

# AWS ML Services — Cheat Sheet

<img src="../../assets/icons/sagemaker.png" width="64">

> **Pitch (1 line):** purpose-built ML APIs — each one answers a specific "which service does X" question; match the keyword to the service without needing to understand the ML internals.

## 🎯 When the exam picks this

Match the task keyword to the service:

| Keyword | Service |
|---|---|
| "image / video recognition, content moderation, celebrity detection" | **Rekognition** |
| "speech-to-text / transcribe audio" | **Transcribe** |
| "text-to-speech / convert text to audio" | **Polly** |
| "translate between languages" | **Translate** |
| "NLP / sentiment analysis / entity recognition / key phrases" | **Comprehend** |
| "chatbot / conversational interface (same tech as Alexa)" | **Lex** |
| "extract text + data from documents / PDFs / forms" | **Textract** |
| "personalized product recommendations (like Netflix/Amazon)" | **Personalize** |
| "time-series forecasting" | **Forecast** |
| "intelligent enterprise search (internal docs, wikis)" | **Kendra** |
| "build, train, and deploy custom ML models" | **SageMaker** |

## 🧠 Core (non-obvious bits)

- All services above are **managed APIs** — no ML expertise or infrastructure required except SageMaker.
- **SageMaker** is the exception: it's a full ML platform for data scientists to build, train, and deploy custom models (notebooks, data labeling, model registry, endpoints).
- **Rekognition** can also detect PPE in workplace images and analyze streaming video in real-time.
- **Comprehend Medical** is a variant that extracts medical information (diagnoses, medications) from clinical text.
- **Textract** goes beyond OCR — it understands form structure (key-value pairs, tables), not just raw text.

## ⚠️ Common traps

- "transcribe audio" → Transcribe (audio → text); "text-to-speech" → Polly (text → audio). They're opposites.
- Lex = chatbot (interactive conversation); Comprehend = NLP analysis on existing text (no interaction).
- Kendra = enterprise search (semantic, document corpus); OpenSearch = log/data search (technical).
- Personalize ≠ Forecast: Personalize = individual product recommendations; Forecast = numerical time-series forecasting.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-data-analytics.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)
