# Sign Language Translator Using Machine Learning
# ✋ Sign Language Translator Using Machine Learning

Real-time ASL hand gesture recognition system that translates 
sign language into text and speech using computer vision 
and a dual-model architecture.

---

## 🎯 Project Overview

This application enables real-time communication for the 
hearing-impaired by translating ASL gestures into readable 
text and audible speech. It uses two separate ML models 
optimised for different recognition tasks — an MLP neural 
network for word/phrase gestures and a Random Forest 
classifier for the full ASL alphabet.

---

## 📊 Model Performance

### MLP — Word/Phrase Recognition
| Metric | Score |
|--------|-------|
| Overall Accuracy | **96.7%** |
| Total Samples Evaluated | 90 (10 per gesture) |
| Weighted F1 Score | 0.97 |
| Parameters | 25,097 |
| Input Features | 126 (MediaPipe landmarks, both hands) |

**Per-gesture accuracy:**
| Gesture | Accuracy |
|---------|----------|
| call me | 100% |
| dislike | 100% |
| done | 100% |
| hello | 100% |
| i love you | 100% |
| loser | 100% |
| ok | 100% |
| peace | 100% |
| you | 70% |

Known limitation: "you" gesture (pointing) shares visual 
similarity with directional signs, causing occasional 
misclassification. Future improvement: collect more diverse 
training samples for directional gestures.

### Random Forest — Alphabet Recognition
- Recognises full ASL alphabet (26 signs, A–Z)
- Input: 63 features (21 MediaPipe landmarks × x/y/z, 
  single hand)
- Label encoding via scikit-learn LabelEncoder

---

## 🏗️ Two-Model Architecture
Webcam Input
↓
MediaPipe Hand Landmark Extraction
↓
├── Word Mode → 126 features (both hands,
│              centered + scaled) → MLP (PyTorch)
│              → 9 gesture classes
│
└── Alphabet Mode → 63 features (single hand,
raw landmarks) → Random Forest
→ 26 letter classes
↓
Prediction → Sentence Builder → gTTS Text-to-Speech

---

## ✨ Features

- Real-time gesture recognition at standard webcam framerates
- Dual mode: word/phrase recognition + full alphabet spelling
- Auto-stability system — requires 15 consistent frames 
  before accepting a prediction (prevents false triggers)
- Sentence builder with space and delete gesture support
- Text-to-speech output via gTTS
- User authentication with OTP email verification
- MongoDB-backed session history
- Flask web interface with live video streaming

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| ML Models | PyTorch (MLP), Scikit-learn (Random Forest) |
| Computer Vision | MediaPipe, OpenCV |
| Backend | Flask, Flask-Bcrypt |
| Database | MongoDB |
| TTS | gTTS |
| Deployment | Python 3.10 |

---
---

## ✨ Features

- Real-time gesture recognition at standard webcam framerates
- Dual mode: word/phrase recognition + full alphabet spelling
- Auto-stability system — requires 15 consistent frames 
  before accepting a prediction (prevents false triggers)
- Sentence builder with space and delete gesture support
- Text-to-speech output via gTTS
- User authentication with OTP email verification
- MongoDB-backed session history
- Flask web interface with live video streaming

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| ML Models | PyTorch (MLP), Scikit-learn (Random Forest) |
| Computer Vision | MediaPipe, OpenCV |
| Backend | Flask, Flask-Bcrypt |
| Database | MongoDB |
| TTS | gTTS |
| Deployment | Python 3.10 |

---

## 🚀 How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Set up environment variables
# Create .env file with:
# SECRET_KEY=your_secret_key
# MONGO_URI=mongodb://localhost:27017/
# EMAIL_USER=your_email@gmail.com
# EMAIL_PASS=your_app_password

# Run the application
python app.py
```

Navigate to `http://localhost:5000`

---
sign-language-translator/
│
├── app.py                    ← Flask app + inference logic
├── model/
│   ├── asl_model.joblib      ← Random Forest (alphabet)
│   └── label_encoder.joblib  ← Label encoder
├── action_model.pth          ← MLP model (word recognition)
├── model_evaluation.ipynb    ← Evaluation notebook
├── evaluation_results.json   ← Accuracy results
├── static/audio/             ← Generated TTS audio files
├── templates/                ← HTML templates
└── requirements.txt

---

## 📈 Evaluation

Evaluated on 90 live webcam samples (10 per gesture class).
Full evaluation code available in `model_evaluation.ipynb`.

To reproduce evaluation results:
```bash
jupyter notebook model_evaluation.ipynb
```

---

## 🔮 Future Improvements

- Collect additional training data for directional gestures 
  to improve "you" gesture accuracy from 70% to 95%+
- Add support for dynamic gestures (motion-based signs)
- Expand word vocabulary beyond 9 phrases
- Deploy as mobile application for accessibilit
