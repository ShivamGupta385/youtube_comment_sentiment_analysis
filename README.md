# YouTube Comments Sentiment Analysis

This project performs sentiment analysis on YouTube video comments using a combination of VADER sentiment analysis and emoji-based sentiment scoring. It integrates emoji sentiment to better capture emotional context, enhancing the overall analysis of user opinions.

## Live Demo
Try it out here: [👉 Deployed on Hugging Face](https://your-huggingface-app-link)  
(Replace with your actual Hugging Face URL)

## Key Features
- Analyze the sentiment of comments from **any YouTube video**.
- Combines **text and emoji sentiment** using an equal-weighted approach.
- Provides insights with **rich visualizations** and **top comments**.
- Uses **Gradio-based interface** for easy interaction.

## How to Use
- Enter a **YouTube video URL** in the Gradio interface.
- Select the **number of comments** you want to analyze.
- Get real-time sentiment analysis, top comments, and visual breakdowns.

## Dataset
- Comments and video metadata are fetched using the **YouTube Data API v3**.
- The API returns a `.csv` file containing the following columns:
  - `author`: Name of the commenter.
  - `comment`: Original YouTube comment.
  - `date`: Date of the comment.
  - `likes`: Number of likes on the comment.

- This CSV file is then used for further sentiment analysis and visualization.

- In the Gradio interface, a **separate tab** is provided to **download the final analyzed CSV file**, which including the original columns also have:
  - `cleaned_comment`: Preprocessed comment text (no URLs, mentions, etc.).
  - `text_sentiment`: VADER sentiment score.
  - `emoji_sentiment`: Sentiment score based on emojis.
  - `final_sentiment`: Combined sentiment label (based on text + emoji).

## Project Workflow
1. **Data Preprocessing**
   - Removed extra spaces, URLs, mentions, and irrelevant tokens that do not contribute to sentiment analysis.

2. **Sentiment Analysis**
   - Used **VADER (Valence Aware Dictionary and sEntiment Reasoner)** for text sentiment.
   - Applied an **emoji sentiment lexicon** to score emojis in comments.
   - Used an **equal-weighted approach** for text and emoji sentiment to determine the final sentiment.

3. **Visualizations & Analysis**
- Sentiment distribution (Pie Chart).
- Most liked comment overall & for each sentiment (Bar Plot).
- Average likes for each sentiment (Bar Plot).
- Word clouds for positive, negative, and neutral comments.
- Comment length distribution by sentiment (Violin Plot).
- ...and more!

## Tools & Libraries
- Pandas, NumPy
- NLTK, VADER
- Emoji
- Matplotlib, Seaborn, WordCloud
- Gradio

## Future Improvements
- Integrate deep learning models like **BERT** for more accurate sentiment prediction.
- Expand and refine the **emoji sentiment lexicon**.
- Support for **multiple languages**.
- Real-time comment streaming using the **YouTube API**.
