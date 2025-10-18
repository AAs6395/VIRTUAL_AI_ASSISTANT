

# VIRTUAL_AI_ASSISTANT

**Your AI Health Companion** - An intelligent disease prediction system powered by machine learning that analyzes symptoms to predict potential diseases and provide health recommendations.

## 📋 Overview

MedicaAI is a web-based healthcare application that uses a Random Forest machine learning model to predict diseases based on user-reported symptoms. The system provides disease predictions with confidence scores, alternative diagnoses, symptom severity analysis, and recommended precautions.

## ✨ Key Features

- **🎯 Accurate Disease Prediction**: Machine learning model trained on comprehensive medical datasets
- **💬 Interactive Chat Interface**: User-friendly conversational UI for symptom input
- **🔍 Smart Symptom Matching**: Fuzzy matching to handle typos and variations in symptom names
- **📊 Confidence Scores**: Probability percentages for each prediction
- **🔄 Alternative Diagnoses**: Multiple possible diseases ranked by likelihood
- **⚕️ Health Recommendations**: Precautionary measures for predicted conditions
- **📈 Severity Analysis**: Symptom severity ratings on a 1-7 scale
- **💡 Symptom Suggestions**: Smart suggestions when symptoms are unrecognized
- **🌐 REST API**: JSON API endpoints for integration with other applications

## 🛠️ Technologies Used

### Backend
- **Flask**: Python web framework for REST API
- **scikit-learn**: Machine learning library for Random Forest classifier
- **pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **joblib**: Model serialization

### Frontend
- **HTML5/CSS3**: Modern responsive design
- **JavaScript**: Interactive user interface
- **Bootstrap** (optional): UI components

### Machine Learning
- **Random Forest Classifier**: Ensemble learning algorithm
- **Grid Search CV**: Hyperparameter optimization
- **Stratified K-Fold**: Cross-validation for model evaluation

## 🚀 Installation & Setup

### Prerequisites

- Python 3.7 or higher
- pip (Python package manager)
- Git

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/medicaai.git
cd medicaai
```

### Step 2: Create Virtual Environment (Recommended)

```bash
python -m venv .venv

# On Windows
.venv\Scripts\activate

# On macOS/Linux
source .venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Train the Model

Before running the application, you need to train the machine learning model:

```bash
python train_model.py
```

This will:
- Load the dataset from `dataset/dataset.csv`
- Train a Random Forest model with optimized hyperparameters
- Save the trained model to the `models/` directory
- Generate performance metrics and feature importance

### Step 5: Run the Application

```bash
python app.py
```

The application will start on `http://0.0.0.0:10000/` (or `http://127.0.0.1:10000/`)

## 📁 Project Structure

```
medicaai/
│
├── .github/                    # GitHub configuration files
├── .venv/                      # Virtual environment (gitignored)
├── __pycache__/               # Python cache files (gitignored)
│
├── dataset/                    # Medical datasets
│   ├── dataset.csv            # Main training dataset
│   ├── symptom_description.csv  # Disease descriptions
│   ├── symptom_precaution.csv   # Recommended precautions
│   └── symptom_severity.csv     # Symptom severity weights
│
├── models/                     # Trained model artifacts
│   ├── disease_rf_model.joblib      # Trained Random Forest model
│   ├── symptom_list.joblib          # List of all symptoms
│   ├── symptom_mapping.joblib       # Symptom-to-feature mapping
│   └── feature_importance.joblib    # Feature importance scores
│
├── static/                     # Static files (CSS, JS, images)
│   └── favicon.ico            # Website favicon
│
├── templates/                  # HTML templates
│   └── index.html             # Main chat interface
│
├── .gitignore                 # Git ignore file
├── app.py                     # Main Flask application
├── predict_disease.py         # Disease prediction logic
├── train_model.py             # Model training script
├── requirements.txt           # Python dependencies
├── render.yaml               # Render deployment configuration
└── README.md                 # Project documentation
```

## 💻 Usage

### Web Interface

1. Open your browser and navigate to `http://127.0.0.1:10000/`
2. Type your symptoms in the chat interface (comma-separated)
   - Example: "fever, cough, headache, fatigue"
3. Press Enter or click Send
4. View the AI-generated prediction with:
   - Primary disease prediction with confidence score
   - Disease description
   - Recommended precautions
   - Alternative possible diseases
   - Symptom severity analysis

### Command-Line Interface

You can also use the prediction system from the command line:

```bash
# Single prediction
python predict_disease.py --symptoms "fever, cough, headache"

# Interactive mode
python predict_disease.py --interactive
```

### REST API

#### Get All Symptoms
```bash
GET /api/symptoms
```

Response:
```json
{
  "status": "success",
  "symptoms": ["fever", "cough", "headache", ...]
}
```

#### Predict Disease
```bash
POST /api/predict
Content-Type: application/json

{
  "symptoms": "fever, cough, headache"
}
```

Response:
```json
{
  "status": "success",
  "messages": [...],
  "raw_results": {
    "top_prediction": {
      "disease": "Common Cold",
      "probability": 0.85,
      "description": "...",
      "precautions": [...]
    },
    "alternative_predictions": [...],
    "symptom_details": [...]
  }
}
```

## 📊 Model Performance

The Random Forest model is trained with:
- **Hyperparameter Tuning**: Grid Search with cross-validation
- **Class Balancing**: Handles imbalanced disease distributions
- **Feature Engineering**: One-hot encoding of symptoms
- **Validation Strategy**: Stratified K-Fold cross-validation

Typical performance metrics:
- **Accuracy**: ~85-95% (varies by dataset)
- **Cross-Validation Score**: Balanced accuracy across diseases
- **Feature Importance**: Identifies most predictive symptoms

## 🔧 Configuration

### Environment Variables

- `PORT`: Server port (default: 10000)
- `FLASK_ENV`: Environment mode (production/development)

### Model Configuration

Edit parameters in `train_model.py`:
```python
param_grid = {
    'n_estimators': [100, 200, 500],
    'max_depth': [None, 20, 40, 60],
    'min_samples_leaf': [1, 2, 4],
    'min_samples_split': [2, 5, 10]
}
```

## 🚀 Deployment

### Deploy on Render

The project includes a `render.yaml` configuration file for easy deployment:

1. Push your code to GitHub
2. Connect your repository to Render
3. Render will automatically deploy using the configuration

### Manual Deployment

1. Ensure all dependencies are installed
2. Train the model: `python train_model.py`
3. Set environment variables
4. Run: `python app.py`

## ⚠️ Important Disclaimers

- **Not a Medical Professional**: This tool is for educational and informational purposes only
- **Seek Professional Help**: Always consult with qualified healthcare providers for medical advice
- **No Diagnosis**: Predictions are probabilistic and should not be used for self-diagnosis
- **Emergency Situations**: Call emergency services for urgent medical conditions
- **Data Privacy**: Do not share sensitive personal health information

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Areas for Contribution

- Add more diseases and symptoms to the dataset
- Improve UI/UX design
- Add multi-language support
- Implement user authentication
- Add symptom search autocomplete
- Create mobile app version
- Improve model accuracy with deep learning

## 📈 Future Enhancements

- [ ] Patient history tracking
- [ ] Integration with wearable devices
- [ ] Chatbot with natural language processing
- [ ] Multi-language support
- [ ] Medical image analysis
- [ ] Telemedicine integration
- [ ] Appointment scheduling
- [ ] Medication reminder system

## 🐛 Known Issues

- Large datasets may increase initial model loading time
- Fuzzy matching may occasionally suggest incorrect symptoms
- Limited to diseases present in the training dataset

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Authors

Aashish Joshi - [AAs6395](https://github.com/AAs6395)

## 🙏 Acknowledgments

- Medical datasets from public health repositories
- scikit-learn community for machine learning tools
- Flask framework developers
- Healthcare professionals who reviewed the symptom data

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Email: jaashish109@gmail.com

---

**⚕️ Remember**: This is an AI assistant tool, not a replacement for professional medical advice. Always consult healthcare providers for medical concerns.


