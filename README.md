
# ⚡ Real-Time EV Charging Station Availability & Demand Predictor 🚗

A robust, end-to-end data engineering and machine learning pipeline designed to predict electric vehicle (EV) charging station availability and demand. This project integrates **MongoDB, PyMongo, Pandas, NumPy, Apache PySpark, and Machine Learning** to process charging station data, identify demand patterns, and predict charger availability.

The system uses distributed data processing and machine learning algorithms to help reduce range anxiety, improve charging station utilization, and support better EV charging infrastructure management.

## 📌 Project Overview

With the increasing adoption of electric vehicles, drivers and charging station operators face two major challenges:

1. **Range Anxiety:** Drivers need reliable information about charging station availability before arriving at a station.
2. **Demand Management:** Charging station operators need to understand demand patterns to improve resource utilization and reduce congestion.

This project addresses these challenges through a data engineering and machine learning pipeline that stores EV charging data in MongoDB, preprocesses the data using Pandas, performs scalable feature engineering with PySpark, and trains machine learning models to predict charging station availability and demand status.

### Key Features

- MongoDB integration for storing and retrieving charging station data.
- Data cleaning and preprocessing using Pandas and NumPy.
- Distributed data processing using Apache PySpark.
- Feature encoding and scaling using the PySpark ML pipeline.
- Machine learning classification using Random Forest and Logistic Regression.
- Model evaluation using Accuracy, Precision, Recall, Macro F1-score, and Confusion Matrix.
- Prediction of charging station availability and demand status.
- Support for inference on incoming charging station telemetry data.
- Visual analysis of model performance and prediction results.

## 🏗️ System Architecture

```text
          EV Charging Station Data
                     |
                     v
             +---------------+
             |   MongoDB     |
             | Data Storage  |
             +---------------+
                     |
                     v
             +---------------+
             |    PyMongo    |
             | Data Retrieval|
             +---------------+
                     |
                     v
             +---------------+
             | Pandas / NumPy|
             | Data Cleaning |
             +---------------+
                     |
                     v
             +---------------+
             |    PySpark    |
             | Feature        |
             | Engineering   |
             +---------------+
                     |
                     v
             +---------------+
             | Machine       |
             | Learning      |
             | Random Forest |
             | Logistic Reg. |
             +---------------+
                     |
                     v
             +---------------+
             | Model         |
             | Evaluation    |
             +---------------+
                     |
                     v
             +---------------+
             | Availability  |
             | & Demand      |
             | Prediction    |
             +---------------+
```

## 🔄 Project Workflow

### 1. Data Ingestion

EV charging station records are stored in MongoDB. The dataset may contain station identifiers, charger types, charging status, power consumption, utilization, timestamps, and demand indicators.

PyMongo connects the Python application to MongoDB and retrieves the required records for processing.

### 2. Data Cleaning and Preprocessing

Pandas and NumPy are used to prepare the raw data for machine learning.

Preprocessing operations include:

- Handling missing and duplicate records.
- Converting timestamps into appropriate formats.
- Correcting data types.
- Identifying invalid or inconsistent values.
- Preparing categorical and numerical features.

### 3. Feature Engineering with PySpark

PySpark processes the cleaned dataset and prepares features for machine learning.

The feature engineering pipeline may include:

- `StringIndexer` for converting categorical values into numerical indices.
- `OneHotEncoder` for encoding categorical features.
- `VectorAssembler` for combining input features into a feature vector.
- `StandardScaler` for scaling numerical features when appropriate.

The resulting feature vectors are used to train and evaluate the machine learning models.

### 4. Machine Learning Model Training

The project uses two classification algorithms:

**Random Forest Classifier**
- Combines multiple decision trees to improve prediction performance.
- Captures nonlinear relationships between charging station features.
- Supports feature importance analysis.
- Uses 300 trees when configured with 300 estimators or trees in the respective implementation.

**Logistic Regression**
- Provides a baseline classification model.
- Estimates class probabilities.
- Offers a simpler model for comparison with Random Forest.

Both models are trained using historical charging station data and evaluated on held-out test data.

### 5. Model Evaluation

The models are evaluated using the following metrics:

- **Accuracy:** Percentage of correctly classified records.
- **Precision:** Proportion of positive predictions that are correct.
- **Recall:** Proportion of actual positive records correctly identified.
- **Macro F1-score:** Average F1-score across classes, treating each class equally.
- **Confusion Matrix:** Displays correct and incorrect predictions for each class.

These metrics help compare the models and understand their performance across different availability or demand classes.

### 6. Prediction and Inference

After training, the selected model can process incoming charging station records and generate predictions.

The predictions can help identify:

- Whether a charging station is predicted to be available.
- Whether demand is expected to be high or low, depending on the target labels.
- Which stations may require further monitoring.
- Potential opportunities to improve charging station utilization.

**Note:** Predictions are based on the features and target labels used during training. Actual real-time operation requires a live data feed, regular data updates, and a deployed inference service.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| MongoDB | NoSQL database for charging station records |
| PyMongo | Python interface for MongoDB |
| Pandas | Data cleaning and manipulation |
| NumPy | Numerical operations |
| Apache PySpark | Distributed data processing |
| PySpark MLlib | Machine learning pipeline and classification |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| PowerShell / Windows / Linux | Execution environment |

## 📋 Prerequisites

Before running the project, ensure that the following are installed:

- Python 3.11 or another version compatible with your installed PySpark and dependencies.
- Java Development Kit (JDK) compatible with your Apache Spark version.
- Apache Spark and PySpark.
- MongoDB Community Server.
- Git.
- A terminal such as PowerShell, Command Prompt, or Linux Terminal.

**Compatibility note:** Verify the supported Python version for your chosen Spark release before installation. Do not assume every Python or Spark version is compatible with every dependency.

## 📦 Installation and Setup

### 1. Clone the Repository

Replace `your-username` with your GitHub username.

```bash
git clone https://github.com/your-username/ev-charging-demand-predictor.git
cd ev-charging-demand-predictor
```

### 2. Create a Virtual Environment

On Windows:

```powershell
py -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can run the environment's Python executable directly or use Command Prompt instead.

### 3. Install Dependencies

Upgrade pip and install the required packages:

```bash
python -m pip install --upgrade pip
python -m pip install numpy pandas matplotlib seaborn pymongo pyspark
```

If your implementation uses scikit-learn for additional evaluation or modeling, install it separately:

```bash
python -m pip install scikit-learn
```

### 4. Configure PySpark on Windows

Set the Python interpreter used by PySpark in PowerShell. Update the path to match your installation.

```powershell
$env:PYSPARK_PYTHON="C:\Path\To\Python\python.exe"
$env:PYSPARK_DRIVER_PYTHON="C:\Path\To\Python\python.exe"
```

Check the installed versions:

```powershell
python --version
java -version
pyspark --version
```

### 5. Start MongoDB

Ensure that MongoDB is running locally on:

```text
mongodb://localhost:27017/
```

For a local MongoDB installation, start the MongoDB service if it is not already running.

### 6. Configure the Database

Update the MongoDB connection settings in the project to match your environment.

Example:

```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["ev_charging_db"]
collection = db["charging_station_data"]
```

Use the database and collection names expected by your implementation.

### 7. Run the Project

Execute the main pipeline script from the project directory:

```bash
python main.py
```

If you use the Python launcher on Windows, you can also run:

```powershell
py -3 main.py
```

The script should execute the implemented data retrieval, preprocessing, feature engineering, training, evaluation, and prediction stages.

## 📊 Model Evaluation

The project compares Random Forest and Logistic Regression to determine which model performs better on the selected classification task.

The following results are illustrative reported values and should be replaced with actual outputs generated by your implementation.

| Model | Accuracy | Precision | Recall | Macro F1-score |
|---|---:|---:|---:|---:|
| Random Forest | 94.5% | 0.93 | 0.94 | 0.935 |
| Logistic Regression | 87.2% | 0.85 | 0.86 | 0.855 |

### Random Forest

The reported results indicate that Random Forest performs better than Logistic Regression across the listed metrics. This suggests that it may be more suitable for the dataset being evaluated.

### Logistic Regression

Logistic Regression provides a baseline against which the more flexible Random Forest model can be compared.

**Important:** These figures are not independently verified benchmark results. Use them only if they match your actual experiment outputs. Model performance depends on the dataset, feature selection, train-test split, class distribution, and model configuration.

### Confusion Matrix

A confusion matrix helps identify the types of classification errors made by each model. For charging station availability, false-positive predictions may be particularly important because a driver could be directed to a station predicted to be available when it is actually occupied or out of service.

## 📈 Expected Outcomes

The project aims to achieve the following outcomes:

1. Build a complete data pipeline connecting MongoDB with Python and PySpark.
2. Clean and transform EV charging station data for machine learning.
3. Develop classification models for charging station availability or demand status.
4. Compare Random Forest and Logistic Regression using standard evaluation metrics.
5. Identify the model that performs best on the test dataset.
6. Generate predictions for new charging station records.
7. Provide a foundation for future real-time charging station monitoring and demand forecasting.

## 🔮 Future Enhancements

- [ ] Integrate real-time charging station APIs and telemetry feeds.
- [ ] Incorporate weather, traffic, time-of-day, and holiday information.
- [ ] Develop time-series models for forecasting future charging demand.
- [ ] Build a dashboard displaying station availability and predicted demand.
- [ ] Add automated model retraining as new data becomes available.
- [ ] Deploy the pipeline on Databricks or AWS EMR.
- [ ] Create a REST API for serving model predictions.
- [ ] Implement dynamic pricing recommendations based on demand.
- [ ] Add monitoring for prediction errors, data quality, and model drift.
- [ ] Evaluate the system using temporal validation and real-world operational data.

## 🚧 Limitations

- Prediction quality depends on the availability and quality of historical data.
- Classification models cannot guarantee actual future charger availability.
- Real-time predictions require fresh telemetry and an operational inference pipeline.
- Demand forecasting over future time intervals may require dedicated time-series models.
- Performance metrics should be validated using unseen data and appropriate evaluation methods.

## 👨‍💻 Applications

This project can support:

- EV drivers looking for available charging stations.
- Charging station operators monitoring utilization.
- Smart city infrastructure planning.
- EV charging network optimization.
- Preliminary demand analysis for electricity distribution planning.

## 📁 Suggested Project Structure

```text
ev-charging-demand-predictor/
│
├── data/
│   └── charging_station_data.csv
│
├── models/
│   └── saved_model/
│
├── outputs/
│   ├── evaluation_metrics.csv
│   └── confusion_matrix.png
│
├── main.py
├── requirements.txt
├── README.md
└── .gitignore
```

This is a suggested structure. Adjust the folders and filenames to match the actual files in your repository.

## 📚 Conclusion

The **Real-Time EV Charging Station Availability & Demand Predictor** demonstrates how database technologies, distributed data processing, and machine learning can be combined to analyze EV charging station data.

MongoDB provides data storage, Pandas supports data preparation, and PySpark enables scalable feature engineering and model training. Random Forest and Logistic Regression provide a basis for comparing predictive performance.

The project establishes a foundation for developing more advanced EV charging analytics systems that can help improve station utilization, support demand management, and provide drivers with better information about charging availability.

---

**Technologies:** Python · MongoDB · PyMongo · Pandas · NumPy · Apache PySpark · Machine Learning

**Project Type:** Data Engineering and Machine Learning
