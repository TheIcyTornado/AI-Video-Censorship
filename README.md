# AI-Video-Censorship

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![OpenAI Whisper](https://img.shields.io/badge/Powered%20by-OpenAI%20Whisper-black.svg)](https://github.com/openai/whisper)
[![Kaggle Dataset](https://img.shields.io/badge/Dataset-Kaggle-lightgrey.svg)](https://www.kaggle.com/datasets/konradb/profanities-in-english-collection/versions/1)

---

## Overview

**AI-Video-Censorship** is a Jupyter Notebook project that automatically detects and censors profanity in videos.  
It uses **OpenAI Whisper** for speech transcription and **FFmpeg** for audio editing.  
Detected swear words are replaced with a bleep sound, creating a clean, censored version of the original video.

---

## Features

- Automatic transcription using Whisper (word-level timestamps)
- Configurable profanity severity levels (mild, strong, severe)
- Adjustable confidence thresholds and padding
- Bleep sound overlay with FFmpeg
- Iterative censorship passes for accuracy
- Entirely contained in a single `.ipynb` notebook

---

## Project Structure

```
📁 AI-Video-Censorship/
│
├── profanity.csv                      # Profanity list (from Kaggle dataset)
├── bleep.mp3                          # Bleep sound file
├── sample_video.mp4                    # Example input video
├── AI-Video-Censorship.ipynb          # Jupyter Notebook
└── README.md                          # Documentation
```

---

## Setup

### 1. Requirements

Ensure you have the following installed:

- Python **3.10+**
- **FFmpeg** (must be available in PATH)
- Required Python packages:

```bash
pip install openai-whisper pandas
```

Verify FFmpeg installation:

```bash
ffmpeg -version
```

---

### 2. Dataset

This project uses the [**Profanities in English – collection**](https://www.kaggle.com/datasets/konradb/profanities-in-english-collection/versions/1) dataset from Kaggle.

Download and extract the dataset, then place the CSV file in the project directory as `profanity.csv`.  
The notebook will automatically normalize and categorize the words into:

- `low_swear_words`
- `mid_swear_words`
- `strong_swear_words`

---

### 3. Configuration

Open **AI-Video-Censorship.ipynb** and adjust the configuration cell:

```python
video_path = "SampleVideo.mp4"     # Input video
bleep_path = "bleep.mp3"           # Bleep sound file
model_size = "small"               # Whisper model size (tiny, base, small, medium, large)
swear_words = low_swear_words      # Choose severity level
MAX_PASSES = 10                    # Maximum censorship passes
PAD = 0.15                         # Padding (seconds) before/after each word
MIN_PROB = 0.8                     # Minimum transcription confidence
```

Then run the notebook cell-by-cell or execute all cells to process and censor your video.

---

## Configuration Options

| Parameter | Description | Default |
|------------|--------------|----------|
| `MAX_PASSES` | Maximum censorship iterations | `10` |
| `PAD` | Time padding (seconds) before and after each word | `0.15` |
| `MIN_PROB` | Minimum Whisper confidence threshold | `0.8` |
| `model_size` | Whisper model size | `"small"` |
| `swear_words` | Set of words to censor (low/mid/strong) | `low_swear_words` |

---

## How It Works

1. **Transcription** – Whisper transcribes the video audio with timestamps and confidence levels.
2. **Detection** – Words are normalized (lowercased and stripped of punctuation) and compared to the selected profanity list.
3. **Audio Filtering** – FFmpeg mutes sections containing profanities and overlays a bleep sound.
4. **Iterative Passes** – The process repeats until no further profanities are detected or the maximum pass count is reached.

---

## Credits

- [**OpenAI Whisper**](https://github.com/openai/whisper) – Automatic speech recognition
- [**FFmpeg**](https://ffmpeg.org/) – Audio/video processing
- [**Kaggle: Profanities in English – collection**](https://www.kaggle.com/datasets/konradb/profanities-in-english-collection/versions/1) – Profanity dataset
- Developed by **Joshua Hipkiss**

---

## License

This project is released under the **MIT License**.  
You are free to use, modify, and distribute it with proper attribution.
