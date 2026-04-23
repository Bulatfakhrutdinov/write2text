# 📝 Write2Text

<div align="center">

**Handwritten Text to Printed Text Conversion using Machine Learning**
**ИИ продукт для конвертации письменного текст в печатный при помощи обученной модели**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104.1-green.svg)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-orange.svg)](https://pytorch.org/)

</div>

---

## 📋 Описание

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

## 🚀 Старт

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

## 📁 Структура проекта

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

## 🛠️ Технологии

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



US (User Story) Как пользователь, я хочу загрузить фотографию рукописного русского текста через сайт, чтобы получить распознанный и грамматически/смыслово связанный печатный текст, обработанный ИИ.

UC (Use Case) Пользователь открывает сайт. Нажимает кнопку загрузки файла и выбирает изображение с русским рукописным текстом. Система отправляет изображение на сервер. ИИ распознаёт символы (OCR) и преобразует их в печатный текст. Обученная модель связывает слова (исправляет ошибки распознавания, восстанавливает связность предложений). Система возвращает итоговый печатный текст на экран. Пользователь копирует или скачивает результат.

ПИМ аналитика (Product Impact Metrics) Точность распознавания символов (Accuracy, % правильных символов) Коэффициент связности текста (пользовательская оценка 1–5, среднее) Время обработки одной фотографии (секунды, p95) Конверсия загрузка → успешный результат (%, количество обработанных фото без ошибок) Повторные использования на одного пользователя (stickiness)

Проблема Школьники и студенты вынуждены работать с бумажными конспектами там, где гаджеты запрещены (уроки, лекции). Перенос записей в цифру вручную — долго, скучно, убивает продуктивность. Готовые OCR-решения есть, но они тупо распознают символы, теряя смысл и связность текста.

Решение Сервис, который за секунды превращает фото рукописного русского текста в печатный, анализируемый и связываемый ИИ. Не просто OCR, а умная доработка: модель сопоставляет текущий текст с ранее распознанным контекстом, исправляя ошибки и восстанавливая логику записей.

Целевая аудитория (ЦА) Школьники и студенты 13–25 лет Те, кто много пишет от руки и хочет быстро оцифровать конспекты Учится на дистанте или гибриде, активно пользуется учебными платформами

Каналы продвижения Сайты для решения задач (e.g. «Решу ЕГЭ», «Фоксфорд», «Сдам ГИА») Учебные платформы и онлайн-школы (баннеры, интеграции) Студенческие форумы и паблики ВК (где сидит ЦА)

Монетизация Ограниченное число бесплатных сканирований в день / месяц Платные опции: снятие лимитов, сканирование текстов на других языках Возможна подписка для активных студентов (безлимит)

Конкурентное преимущество (уникальность) Ни один конкурент (мобильные приложения или сайты-OCR) не использует дообученную ИИ-модель, которая связывает текущий распознанный текст с историей предыдущих анализов. Это даёт не просто символы, а осмысленный, скорректированный и связанный результат — как если бы текст перепечатал человек, а не робот.

---

## 🙏 Acknowledgments

- [TrOCR](https://github.com/microsoft/unilm/tree/master/trocr) by Microsoft
- [raxtemur/trocr-base-ru](https://huggingface.co/raxtemur/trocr-base-ru) for Russian language

---
