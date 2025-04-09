# Streamlit YouTube Transcript Summarizer - Architecture & Plan

## Overview
A Streamlit web app where the user inputs a YouTube URL, clicks **"Grab Transcript"**, and receives a concise list of key takeaways from the video. The app:
- Fetches the transcript (supports multilingual videos)
- Summarizes it using OpenRouter's `openrouter/quasar-alpha` model
- Displays only the key bullet points

---

## Components

### 1. User Interface (Streamlit)
- **Input:** Text box for YouTube URL
- **Button:** "Grab Transcript"
- **Output:** Bullet points of key takeaways

### 2. API Key Handling
- Read OpenRouter API key from `api.txt` in the project root

### 3. Fetching YouTube Transcript
- Use `youtube-transcript-api`
- Support multilingual transcripts
- Concatenate transcript segments into a single string

### 4. Summarization via OpenRouter
- Prepare a prompt instructing the model to generate **only key bullet points**
- Use the `openrouter/quasar-alpha` model via OpenRouter API
- Parse and display the bullet points

---

## Dependencies
- `streamlit`
- `youtube-transcript-api`
- `requests`

---

## Error Handling
- Invalid or unsupported YouTube URL
- Transcript unavailable
- API errors or invalid API key

---

## User Flow

```mermaid
flowchart TD
    A[User inputs YouTube URL] --> B[Clicks "Grab Transcript"]
    B --> C[Read API key from api.txt]
    C --> D[Fetch transcript via youtube-transcript-api]
    D --> E[Prepare prompt for OpenRouter]
    E --> F[Send prompt to OpenRouter API]
    F --> G[Receive bullet points summary]
    G --> H[Display bullet points in Streamlit app]
```

---

## Prompt Design
- Instruct the model to:
  - Read the entire transcript
  - Generate a **concise** list of the **most important takeaways** as bullet points
  - Ignore less relevant details
- Example prompt:
  ```
  Given the following video transcript, extract the key takeaways as concise bullet points:
  [Transcript here]
  ```

---

## Summary
This app will provide users with a quick, clear understanding of any YouTube video's main points, supporting multiple languages and focusing on simplicity and clarity.