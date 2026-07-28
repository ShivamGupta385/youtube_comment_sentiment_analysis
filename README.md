# EchoSense: Real-Time YouTube Audience Sentiment Platform

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![Gradio](https://img.shields.io/badge/UI-Gradio-orange?style=for-the-badge)
![HuggingFace](https://img.shields.io/badge/Deployment-HuggingFace%20Spaces-yellow?style=for-the-badge&logo=huggingface)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

EchoSense is an automated sentiment analysis platform that evaluates viewer feedback from YouTube video comment streams in real time. By combining **VADER text analysis** with an **emoji sentiment lexicon**, EchoSense accurately captures both textual and visual emotional context in unstructured user-generated content.

**Live Demo:**  
https://huggingface.co/spaces/Shivam835/EchoSense

---

# Key Features

- **Real-Time Data Ingestion:** Fetches YouTube comments and video metadata using the YouTube Data API v3.
- **Hybrid Sentiment Scoring:** Combines VADER sentiment analysis with emoji sentiment mapping using an equal-weighted scoring approach.
- **Interactive Visualizations:** Generates sentiment pie charts, engagement bar plots, word clouds, and comment-length violin plots.
- **CSV Export:** Allows users to download processed comments along with sentiment scores and classifications.

---

# 🛠️ System Architecture & Workflow

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

### Workflow

1. **Data Ingestion**
   - Retrieves `author`, `comment`, `date`, and `likes` metadata using the YouTube Data API v3.

2. **Text Preprocessing**
   - Removes URLs, mentions, special characters, and unnecessary whitespace using Regex and NLTK.

3. **Hybrid Sentiment Analysis**
   - **Text Sentiment:** Computed using **VADER**.
   - **Emoji Sentiment:** Computed using an emoji sentiment lexicon.
   - **Final Classification:** Equal-weighted combination of both scores to classify comments as **Positive**, **Negative**, or **Neutral**.

4. **Visualization & Export**
   - Generates analytical plots and exports processed data as a downloadable CSV report.

---

# Data Schema

| Column | Description |
|---------|-------------|
| `author` | Display name of the commenter |
| `comment` | Original YouTube comment |
| `date` | Comment publication timestamp |
| `likes` | Number of likes received |
| `cleaned_comment` | Preprocessed comment text |
| `text_sentiment` | VADER compound sentiment score |
| `emoji_sentiment` | Emoji lexicon sentiment score |
| `final_sentiment` | Final classification (Positive, Negative, Neutral) |

---

# Local Installation

## 1. Prerequisites

Obtain a valid **YouTube Data API v3 Key** from the Google Cloud Console.

## 2. Clone the Repository

```bash
git clone https://github.com/Shivam835/EchoSense.git
cd EchoSense
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 4. Run the Application

```bash
python app.py
```

---

# Tech Stack

### Programming Language
- Python

### Data Processing
- Pandas
- NumPy

### API Integration
- google-api-python-client

### Natural Language Processing
- NLTK
- VaderSentiment
- Emoji
- Regex

### Data Visualization
- Matplotlib
- Seaborn
- WordCloud

### Interface & Deployment
- Gradio
- Hugging Face Spaces

---

# Future Roadmap

- [ ] Integrate transformer-based models (e.g., BERT) for improved contextual sentiment analysis.
- [ ] Expand the emoji sentiment lexicon to support modern slang and evolving emoji usage.
- [ ] Add multilingual sentiment analysis.
- [ ] Implement WebSocket-based real-time YouTube Live comment tracking.

---

## 👨‍💻 Author

**Shivam Gupta**

If you found this project useful, consider giving it a ⭐ on GitHub!
