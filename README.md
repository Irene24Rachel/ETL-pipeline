# ETL Pipeline for Data Preprocessing

A Python-based ETL (Extract, Transform, Load) pipeline designed to automate data extraction, validation, preprocessing, feature engineering, transformation, and reporting.

This project demonstrates a structured approach to preparing raw data for downstream data science and machine learning workflows.

## 🚀 Project Overview

Machine learning projects depend heavily on clean, consistent, and properly transformed data.

This project implements an ETL workflow that:

- Extracts data from CSV files
- Explores missing values
- Validates input data
- Performs feature engineering
- Scales numerical features
- Encodes categorical features
- Transforms data using scikit-learn pipelines
- Saves processed data
- Generates an automated JSON report
- Provides logging throughout the pipeline

## 🔄 ETL Workflow

```text
Raw CSV Data
     │
     ▼
  Extract
     │
     ▼
  Explore
     │
     ▼
  Validate
     │
     ▼
Feature Engineering
     │
     ▼
 Data Transformation
     │
     ├── Numerical Features
     │       └── StandardScaler
     │
     └── Categorical Features
             └── OneHotEncoder
     │
     ▼
Processed Dataset
     │
     ▼
Automated Report
```

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Pipeline development |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Scikit-learn | Data preprocessing |
| StandardScaler | Numerical feature scaling |
| OneHotEncoder | Categorical feature encoding |
| ColumnTransformer | Feature-specific transformations |
| Pipeline | Preprocessing workflow |
| Logging | Execution tracking |
| JSON | Automated reporting |

## 📋 Pipeline Stages

### 1. Extract

The pipeline loads structured CSV data using Pandas.

### 2. Explore

The pipeline examines the dataset and generates a summary of missing values.

### 3. Validate

Input data is validated before further processing.

### 4. Feature Engineering

Additional features are generated from existing data.

Examples include:

- Income per age
- Income category

### 5. Transform

Numerical and categorical features are processed separately.

Numerical features are scaled using:

```python
StandardScaler()
```

Categorical features are encoded using:

```python
OneHotEncoder()
```

A `ColumnTransformer` combines the preprocessing workflows.

### 6. Load

The transformed dataset is saved as a processed CSV file.

### 7. Reporting

The pipeline generates a JSON report containing information such as:

- Number of rows
- Number of columns
- Report generation timestamp

## 📁 Project Structure

```text
ETL-pipeline/
│
├── etl_pipeline.py
├── README.md
├── requirements.txt
└── .gitignore
```

The pipeline automatically creates the required data directories during execution.

## ▶️ How to Run

### 1. Clone the repository

```bash
git clone https://github.com/Irene24Rachel/ETL-pipeline.git
```

### 2. Navigate to the project

```bash
cd ETL-pipeline
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the pipeline

```bash
python etl_pipeline.py
```

## 📊 Output

The pipeline generates:

- Raw sample data
- Processed data
- JSON processing report
- Execution logs

The processed dataset can be used as an input for further data analysis or machine learning workflows.

## 🎯 Learning Outcomes

This project provided practical experience with:

- ETL workflow design
- Data validation
- Data preprocessing
- Feature engineering
- Numerical feature scaling
- Categorical feature encoding
- Scikit-learn preprocessing pipelines
- Logging
- Automated reporting

## 🔮 Future Improvements

Planned improvements include:

- Add automated data quality tests
- Move configuration to an external configuration file
- Add unit tests
- Add command-line arguments
- Add GitHub Actions CI/CD
- Connect the pipeline to a machine learning model
- Add data visualization
- Add data quality monitoring
- Integrate the pipeline with a real-world dataset

## 👩‍💻 Author

**Irene Rachel S**

B.Tech Information Technology Student  
Aspiring AI/ML Developer
