# MLOps with ZenML and MLflow

## 📌 Project Overview

This project is a simple test to understand the basics of MLOps using **ZenML** and **MLflow**. It follows a basic machine learning workflow, including:

- Data ingestion
- Data cleaning
- Data splitting (train/test)
- Model training
- Model evaluation
- Deployment decision based on model performance

## 📂 Project Structure

### Directories
- **`data/`**: Contains the dataset used for training and inference.
- **`src/`**: Contains helper classes for various ML steps:
  - `data_cleaning.py`
  - `evaluation.py`
  - `model_dev.py`
- **`steps/`**: Contains ML pipeline steps:
  - `clean_data.py`
  - `evaluate_model.py`
  - `ingest_data.py`
  - `model_train.py`
- **`pipelines/`**: Defines training and deployment pipelines:
  - `deployment_pipeline.py`
  - `training_pipeline.py`
  - `utils.py` (helper functions for deployment)

### Main Scripts
- **`run_training.py`**: Runs the training pipeline.
- **`run_deployment.py`**: Runs the deployment pipeline.

### `deployment_pipeline.py`
This script defines a continuous deployment pipeline using ZenML. The pipeline:
- Ingests data
- Cleans and splits it
- Trains a model
- Evaluates the model's performance
- Deploys the model if it meets a minimum accuracy threshold (default: 0.92)

### `run_deployment.py`
This script manages the deployment process. It allows running:
- The deployment pipeline to train and deploy a model (`--config deploy`)
- The inference pipeline to make predictions (`--config predict`)
- Both (`--config deploy_and_predict` by default)

## 📦 Requirements

Before running the project, install the necessary dependencies:

```bash
pip install -r requirements.txt
```

## ▶️ Running the Project

1. Navigate to the project directory:

   ```bash
   cd MLOps-ZenML-Introduction
   ```

2. Run the training pipeline:
   ```bash
   python run_training.py
   ```

3. Run the deployment script:
   ```bash
   python run_deployment.py --config deploy
   ```
   or
   ```bash
   python run_deployment.py --config predict
   ```

## 🖥️ Running on Windows

ZenML requires background processes using **daemon**, which is not supported on Windows. To work around this:

- If your BIOS supports virtualization, you can use **Windows Subsystem for Linux (WSL)** to run a Linux environment in VSCode.
- If WSL is not available (as in my case), an alternative is to use **Google Cloud Platform (GCP)**:
  1. Create a **Virtual Machine (VM)** on GCP with Ubuntu.
  2. Connect to the VM from your local machine via SSH.
  3. Transfer project files to the VM.
  4. Set up a virtual environment and install dependencies:
     ```bash
     pip install -r requirements.txt
     ```
  5. Run the deployment commands in the VM:
     ```bash
     python run_deployment.py --config deploy
     python run_deployment.py --config predict
     ```

**Note:** The **ZenML dashboard** and **MLflow UI** cannot be launched on GCP due to cloud service restrictions.

## 🚀 Future Improvements

- Add more robust data validation steps.
- Explore other model deployment strategies.
- Automate the workflow using CI/CD pipelines.
