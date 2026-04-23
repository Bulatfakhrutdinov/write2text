# 📝 Write2Text

<div align="center">

**Handwritten Text to Printed Text Conversion using Machine Learning**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104.1-green.svg)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-orange.svg)](https://pytorch.org/)

</div>

---

## 📋 Description

**Write2Text** converts images containing handwritten text into printed text. The system segments text into individual words and recognizes them using the TrOCR model.

### 🔄 How It Works

1. **Image Upload** → User uploads an image with handwritten text
2. **Segmentation** → System divides text into separate words and rows
3. **Recognition** → Each word is processed by the OCR model (TrOCR)
4. **Result** → Recognized text is returned in printed format

---

## ✨ Features

- 🖼️ Image processing with various formats support
- ✂️ Intelligent text segmentation into words
- 🤖 ML-based recognition using TrOCR
- 🌐 Web interface for easy usage
- 🚀 REST API for integration
- 💾 Local model storage for offline work

---

## 🚀 Quick Start

### Installation

```bash
# Clone repository
git clone <repository-url>
cd write2text

# Create virtual environment
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Download OCR model
python download_model.py
```

### Usage

```bash
# Start server
python main.py
```

Open `frontend/index.html` or navigate to `http://localhost:8000`

---


## Docker Setup
### Build and Run Locally

Build Docker image
docker build -t write2text-ocr:latest .

Run container
```bash
docker run -d \
  --name write2text-ocr \
  -p 8000:8000 \
  write2text-ocr:latest
```

Check logs
```bash
docker logs -f write2text-ocr
```

Stop container
```bash
docker stop write2text-ocr
```

Remove container
```bash
docker rm write2text-ocr
```

## 📁 Project Structure

```
write2text/
├── backend/          # FastAPI application
├── frontend/         # Web interface
├── ml/               # ML components
│   ├── preprocessing/  # Text segmentation
│   ├── ocr/          # OCR model
│   └── notebooks/    # Experiments
├── models/           # Saved ML models
├── main.py           # Entry point
└── download_model.py # Model download script
```

---

## 🛠️ Technologies

- **FastAPI** — Web framework
- **PyTorch** — Deep learning
- **Transformers** — Pre-trained models
- **TrOCR** — Text recognition
- **OpenCV** — Image processing

---

## 📡 API

### `POST /segment`

Upload image for processing.

```bash
curl -X POST "http://localhost:8000/segment" \
     -F "file=@image.png"
```

**Response:**
```json
{
  "status": "success",
  "word_count": 42,
  "recognized_text": "Recognized text...",
  "word_frames": [...]
}
```

---

## 🔧 Configuration

Change OCR model in `ml/ocr/model.py`:
```python
ocr_model = OCRModel(model_name)
```

Device is auto-detected: CUDA → MPS → CPU

---

## 🙏 Acknowledgments

- [TrOCR](https://github.com/microsoft/unilm/tree/master/trocr) by Microsoft
- [raxtemur/trocr-base-ru](https://huggingface.co/raxtemur/trocr-base-ru) for Russian language

---
