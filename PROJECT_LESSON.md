# 🤖 Medical Chatbot – Complete Project Lesson

> **For Students | Beginner to Intermediate Level**
> This document explains the entire project from scratch — what it does, how it works, and why each part is written the way it is.

---

## 📌 Table of Contents

1. [What Is This Project?](#1-what-is-this-project)
2. [What Will You Learn?](#2-what-will-you-learn)
3. [Technologies Used](#3-technologies-used)
4. [Project Folder Structure](#4-project-folder-structure)
5. [How the Chatbot Works – Big Picture](#5-how-the-chatbot-works--big-picture)
6. [The Dataset – The Brain of the Bot](#6-the-dataset--the-brain-of-the-bot)
7. [Installing the Project](#7-installing-the-project)
8. [Running the Project](#8-running-the-project)
9. [Code Walkthrough – Line by Line](#9-code-walkthrough--line-by-line)
   - [Step 1 – Importing Libraries](#step-1--importing-libraries)
   - [Step 2 – Loading the Dataset](#step-2--loading-the-dataset)
   - [Step 3 – Loading the AI Model](#step-3--loading-the-ai-model)
   - [Step 4 – Keyword Fallback Responses](#step-4--keyword-fallback-responses)
   - [Step 5 – Health Tips System](#step-5--health-tips-system)
   - [Step 6 – Finding the Best Cure](#step-6--finding-the-best-cure)
   - [Step 7 – Translation Feature](#step-7--translation-feature)
   - [Step 8 – The Web Interface (Streamlit)](#step-8--the-web-interface-streamlit)
10. [Key AI Concepts Explained Simply](#10-key-ai-concepts-explained-simply)
11. [How the Languages Work](#11-how-the-languages-work)
12. [What Happens When You Click "Get Response"](#12-what-happens-when-you-click-get-response)
13. [Common Errors and Fixes](#13-common-errors-and-fixes)
14. [Summary](#14-summary)

---

## 1. What Is This Project?

This is a **Medical Chatbot** — a web application where a user can type in a disease name or symptoms, and the chatbot responds with a suggested cure or treatment.

**Example:**
- User types: `"I have a fever and headache"`
- Chatbot replies: `"Rest in a dark room, use a cold compress, stay hydrated, and take prescribed migraine medications."`

It also:
- Gives **personalized health tips** (like sleep, energy, stress advice)
- Translates the response into **13 different languages** (Hindi, Tamil, French, Arabic, etc.)

This project is a great example of combining **Artificial Intelligence**, **Natural Language Processing (NLP)**, and a **Web Interface** all in one Python project.

---

## 2. What Will You Learn?

By studying this project, you will understand:

| Concept | Where It Is Used |
|---|---|
| Reading CSV files with Python | Loading the disease dataset |
| Natural Language Processing (NLP) | Understanding user's typed question |
| AI Sentence Similarity | Matching user input to diseases |
| Streamlit (Web UI) | Building the chatbot interface |
| Translation API | Converting response to other languages |
| Caching in Python | Speeding up model loading |
| Conditional logic (if/else) | Keyword matching and tips selection |

---

## 3. Technologies Used

Before we dive into code, here is every tool/library used and what it does:

| Library | Purpose | Simple Explanation |
|---|---|---|
| `streamlit` | Web Interface | Turns your Python script into a web app with buttons, text boxes etc. |
| `pandas` | Data Handling | Reads and manages the CSV spreadsheet (the disease dataset) |
| `sentence-transformers` | AI Model | Converts text into numbers so the computer can compare meaning |
| `torch` (PyTorch) | AI Backend | The engine that powers the sentence transformer model |
| `deep-translator` | Language Translation | Translates text to Hindi, Tamil, French, etc. using Google Translate |
| `scikit-learn` | Utility | General machine learning utilities |

---

## 4. Project Folder Structure

```
python-chatbot/
│
├── chat.py                  ← The main Python file (the entire chatbot code)
├── dataset - Sheet1.csv     ← The disease + cure data (the chatbot's knowledge)
├── requirement.txt          ← List of all Python packages to install
├── README.md                ← Basic project description
└── images/                  ← Folder for any screenshots or images
```

**Think of it this way:**
- `chat.py` = the brain (logic + interface)
- `dataset - Sheet1.csv` = the memory (knowledge about diseases)
- `requirement.txt` = the shopping list (what to install)

---

## 5. How the Chatbot Works – Big Picture

Here is the complete flow in simple steps:

```
User types a question
        ↓
The AI model converts the question into a number (embedding)
        ↓
It compares that number with all disease names in the dataset
        ↓
It finds the most similar disease (using cosine similarity)
        ↓
It returns the cure for that disease
        ↓
If the user selected a language, it translates the cure
        ↓
The answer is shown on screen
```

If the AI is not confident enough (similarity score too low), it falls back to checking simple keywords like "fever", "cough", etc.

---

## 6. The Dataset – The Brain of the Bot

The file `dataset - Sheet1.csv` is a spreadsheet with **two columns**:

| disease | cure |
|---|---|
| Common Cold Runny Nose Sneezing Cough | Rest, stay hydrated, take vitamin C... |
| Influenza Fever Body Aches Fatigue | Drink plenty of fluids, rest, take antiviral medications... |
| Migraine Headache Sensitivity to Light Nausea | Rest in a dark room, use a cold compress... |
| Diabetes Frequent Urination Excessive Thirst | Maintain a healthy diet, monitor blood sugar... |
| ... | ... |

The dataset has around **100+ diseases** with their symptoms and cures.

**The `disease` column** contains the disease name AND its symptoms together (this helps the AI match even if the user types symptoms instead of a disease name).

**The `cure` column** contains the treatment/suggestion text that will be shown to the user.

---

## 7. Installing the Project

### Step 1 – Make sure Python is installed
Open your terminal/command prompt and type:
```
python --version
```
You should see something like `Python 3.10.x`. If not, download Python from [python.org](https://python.org).

### Step 2 – Navigate to the project folder
```
cd "s:\New folder (11)\python-chatbot"
```

### Step 3 – Install all required packages
```
pip install -r requirement.txt
```

> This reads `requirement.txt` and installs all the listed packages automatically.

**What gets installed:**
```
streamlit          ← web app framework
transformers       ← AI model tools
torch              ← deep learning engine
sentence-transformers ← AI text similarity
googletrans==4.0.0rc1 ← translation (older, use deep-translator instead)
pandas             ← data handling
scikit-learn       ← machine learning utilities
```

> **Note:** Also install `deep-translator` separately (used in the code):
> ```
> pip install deep-translator
> ```

---

## 8. Running the Project

### How to Run

Open your terminal, navigate to the folder where `chat.py` is located, then run:

```
python -m streamlit run "s:\New folder (11)\python-chatbot\chat.py"
```

OR navigate into the folder first:
```
cd "s:\New folder (11)\python-chatbot"
python -m streamlit run chat.py
```

### What Happens After Running

- Your terminal will show: `Local URL: http://localhost:8501`
- A browser window opens automatically with the chatbot interface
- You will see:
  - A text box to type your question
  - A dropdown to select language
  - Two buttons: "Get Response" and "Get a Personalized Health Tip"

> **Why use `python -m streamlit` instead of just `streamlit`?**
> Using `python -m` ensures the correct Python environment is used, avoiding PATH issues on Windows.

---

## 9. Code Walkthrough – Line by Line

Now let's go through `chat.py` step by step.

---

### Step 1 – Importing Libraries

```python
import random
import pandas as pd
import streamlit as st
from sentence_transformers import SentenceTransformer, util
from deep_translator import GoogleTranslator
import torch
```

**What each import does:**

| Import | Purpose |
|---|---|
| `random` | Used to randomly pick one health tip from a list |
| `pandas as pd` | Used to read and work with the CSV dataset |
| `streamlit as st` | Used to create the web interface |
| `SentenceTransformer, util` | The AI model for text similarity |
| `GoogleTranslator` | Used to translate responses to other languages |
| `torch` | PyTorch – the deep learning engine for the AI model |

---

### Step 2 – Loading the Dataset

```python
df = pd.read_csv('dataset - Sheet1.csv')
```

This loads the CSV file into a **DataFrame** (think of it as a Python table).

After this line, `df` looks like this in memory:

| | disease | cure |
|---|---|---|
| 0 | Common Cold Runny Nose Sneezing Cough | Rest, stay hydrated... |
| 1 | Influenza Fever Body Aches Fatigue | Drink plenty of fluids... |
| 2 | Migraine Headache Sensitivity to Light... | Rest in a dark room... |

- `df['disease']` → gives the entire disease column as a list
- `df['cure']` → gives the entire cure column as a list
- `df.iloc[5]['cure']` → gives the cure of row number 5

---

### Step 3 – Loading the AI Model

```python
@st.cache_resource
def load_model():
    device = 'cuda' if torch.cuda.is_available() else 'cpu'
    model = SentenceTransformer('all-MiniLM-L6-v2', device=device)
    return model

model = load_model()
```

**Breaking this down:**

**`@st.cache_resource`** – This is a decorator (a special instruction). It tells Streamlit: *"Load this model only ONCE, and keep it in memory. Don't reload it every time the user clicks a button."*
→ Without this, the AI model would reload every time, making the app very slow.

**`torch.cuda.is_available()`** – This checks if the computer has a GPU (graphics card for fast AI computation). If yes, it uses `'cuda'` (GPU); if no, it uses `'cpu'` (normal processor). On most student laptops, this will default to `'cpu'`.

**`SentenceTransformer('all-MiniLM-L6-v2')`** – This loads a pre-trained AI model called `all-MiniLM-L6-v2`. This model was already trained by researchers on millions of sentences. We are just using (not training) it.

> **What is a pre-trained model?**
> Imagine a student who already studied 10 years of English. You don't teach them English again — you just ask them to read your text. That's what a pre-trained model is.

---

### Step 4 – Keyword Fallback Responses

```python
medical_keywords = {
    "fever": "It sounds like you may have a fever. Stay hydrated and consider seeing a doctor if symptoms persist.",
    "cough": "A persistent cough might be due to an infection or allergy. Try warm fluids and rest.",
    "headache": "Headaches can have many causes...Consider resting and drinking water.",
    "cold": "Common colds usually go away on their own. Stay warm, drink fluids, and get rest.",
}
```

This is a **dictionary** (a Python data structure with key-value pairs).

**When is this used?**
If the AI's similarity score is too low (meaning it's not confident enough in its answer), the chatbot falls back to this dictionary. It looks for words like "fever" or "cough" in the user's input and gives a basic response.

This acts as a **safety net** so the bot never gives an empty or wrong answer.

---

### Step 5 – Health Tips System

```python
health_tips = {
    "sleep": [
        "Try to get at least 7-8 hours of sleep each night.",
        "Establish a regular sleep routine to improve sleep quality.",
        "Avoid screens before bed to help your mind relax.",
    ],
    "energy": [...],
    "stress": [...],
    "general": [...],
}
```

```python
def get_personalized_health_tip(user_input):
    user_input_lower = user_input.lower()

    if "tired" in user_input_lower or "fatigue" in user_input_lower:
        return random.choice(health_tips["energy"])
    elif "sleep" in user_input_lower or "rest" in user_input_lower:
        return random.choice(health_tips["sleep"])
    elif "stress" in user_input_lower or "anxious" in user_input_lower:
        return random.choice(health_tips["stress"])
    else:
        return random.choice(health_tips["general"])
```

**How this works:**

1. The user's input is converted to **lowercase** using `.lower()` so that `"TIRED"` and `"tired"` both match
2. It checks if the input contains keywords like `"tired"`, `"sleep"`, `"stress"`
3. It picks a **random tip** from the matching category using `random.choice()`

**Example:**
- User types: `"I feel tired all the time"`
- Function detects `"tired"` → returns a random energy tip
- Output: `"Exercise regularly to boost your energy levels."`

---

### Step 6 – Finding the Best Cure

This is the **core AI function** of the entire project:

```python
def find_best_cure(user_input):
    user_input_embedding = model.encode(user_input, convert_to_tensor=True)
    disease_embeddings = model.encode(df['disease'].tolist(), convert_to_tensor=True)
    
    similarities = util.pytorch_cos_sim(user_input_embedding, disease_embeddings)[0]
    best_match_idx = similarities.argmax().item()
    best_match_score = similarities[best_match_idx].item()
    
    SIMILARITY_THRESHOLD = 0.5
    
    if best_match_score < SIMILARITY_THRESHOLD:
        for keyword, response in medical_keywords.items():
            if keyword in user_input.lower():
                return response
        return "I'm sorry, I don't have enough information on this. Please consult a healthcare professional."
    
    return df.iloc[best_match_idx]['cure']
```

**Step-by-step breakdown:**

#### Part 1 – Encode the user input
```python
user_input_embedding = model.encode(user_input, convert_to_tensor=True)
```
The AI model converts the user's text into a list of numbers (called an **embedding** or **vector**).

> **What is an embedding?**
> Imagine words on a map. Similar words are placed close together. "Fever" and "temperature" would be near each other. "Fever" and "car" would be far apart. An embedding is like a GPS coordinate for a word or sentence.

Example:
- `"I have a fever"` → `[0.23, -0.45, 0.88, ...]` (a list of 384 numbers)

#### Part 2 – Encode all diseases
```python
disease_embeddings = model.encode(df['disease'].tolist(), convert_to_tensor=True)
```
The same model converts every disease name in the dataset into numbers (embeddings).

#### Part 3 – Calculate similarity
```python
similarities = util.pytorch_cos_sim(user_input_embedding, disease_embeddings)[0]
```
This function calculates **Cosine Similarity** between the user's input and every disease in the dataset.

> **What is Cosine Similarity?**
> It measures the angle between two vectors (lists of numbers). If angle = 0°, they are identical (similarity = 1.0). If angle = 90°, they are completely different (similarity = 0.0). This is a standard way to compare text meanings in AI.

The result `similarities` contains a score between 0 and 1 for every disease.

#### Part 4 – Find the best match
```python
best_match_idx = similarities.argmax().item()
best_match_score = similarities[best_match_idx].item()
```
- `.argmax()` finds the **index** of the highest similarity score (which disease is the best match)
- `.item()` converts it from a tensor (AI format) to a regular Python number

#### Part 5 – Threshold check
```python
SIMILARITY_THRESHOLD = 0.5
if best_match_score < SIMILARITY_THRESHOLD:
    ...
```
If the best match has a score below 0.5 (50%), the AI is not confident. So it falls back to keyword matching or a default message.

#### Part 6 – Return the cure
```python
return df.iloc[best_match_idx]['cure']
```
This returns the cure text from the row in the dataset that matched best.

---

### Step 7 – Translation Feature

```python
def translate_text(text, dest_language='en'):
    try:
        if dest_language == 'en':
            return text
        translator = GoogleTranslator(source='en', target=dest_language)
        return translator.translate(text)
    except Exception as e:
        st.error(f"Translation error: {e}")
        return text
```

**How it works:**
- If the user selected English (`'en'`), just return the original text without any translation
- Otherwise, use `GoogleTranslator` to translate the English response into the selected language
- If translation fails for any reason, return the original English text (so the app doesn't crash)

**`try...except` explained:**
This is error handling. It's like saying: *"Try to do this. If it fails, don't crash — just do this other thing instead."*

---

### Step 8 – The Web Interface (Streamlit)

```python
st.title("Medical Chatbot 🤖")
user_input = st.text_input("Ask a question:")
```

`st.title()` → Shows a big heading on the web page
`st.text_input()` → Creates a text box where the user types their question

```python
language_choice = st.selectbox("Select Language", [
    "English", "Hindi", "Gujarati", "Korean", "Turkish",
    "German", "French", "Arabic", "Urdu", "Tamil", "Telugu", "Chinese", "Japanese"
])
```

`st.selectbox()` → Creates a dropdown menu with language options

```python
language_codes = {
    "English": "en",
    "Hindi": "hi",
    "Tamil": "ta",
    ...
}
```

This maps human-readable language names to their **ISO language codes** (standard 2-letter codes used by translation APIs).

```python
if st.button("Get Response"):
    if user_input:
        response = find_best_cure(user_input)
        translated_response = translate_text(response, dest_language=language_codes[language_choice])
        st.write(f"**My Suggestion is:** {translated_response}")
        st.write("*Please note, the translation is provided by AI and might not be perfect.*")
```

`st.button()` → Creates a clickable button. The code inside `if st.button(...)` runs **when the user clicks that button**.

`st.write()` → Displays text on the page. Using `**text**` makes it **bold**. Using `*text*` makes it *italic*.

The same pattern is used for the "Get a Personalized Health Tip" button.

---

## 10. Key AI Concepts Explained Simply

### What is NLP (Natural Language Processing)?

NLP = Teaching computers to understand human language.

When you type `"I have pain in my head"`, a computer without NLP would not know this is related to "headache". With NLP and sentence embeddings, it understands the meaning and can match it to "Migraine / Headache" in the dataset.

### What is a Sentence Transformer?

A Sentence Transformer is an AI model that converts sentences into vectors (lists of numbers). Sentences with similar meanings get similar vectors.

```
"I have a headache"       → [0.22, -0.45, 0.71, ...]
"My head is hurting"      → [0.24, -0.43, 0.69, ...]   ← very close!
"I love eating pizza"     → [-0.88, 0.12, -0.33, ...]  ← very far apart
```

The model `all-MiniLM-L6-v2` is a small but powerful model — "MiniLM" means it's a mini version, "L6" means it has 6 layers, and "v2" means version 2.

### What is Cosine Similarity?

Think of two arrows pointing from the center of a circle. If both arrows point in roughly the same direction, the angle between them is small → high similarity. If they point in completely different directions → low similarity.

Cosine similarity = cos(angle between the two vectors)
- Score = 1.0 → identical meaning
- Score = 0.5 → somewhat related
- Score = 0.0 → completely unrelated

In this project: threshold = 0.5 → if score ≥ 0.5, return the cure from dataset.

---

## 11. How the Languages Work

The chatbot supports **13 languages**:

| Language | Code |
|---|---|
| English | en |
| Hindi | hi |
| Gujarati | gu |
| Korean | ko |
| Turkish | tr |
| German | de |
| French | fr |
| Arabic | ar |
| Urdu | ur |
| Tamil | ta |
| Telugu | te |
| Chinese (Simplified) | zh-CN |
| Japanese | ja |

**The flow:**
1. The chatbot always finds the cure in **English** first (using the dataset)
2. Then if the user selected a non-English language, it translates the English response using Google Translate
3. The translated text is shown on screen

This means the dataset only needs to be in English — the translation takes care of all other languages automatically!

---

## 12. What Happens When You Click "Get Response"

Here is the complete step-by-step process when a user types a question and clicks "Get Response":

```
1. User types: "I have fever and body aches"
   ↓
2. streamlit captures the input as: user_input = "I have fever and body aches"
   ↓
3. find_best_cure(user_input) is called
   ↓
4. AI model encodes "I have fever and body aches" → vector [0.12, 0.55, ...]
   ↓
5. AI model encodes all 100+ disease entries in the dataset → list of vectors
   ↓
6. Cosine similarity is calculated between user vector and every disease vector
   ↓
7. Best match found: "Influenza Fever Body Aches Fatigue" with score 0.82
   ↓
8. Score 0.82 > 0.5 (threshold) → return the cure from that row
   ↓
9. Cure: "Drink plenty of fluids, rest, take antiviral medications if prescribed..."
   ↓
10. If language is Tamil: translate to Tamil using GoogleTranslator
    ↓
11. Display the translated cure on the web page
```

---

## 13. Common Errors and Fixes

| Error | Cause | Fix |
|---|---|---|
| `File does not exist: chat.py` | You ran streamlit from the wrong folder | Navigate to the project folder first: `cd "s:\New folder (11)\python-chatbot"` then run |
| `ModuleNotFoundError: No module named 'streamlit'` | Package not installed | Run `pip install streamlit` |
| `ModuleNotFoundError: No module named 'sentence_transformers'` | Package not installed | Run `pip install sentence-transformers` |
| `Translation error` | Internet not available or translation API issue | Check your internet connection |
| App loads very slowly first time | AI model is downloading (~80MB) | Wait once — it caches after that |

---

## 14. Summary

Here is the project in a nutshell:

| Component | What It Does |
|---|---|
| `dataset - Sheet1.csv` | Stores 100+ diseases with symptoms and cures |
| `SentenceTransformer` model | Converts text into AI vectors for comparison |
| `cosine_similarity` | Finds which disease matches the user's question |
| `medical_keywords` dict | Backup when AI is not confident |
| `health_tips` dict | Gives lifestyle tips based on user keywords |
| `translate_text()` | Translates the cure to the chosen language |
| `streamlit` | Creates the visual web interface |

### Key Takeaways for Students

1. **AI doesn't understand words — it understands numbers.** Text is converted to vectors for comparison.
2. **Pre-trained models save time.** We didn't train the AI — we used an already trained model.
3. **Always have a fallback.** If AI fails, keywords take over. If keywords fail, a polite default message is shown.
4. **Streamlit makes web apps easy.** No HTML/CSS needed — just Python.
5. **Translation separates concerns neatly.** The chatbot always works in English internally. Translation is a separate layer on top.

---

> **Tip for Class:** Try adding new diseases to the CSV file and test if the chatbot finds them correctly. Also try typing symptoms instead of disease names and see how the AI still understands!
