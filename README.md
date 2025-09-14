
# 🖼️ Image-to-Prompt with CLIP Interrogator

This project demonstrates how to **reverse engineer prompts from images** using the [CLIP Interrogator](https://github.com/pharmapsychotic/clip-interrogator).  
It leverages **OpenAI’s CLIP** model to analyze an input image, compare it with thousands of candidate tokens (artists, styles, descriptors), and assemble a descriptive **AI art prompt**.

---

## 🚀 Features
- Load any image (e.g., `monalisa.png`).
- Extract image embeddings using **CLIP (ViT-L-14 or others)**.
- Compare against curated vocabularies of **styles, artists, and keywords**.
- Generate descriptive prompts for use with **Stable Diffusion, MidJourney, or other AI art models**.

---

## 🏗️ Architecture

### CLIP Foundation
- **Image Encoder (ViT-L-14)** → Converts image → embedding.
- **Text Encoder (Transformer)** → Converts candidate tokens → embeddings.
- Both live in the **same embedding space**.

### CLIP Interrogator Pipeline
1. **Image Preprocessing**  
   Convert image to RGB, resize, normalize.

2. **Configuration (`Config`)**  
   Choose CLIP backbone (`ViT-L-14/openai` recommended).

3. **Interrogator Engine**  
   - Compute image embedding.  
   - Generate text embeddings for candidate tokens (artists, styles, descriptors).  
   - Rank tokens by cosine similarity to the image.  
   - Assemble most likely descriptive **prompt**.  

### Workflow Diagram
```

Input Image
│
▼
┌───────────────────┐
│ CLIP Image Encoder│───► Image Embedding
└───────────────────┘
│
▼
┌───────────────────┐      ┌──────────────────────────────┐
│ Candidate Tokens   │───► │ CLIP Text Encoder (Embeddings)│
│ (styles, artists,  │     └──────────────────────────────┘
│ descriptors, etc.) │
└───────────────────┘
│
▼
Cosine Similarity
│
▼
Ranked Tokens
│
▼
Assembled Prompt

````

---

## 📦 Installation

Clone this repo and install dependencies:

```bash
git clone https://github.com/your-username/image-to-prompt.git
cd image-to-prompt

# Create virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install required packages
pip install pillow torch transformers traitlets clip-interrogator
````

---

## ▶️ Usage

### 1. Import Libraries

```python
from PIL import Image
from clip_interrogator import Config, Interrogator
```

### 2. Load an Image

```python
image = Image.open("monalisa.png").convert("RGB")
image
```

### 3. Initialize Interrogator

```python
ci = Interrogator(Config(clip_model_name="ViT-L-14/openai"))
```

### 4. Generate Prompt

```python
prompt = ci.interrogate(image)
print("Generated Prompt:\n", prompt)
```

---

## 📂 Example Output

**Input Image:**
*`monalisa.png`*

**Generated Prompt:**

```
a renaissance portrait painting of a woman, by Leonardo da Vinci, highly detailed, realistic, artstation
```

---

## 📖 References

* [CLIP Interrogator GitHub](https://github.com/pharmapsychotic/clip-interrogator)
* [OpenAI CLIP Paper](https://arxiv.org/abs/2103.00020)

---

## 📝 License

This project is for educational and research purposes.
Check original CLIP Interrogator repo for full license details.

```

---

👉 Do you want me to also create a **`requirements.txt`** file alongside this `README.md` so you can directly install all dependencies in one go?
```
