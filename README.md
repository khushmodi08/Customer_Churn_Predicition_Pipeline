# Customer Churn Prediction - End-to-End ML Pipeline

A comprehensive data management pipeline for customer churn prediction, implementing all stages from data ingestion to model deployment with automated versioning and monitoring.

## Project Overview

This project implements a complete end-to-end machine learning pipeline for predicting customer churn in telecommunications. The pipeline automates the entire ML workflow including data collection, validation, feature engineering, model training, and deployment with comprehensive logging and versioning.

## Dataset

**Primary Dataset**: IBM Telco Customer Churn Dataset
- **Source**: Kaggle - https://www.kaggle.com/datasets/blastchar/telco-customer-churn
- **Size**: 7,043 customers with 21 features
- **Target**: Binary churn classification (Yes/No)

### Dataset Features:
- **Demographics**: gender, SeniorCitizen, Partner, Dependents
- **Services**: PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
- **Account**: Contract, PaperlessBilling, PaymentMethod
- **Financial**: MonthlyCharges, TotalCharges
- **Behavioral**: tenure (months with company)
- **Target**: Churn (Yes/No)

## Complete Pipeline Architecture

### Pipeline Steps (main_pipeline.py):

1. **Step 1: Problem Formulation** - Business problem definition and objectives
2. **Step 2: Data Ingestion** - Fetch data from multiple sources (CSV + Hugging Face API)
3. **Step 3: Raw Data Storage** - Organize and catalog raw data
4. **Step 4: Data Validation** - Validate data quality and integrity
5. **Step 5: Data Preparation** - Clean and preprocess data
6. **Step 6: Data Transformation** - Feature engineering and storage
7. **Step 7: Feature Store** - Manage engineered features
8. **Step 8: Data Versioning** - DVC-based version control for datasets
9. **Step 9: Model Training** - Train and evaluate ML models

## Project Structure

```
churn-prediction-pipeline/
├── config/                        # Configuration files
│   ├── dvc/                       # DVC configuration
│   │   ├── dvc.yaml               # Pipeline definition
│   │   ├── dvc.lock               # Pipeline lock file
│   │   └── .dvcignore             # DVC ignore patterns
│   ├── env/                       # Environment configuration
│   │   └── .env.example           # Environment template
│   └── README.md                  # Configuration guide
├── scripts/                       # Setup and utility scripts
│   ├── setup_project.sh           # Complete project setup
│   ├── setup_dvc.sh               # DVC setup script
│   └── setup_dvc_credentials.sh   # DVC credentials setup
├── src/                           # Source code
│   ├── data_ingestion.py          # Step 2: Data ingestion
│   ├── data_validation.py         # Step 4: Data validation
│   ├── data_preparation.py        # Step 5: Data preparation
│   ├── data_transformation_storage.py # Step 6: Data transformation
│   ├── feature_store.py           # Step 7: Feature store
│   ├── data_versioning.py         # Step 8: Data versioning
│   ├── build_model.py             # Step 9: Model training
│   └── utils/                     # Utility functions
├── data/                          # Data storage (DVC tracked)
│   ├── raw/                       # Raw ingested data
│   ├── cleaned/                   # Cleaned data
│   ├── processed/                 # Transformed data
│   │   └── training_sets/         # ML-ready datasets
│   ├── feature_store/             # Feature store
│   ├── eda/                       # Exploratory data analysis
│   │   ├── raw/                   # Raw data EDA
│   │   └── cleaned/               # Cleaned data EDA
│   └── models/                    # Trained models
├── database/                      # Database setup
│   └── init.sql                   # SQLite schema
├── docs/                          # Documentation
│   ├── DVC_Data_Versioning_Guide.md # DVC guide
│   └── DM4ML_Assignment_Detailed_Instructions.md
├── logs/                          # Pipeline logs
├── reports/                       # Generated reports
├── Dockerfile                     # Docker configuration
├── docker-compose.yml             # Docker services
├── requirements.txt               # Python dependencies
├── main_pipeline.py               # Main pipeline runner
├── problem_formulation.md         # Business problem definition
├── dvc.yaml -> config/dvc/dvc.yaml    # Symbolic link
├── dvc.lock -> config/dvc/dvc.lock    # Symbolic link
├── .dvcignore -> config/dvc/.dvcignore # Symbolic link
├── .env.example -> config/env/.env.example # Symbolic link
└── README.md                      # This file
```


## Pipeline Components

### 1. Data Ingestion (`src/data_ingestion.py`)
- **Purpose**: Fetch data from multiple sources
- **Features**: CSV loading, Hugging Face API integration
- **Output**: Raw data in `data/raw/`
- **Logs**: `logs/data_ingestion.log`

### 2. Raw Data Storage (`src/raw_data_storage.py`)
- **Purpose**: Organize and catalog raw data
- **Features**: Directory structure, data catalog
- **Output**: Organized data hierarchy
- **Logs**: `logs/raw_data_storage.log`

### 3. Data Validation (`src/data_validation.py`)
- **Purpose**: Validate data quality and integrity
- **Features**: Schema validation, quality checks, statistical analysis
- **Output**: Validation reports in `reports/validation_reports/`
- **Logs**: `logs/data_validation.log`

### 4. Data Preparation (`src/data_preparation.py`)
- **Purpose**: Clean and preprocess raw data
- **Features**: Missing value handling, categorical encoding, data type conversion
- **Output**: Cleaned data in `data/cleaned/churn_data_cleaned.csv`
- **Logs**: `logs/data_preparation.log`

### 5. Data Transformation (`src/data_transformation_storage.py`)
- **Purpose**: Engineer features and store in database
- **Features**: Feature engineering, scaling, SQLite storage
- **Output**: Transformed features in `data/processed/training_sets/`
- **Logs**: `logs/data_transformation_storage.log`

### 6. Feature Store (`src/feature_store.py`)
- **Purpose**: Manage engineered features
- **Features**: Feature retrieval API, metadata tracking
- **Output**: Feature store in `data/feature_store/`
- **Logs**: `logs/feature_store.log`

### 7. Data Versioning (`src/data_versioning.py`)
- **Purpose**: DVC-based version control for datasets
- **Features**: Git-like versioning, reproducibility, collaboration
- **Output**: DVC-tracked data with `.dvc` files
- **Logs**: `logs/data_versioning.log`

#### DVC Data Versioning Features:
- **Automatic Versioning**: Each pipeline step creates a version
- **Git Integration**: Versions tracked in Git with tags
- **Reproducibility**: Exact data states can be recreated
- **Remote Storage**: Optional cloud storage integration
- **Collaboration**: Team can work with consistent data versions

### 8. Model Training (`src/build_model.py`)
- **Purpose**: Train and evaluate ML models
- **Features**: Multiple algorithms, hyperparameter tuning, model evaluation
- **Output**: Trained models in `src/models/`
- **Logs**: `logs/build_model.log`

## Expected Performance

### Model Performance Targets:
- **Accuracy**: > 85%
- **Precision**: > 80%
- **Recall**: > 75%
- **F1-Score**: > 0.8
- **AUC-ROC**: > 0.85

### Business Impact:
- **Churn Reduction**: 5% decrease in quarterly churn rate
- **Cost Savings**: Reduced customer acquisition costs
- **Revenue Protection**: Maintained customer lifetime value

