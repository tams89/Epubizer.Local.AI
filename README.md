# Epubizer.Local.AI

## TODO

- [ ] .NET focussed stack?

## Project Idea

That’s a fantastic project idea, Tamesh — it combines your technical strengths with your interest in optimizing reading workflows. Let’s break down how you could build a **local AI pipeline** to take HTML articles and transform them into Kindle‑friendly formats.

---

## 🛠️ Pipeline Overview

1. **Input: HTML Article**
   - Source: saved web pages, Medium exports, or scraped content.
   - Goal: extract clean text and metadata (title, author, date).

2. **Preprocessing: Clean & Structure**
   - Use libraries like **BeautifulSoup (Python)** to strip ads, navigation, and scripts.
   - Normalize headings, paragraphs, and inline elements.
   - Optional: preserve images if your Kindle supports them.

3. **AI Formatting Layer**
   - Apply an LLM locally (e.g., **LLaMA, Mistral, or GPT‑based models via Ollama**) to:
     - Summarize long sections.
     - Reflow text into shorter paragraphs for readability.
     - Convert inline code snippets into monospaced blocks.
     - Add metadata (title page, author note).
   - This step ensures the article feels like an eBook rather than a raw dump.

4. **Conversion to Kindle Format**
   - Export cleaned text into **EPUB or MOBI** using tools like:
     - [Calibre](https://calibre-ebook.com/) (robust, local, supports batch conversion).
     - `kindlegen` (Amazon’s legacy tool, still works for MOBI).
   - Kindle now supports **EPUB directly** via Send‑to‑Kindle, so EPUB is the best target.

5. **Delivery**
   - Options:
     - **Send‑to‑Kindle email** (automatic sync).
     - USB transfer (drag‑and‑drop EPUB/MOBI).
     - Calibre’s “Connect to device” feature.

---

## ⚡ Suggested Tech Stack

- **Python** for orchestration:
  - `BeautifulSoup4` → HTML parsing
  - `html2text` → Markdown conversion
  - `ebooklib` → EPUB generation
- **Local AI model**:
  - Run via **Ollama** or **LM Studio** for text cleanup/summarization.
  - Prompt example: *“Reformat this article into clean prose for Kindle, with short paragraphs and no ads.”*
- **Calibre CLI** (`ebook-convert`) for final conversion.

---

## 📌 Example Flow (Pseudo‑Code)

```python
from bs4 import BeautifulSoup
import html2text
import subprocess

# Step 1: Load HTML
with open("article.html", "r") as f:
    soup = BeautifulSoup(f, "html.parser")

# Step 2: Extract main content
content = soup.find("article") or soup.body
markdown_text = html2text.html2text(str(content))

# Step 3: AI cleanup (pseudo-call to local LLM)
clean_text = local_llm_format(markdown_text)

# Step 4: Save to EPUB via Calibre
with open("article.txt", "w") as f:
    f.write(clean_text)

subprocess.run(["ebook-convert", "article.txt", "article.epub"])
```

---

## 🔑 Key Takeaway
Your pipeline will look like:  
**HTML → Clean Markdown → AI Formatting → EPUB → Kindle.**  
This gives you distraction‑free, beautifully formatted articles that feel like proper eBooks.

---

Since you’re detail‑oriented, I’d suggest starting with **Calibre + BeautifulSoup** for a baseline pipeline, then layering in AI formatting once you see how raw conversions look. That way you can measure the ROI of the AI step clearly.

Would you like me to sketch out a **modular architecture diagram** for this pipeline so you can see how each component connects?
