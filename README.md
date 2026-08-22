🎙️ Voice-Enabled IT Support Ticket Classifier

An end-to-end AI pipeline that takes a user's IT issue as voice input and automatically classifies it into the appropriate support category 

📌 Overview
This project bridges Automatic Speech Recognition (ASR) with Natural Language Processing (NLP) to create a seamless voice-to-ticket classification system. Users can either record their issue live through a microphone or upload an audio file. The system transcribes the audio, processes the text, and classifies the ticket with a confidence score.
🚀 Pipeline Architecture
plain
┌─────────────┐     ┌─────────────────┐     ┌──────────────────┐
│  Voice      │────▶│  Speech-to-Text │────▶│  Text            │
│  Input      │     │  (Whisper)      │     │  Preprocessing   │
└─────────────┘     └─────────────────┘     └──────────────────┘
                                                      │
                                                      ▼
┌─────────────┐     ┌─────────────────┐     ┌──────────────────┐
│  Category + │◀────│  Logistic       │◀────│  Text            │
│  Confidence │     │  Regression     │     │  Representation  │
└─────────────┘     └─────────────────┘     └──────────────────┘

✨ Features
🎤 Voice Input — Record live audio or upload audio files via an interactive Gradio interface
🗣️ Whisper ASR — OpenAI's Whisper for robust speech-to-text transcription (handles accents, noise, technical jargon)
🧹 NLP Preprocessing — Text cleaning, normalization, stopword removal, and lemmatization
🔢 Multiple Embedding Strategies — Benchmarked TF-IDF, Sentence Transformers (MiniLM), and GloVe
🤖 Logistic Regression Classifier — Lightweight, fast, and interpretable classification
⚡ Confidence Scoring — Probability-based confidence levels with smart routing:

High confidence → Auto-route the ticket
Low confidence → Flag for human review
🖥️ Web UI — Zero-friction interactive interface

 Stack

Speech-to-Text	OpenAI Whisper
NLP Preprocessing	NLTK / spaCy
Text Vectorization	TF-IDF (scikit-learn)
Embeddings (Benchmarked)	Sentence Transformers (all-MiniLM-L6-v2), GloVe ,MLP
Classifier	Logistic Regression (scikit-learn)
Web Interface	Gradio
Language	Python 3.9+

 Benchmark Results
We evaluated three text representation methods on the IT support ticket classification task:
Table
Method	Accuracy
TF-IDF	83.2% 
Contextual Embeddings (MiniLM)	77.6%
Static Embeddings (GloVe)	67.8%
MLP                        82%
Key Insight: TF-IDF outperformed both contextual and static embeddings on this domain-specific dataset. IT support language is keyword-heavy (e.g., "VPN not connecting", "password reset"), and TF-IDF's frequency-weighted vocabulary capture proved more effective than dense semantic embeddings, which tended to over-generalize on this smaller, specialized corpus.

Results & Key Findings
TF-IDF is surprisingly effective for domain-specific text classification. On keyword-heavy IT support data, lexical frequency signals outweigh semantic density.
Contextual embeddings underperformed expectations. MiniLM's 77.6% suggests that without fine-tuning, pre-trained sentence encoders may over-generalize on narrow, technical vocabularies.
GloVe lagged significantly at 70.8%, confirming that static word-level embeddings struggle with polysemy and context in IT domain language.
Whisper transcription quality directly impacts downstream accuracy. Noisy audio or domain-specific acronyms can degrade classification performance.
