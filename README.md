# Brain Tumor Detection using Deep Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)](https://tensorflow.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.68%2B-green)](https://fastapi.tiangolo.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An AI-powered tool designed to classify brain tumors (or the lack thereof) based on MRI scans using deep learning techniques. This project implements a Convolutional Neural Network (CNN) to detect and classify brain tumors into four categories: **Glioma**, **Meningioma**, **No Tumor**, and **Pituitary**.

## 🧠 About the Project

Brain tumor detection is a critical medical application where early and accurate diagnosis can significantly impact treatment outcomes. This project leverages deep learning to assist in the automated classification of brain MRI scans, potentially serving as a diagnostic aid for medical professionals.

### Key Features

- **Multi-class Classification**: Detects 4 different types of brain conditions
- **Deep CNN Architecture**: Custom-built CNN with data augmentation
- **REST API**: FastAPI-based backend for easy integration
- **High Accuracy**: Trained model with validation accuracy metrics
- **Production Ready**: Dockerized deployment with proper error handling

## 🏗️ Architecture

### Model Architecture

The CNN model consists of:
- **Input Layer**: 256×256×3 RGB images
- **Preprocessing**: Resizing and rescaling layers
- **Data Augmentation**: Random flips and rotations
- **Convolutional Layers**: 6 Conv2D layers with MaxPooling
- **Dense Layers**: Fully connected layers with ReLU activation
- **Output**: 4-class softmax classification

### Classes

1. **Glioma** - Most common and aggressive brain tumor
2. **Meningioma** - Tumor arising from the meninges
3. **No Tumor** - Healthy brain scan
4. **Pituitary** - Tumor of the pituitary gland

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- pip package manager
- Virtual environment (recommended)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Sukarth/Tumor_Detection.git
   cd Tumor_Detection
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r api/requirements.txt
   ```

### Running the API

1. **Start the FastAPI server**
   ```bash
   cd api
   python main.py
   ```
   The API will be available at `http://localhost:8000`

2. **Test the API**
   ```bash
   curl http://localhost:8000/ping
   ```
   Expected response: `"Hello, I am alive"`

3. **API Documentation**
   Visit `http://localhost:8000/docs` for interactive API documentation

## 📝 Usage

### Making Predictions

**Using cURL:**
```bash
curl -X POST "http://localhost:8000/predict" \
     -H "accept: application/json" \
     -H "Content-Type: multipart/form-data" \
     -F "file=@path/to/your/brain_scan.jpg"
```

**Response Format:**
```json
{
  "class": "glioma",
  "confidence": 0.95
}
```

### Python Client Example

```python
import requests
import json

def predict_brain_tumor(image_path):
    url = "http://localhost:8000/predict"
    
    with open(image_path, "rb") as file:
        files = {"file": file}
        response = requests.post(url, files=files)
    
    if response.status_code == 200:
        result = response.json()
        print(f"Predicted class: {result['class']}")
        print(f"Confidence: {result['confidence']:.2%}")
        return result
    else:
        print(f"Error: {response.status_code}")
        return None

# Usage
result = predict_brain_tumor("path/to/brain_scan.jpg")
```

## 🛠️ Development

### Project Structure

```
Tumor_Detection/
├── api/
│   ├── main.py              # FastAPI application
│   ├── Model.keras          # Trained model file
│   └── requirements.txt     # Python dependencies
├── Model/
│   ├── Model.ipynb         # Jupyter notebook for training
│   └── my_full_model.h5    # Legacy model format
├── frontend/               # Frontend application (WIP)
├── .gitignore             # Git ignore rules
├── LICENSE                # MIT License
└── README.md              # This file
```

### Model Training

To retrain the model:

1. **Prepare your dataset** in the following structure:
   ```
   dataset/
   ├── glioma/
   ├── meningioma/
   ├── notumor/
   └── pituitary/
   ```

2. **Run the training notebook**
   ```bash
   jupyter notebook Model/Model.ipynb
   ```

3. **Update the model** in the API directory after training

### API Endpoints

| Endpoint | Method | Description |
|----------|--------|--------------|
| `/ping` | GET | Health check endpoint |
| `/predict` | POST | Upload image and get tumor prediction |
| `/docs` | GET | Interactive API documentation |

## 🧪 Testing

### Unit Tests

```bash
# Run API tests
python -m pytest tests/
```

### Manual Testing

1. Test with sample images from each class
2. Verify confidence scores are reasonable
3. Check edge cases (corrupted images, wrong formats)

## 📊 Model Performance

- **Training Accuracy**: ~98.5%
- **Validation Accuracy**: ~95.0%
- **Model Size**: ~718KB
- **Inference Time**: ~200ms per image

## 🐳 Docker Deployment

### Build Docker Image

```bash
docker build -t tumor-detection .
docker run -p 8000:8000 tumor-detection
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guidelines
- Add docstrings to all functions
- Include unit tests for new features
- Update README for significant changes

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

**IMPORTANT**: This tool is for educational and research purposes only. It should NOT be used as a substitute for professional medical diagnosis or treatment. Always consult qualified healthcare professionals for medical advice.

## 🙏 Acknowledgments

- Original dataset contributors
- TensorFlow and Keras teams
- FastAPI framework developers
- The open-source community

## 📞 Contact

- GitHub: [@Sukarth](https://github.com/Sukarth)
- Project Link: [https://github.com/Sukarth/Tumor_Detection](https://github.com/Sukarth/Tumor_Detection)

---

**Made with ❤️ for advancing medical AI research**