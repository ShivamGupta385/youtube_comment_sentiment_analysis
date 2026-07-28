# EchoSense: Real-Time YouTube Audience Sentiment Platform

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![Gradio](https://img.shields.io/badge/UI-Gradio-orange?style=for-the-badge)
![HuggingFace](https://img.shields.io/badge/Deployment-HuggingFace%20Spaces-yellow?style=for-the-badge&logo=huggingface)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**EchoSense** is a real-time YouTube audience sentiment analysis platform that extracts, preprocesses, and analyzes viewer comments using a hybrid sentiment engine. By combining **VADER** text analysis with a custom **emoji sentiment lexicon**, EchoSense captures both textual and visual emotional context from unstructured user-generated content, providing interactive analytics through a Gradio interface.

**Live Demo:** https://huggingface.co/spaces/Shivam835/EchoSense

---

# Key Features

- **Real-Time Data Ingestion:** Fetches YouTube comments and video metadata using the YouTube Data API v3.
- **Smart API Quota Management:** Automatically rotates between multiple API keys to handle YouTube API quota limits and ensure uninterrupted analysis.
- **Hybrid Sentiment Scoring:** Combines VADER sentiment analysis with emoji sentiment mapping using an equal-weighted approach.
- **Interactive Dashboard:** Built with Gradio to provide instant visual analytics directly in the browser.
- **Rich Visualizations:** Generates sentiment pie charts, engagement bar plots, word clouds, daily sentiment trends, and comment-length violin plots.
- **CSV Export:** Allows users to download processed comments together with sentiment scores and classifications.

---

# System Architecture & Workflow

```text
                   +----------------------+
                   |  YouTube Data API v3 |
                   +----------+-----------+
                              |
                              v
                  +-----------------------+
                  |   Data Ingestion      |
                  +-----------+-----------+
                              |
                              v
               +----------------------------+
               | Text Preprocessing         |
               | (Regex + NLTK Cleaning)    |
               +-----------+----------------+
                               |
                               v
              +--------------------------------------+
              | Hybrid Sentiment Analysis            |
              |  • VADER Text Sentiment              |
              |  • Emoji Sentiment Lexicon           |
              +-----------+--------------------------+
                              |
                              v
                +-------------------------------+
                | Composite Sentiment Scoring   |
                +-----------+-------------------+
                              |
                    +---------+---------+
                    |                   |
                    v                   v
          +------------------+   +-------------------+
          | Visualizations   |   | CSV Export        |
          +------------------+   +-------------------+
                    \                 /
                     \               /
                      +-------------+
                      | Gradio UI   |
                      +-------------+
```

---

# Project Workflow

## 1. Data Ingestion

- Retrieves YouTube comments and video metadata using the **YouTube Data API v3**.
- Extracts:
  - Author
  - Comment
  - Publication Date
  - Like Count

---

## 2. Text Preprocessing

- Removes URLs
- Removes user mentions
- Removes unnecessary whitespace
- Cleans noisy tokens
- Converts API responses into structured Pandas DataFrames

---

## 3. Multi-Modal Sentiment Analysis

### Text Sentiment

Computed using **VaderSentiment**.

### Emoji Sentiment

Computed using a custom emoji sentiment lexicon.

### Final Sentiment

Both scores are combined using an equal-weighted strategy to classify each comment as:

- Positive
- Neutral
- Negative

---

## 4. Analytics & Visualization

EchoSense automatically generates:

- Overall sentiment distribution
- Pie charts
- Bar charts
- Daily sentiment trends
- Average likes by sentiment
- Most active commenters
- Word clouds
- Comment-length violin plots

---

# Data Schema

Processed comments are exported with the following schema.

| Column | Description |
|---------|-------------|
| **author** | Display name of the commenter |
| **comment** | Original YouTube comment |
| **date** | Comment publication timestamp |
| **likes** | Number of likes received |
| **cleaned_comment** | Preprocessed comment text |
| **text_sentiment** | VADER compound sentiment score |
| **emoji_sentiment** | Emoji lexicon sentiment score |
| **final_sentiment** | Final sentiment classification (**Positive**, **Neutral**, **Negative**) |

---

# Using the Live Demo

The application is publicly deployed on **Hugging Face Spaces**.

Since the YouTube API keys are securely stored using **Hugging Face Space Secrets**, users **do not need to provide their own API keys** when using the hosted version.

### Steps

1. Paste a YouTube video URL.

Example:

```text
https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

or

```text
https://youtu.be/dQw4w9WgXcQ
```

2. Select the maximum number of comments to analyze (up to **100,000**).

3. Click **Analyze**.

4. Explore:

- Video metadata
- Sentiment summary
- Interactive visualizations
- Statistical insights

5. Download the processed dataset from the **Download CSV Only** tab.

---

# Running Locally

## 1. Prerequisites

Before running the project locally, ensure you have:

- Python **3.10+**
- A valid **YouTube Data API v3 Key**
- Git installed

If you plan to run the notebook version, you'll also need:

- Jupyter Notebook

---

## 2. Clone the Project

Choose one of the following depending on how you want to use EchoSense.

### Option A — Clone the GitHub Repository (Recommended)

```bash
git clone https://github.com/Shivam835/EchoSense.git
cd EchoSense
```

The GitHub repository contains:

- Complete source code
- Jupyter Notebook implementation
- Documentation
- Project assets

---

### Option B — Clone the Hugging Face Space

If you'd like to run the exact version deployed on Hugging Face Spaces:

```bash
git clone https://huggingface.co/spaces/Shivam835/EchoSense
cd EchoSense
```

The Hugging Face Space contains the deployable Gradio application used for the public demo.

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Option A — Run the Gradio Application

If you're using the **Gradio application** (GitHub or Hugging Face Space), configure your YouTube API keys as environment variables.

### Windows

```cmd
set MY_API_KEY_1=your_first_api_key
set MY_API_KEY_2=your_second_api_key
```

### macOS / Linux

```bash
export MY_API_KEY_1="your_first_api_key"
export MY_API_KEY_2="your_second_api_key"
```

> **Note:** If you only have one API key, you may use the same key for both variables. Using two keys is recommended to minimize interruptions caused by YouTube API quota limits.

Start the application:

```bash
python app.py
```

Open:

```text
http://127.0.0.1:7860
```

---

## Option B — Run the Original Jupyter Notebook

If you're using the notebook implementation from the GitHub repository:

Open:

```text
Youtube_Comments_Sentiment_Analysis.ipynb
```

Update:

- Your YouTube Data API v3 Key
- Target YouTube Video ID

Example:

```text
https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Video ID:

```text
dQw4w9WgXcQ
```

Launch Jupyter:

```bash
jupyter notebook Youtube_Comments_Sentiment_Analysis.ipynb
```

Run all notebook cells to perform the complete sentiment analysis.

---

# Tech Stack

## Programming Language

- Python

## Data Processing

- Pandas
- NumPy

## API Integration

- google-api-python-client

## Natural Language Processing

- NLTK
- VaderSentiment
- Emoji
- Regex

## Data Visualization

- Matplotlib
- Seaborn
- WordCloud

## Interface & Deployment

- Gradio
- Hugging Face Spaces
- Jupyter Notebook

---

# Future Roadmap

- [ ] Integrate transformer-based models (e.g., fine-tuned BERT) for improved contextual sentiment analysis.
- [ ] Expand the emoji sentiment lexicon to support modern slang and evolving emoji usage.
- [ ] Implement multilingual sentiment analysis and translation.
- [ ] Add WebSocket support for real-time YouTube Live comment tracking.
- [ ] Support historical sentiment comparison across multiple videos.
- [ ] Enable batch analysis for YouTube playlists and channels.

---


If you found this project useful, consider giving it a ⭐ on GitHub!
