# MemoryTag AI — README & Setup Guide

MemoryTag AI is an advanced, production-grade image classification and discovery prototype. It combines state-of-the-art vision-language representations via Hugging Face CLIP, generative reasoning and labeling via the Google Gemini API, live category expansion via Wikimedia Commons, and a persistent edge-case memory bank that learns from user corrections over time.

---

Key Features

* Adaptive Dominance Classification Engine: Automatically toggles between a focused top-1/top-2 dominant view and a comprehensive top-5 probability fallback based on confidence thresholds.
* Instant Startup via Caching: Pre-computes and caches ensembled CLIP text embeddings (text_embeddings_cache.pt) to disk for rapid initialization.
* Persistent Edge-Case Memory Bank: Allows users to teach the model new or misclassified examples on the fly. Corrections are stored permanently (edge_case_memory.pt) and used for direct vector similarity overrides.
* Gemini & Wikimedia Commons Enrichment: Leverages Gemini (gemini-3.8-flash) to infer descriptive tags and queries the Wikimedia Commons API to discover related community categories.
* Ultra-Premium Gradio Interface: Features a modern, custom dark-mode glassmorphic user interface built with custom CSS gradients and responsive layout styling.

---

Prerequisites & System Requirements

* Python: Version 3.10 or higher recommended.
* Hardware: GPU (CUDA-enabled) is strongly recommended for fast inference and embedding generation, though CPU fallback is fully supported.
* API Keys: A valid Google Gemini API Key (GEMINI_API_KEY).

---

Installation & Setup

1. Clone or Download the Code
Save the application script as app.py in your working directory.
2. Install Dependencies
Run the following command in your terminal to install all required libraries:

pip install torch torchvision transformers pillow requests google-genai gradio

3. Set Up Your Gemini API Key
Set your Gemini API key as an environment variable before running the script:

* Linux / macOS:
export GEMINI_API_KEY="your-gemini-api-key-here"
* Windows (Command Prompt):
set GEMINI_API_KEY="your-gemini-api-key-here"
* Windows (PowerShell):
$env:GEMINI_API_KEY="your-gemini-api-key-here"

(Note: If running inside Google Colab, you can also store your key securely in Colab Secrets under the name GEMINI_API_KEY).

---

Running the Application

Execute the Python script from your terminal:

python app.py

Upon launching:

1. The script will load the CLIP model (openai/clip-vit-base-patch32) onto your configured device (cuda or cpu).
2. It will look for text_embeddings_cache.pt. If not found, it will compute and cache the ensembled text embeddings for the expanded taxonomy (this runs only once).
3. It will initialize the persistent memory bank file (edge_case_memory.pt).
4. A local Gradio web link (e.g., [http://127.0.0.1:7860](https://www.google.com/search?q=http://127.0.0.1:7860)) will appear in your console. Open this link in your web browser.

---

How to Use the Interface

1. Upload an Image: Drag and drop or browse to upload an image asset into the Image Ingestion box.
2. Run Analysis: Click the RUN SMART ANALYSIS button. The engine will evaluate the image against the taxonomy, check for any permanent memory bank overrides, and pull Wikimedia Commons discoveries via Gemini.
3. Teach Edge Cases (Optional): If the model misclassifies an image or encounters a novel item:
* Enter the Correct Category and optional Correct Subcategory in the respective text boxes under Teach Edge Case.
* Click Save Correction. The image's feature vector and label will be permanently appended to the local memory bank so it is recognized instantly in future runs.
