# MLflow on AWS - Wine Quality Prediction

A comprehensive machine learning project demonstrating MLflow experiment tracking and model management deployed on AWS infrastructure. This project predicts wine quality using ElasticNet regression with full MLops pipeline integration.

## 🚀 Features

- **Machine Learning Model**: ElasticNet regression for wine quality prediction
- **Experiment Tracking**: Complete MLflow integration with parameter and metric logging
- **Model Registry**: Automated model versioning and registration
- **Cloud Deployment**: AWS EC2 + S3 integration for scalable MLflow server
- **Remote Tracking**: Production-ready MLflow tracking server setup

## 📊 Dataset

- **Source**: Red Wine Quality Dataset from UCI ML Repository
- **Features**: 11 physicochemical properties of wine
- **Target**: Wine quality score (0-10)
- **Size**: 1599 samples

## 🎯 Metrics Tracked

- **RMSE** (Root Mean Square Error)
- **MAE** (Mean Absolute Error) 
- **R² Score** (Coefficient of Determination)

## 🛠️ Tech Stack

- **ML Framework**: scikit-learn
- **Experiment Tracking**: MLflow
- **Cloud Platform**: AWS (EC2, S3, IAM)
- **Languages**: Python
- **Libraries**: pandas, numpy, sklearn

## 📋 Prerequisites

- AWS Account with appropriate permissions
- Python 3.7+
- AWS CLI configured
- Git

## ⚙️ MLflow on AWS Setup

### 1. AWS Console Setup
1. Login to AWS console
2. Create IAM user with **AdministratorAccess** policy
3. Note down Access Key ID and Secret Access Key

### 2. Local AWS CLI Configuration
```bash
aws configure
# Enter your AWS Access Key ID
# Enter your AWS Secret Access Key  
# Enter your preferred region (e.g., us-east-1)
# Enter output format (json)
```

### 3. S3 Bucket Creation
```bash
# Create S3 bucket for MLflow artifacts
aws s3 mb s3://your-mlflow-bucket-name
```

### 4. EC2 Instance Setup
1. Launch Ubuntu EC2 instance (t2.micro for testing)
2. Configure Security Group:
   - Add inbound rule: **Port 5000**, Source: **0.0.0.0/0** (or your IP)
   - Keep SSH (Port 22) access
3. Connect to EC2 instance

### 5. EC2 MLflow Server Installation
```bash
# Update system packages
sudo apt update

# Install Python and package managers
sudo apt install python3-pip
sudo apt install pipenv
sudo apt install virtualenv

# Create MLflow directory
mkdir mlflow
cd mlflow

# Install dependencies
pipenv install mlflow
pipenv install awscli
pipenv install boto3

# Activate virtual environment
pipenv shell

# Configure AWS credentials on EC2
aws configure
```

### 6. Start MLflow Server
```bash
# Start MLflow server with S3 artifact store
mlflow server -h 0.0.0.0 --default-artifact-root s3://your-mlflow-bucket-name

# Server will run on: http://your-ec2-public-ip:5000
```

### 7. Local Environment Setup
```bash
# Set MLflow tracking URI in your local environment
export MLFLOW_TRACKING_URI=http://your-ec2-public-ip:5000/

# For permanent setup, add to ~/.bashrc or ~/.zshrc
echo 'export MLFLOW_TRACKING_URI=http://your-ec2-public-ip:5000/' >> ~/.bashrc
```

## 🚀 Usage

### Basic Usage
```bash
# Run with default parameters (alpha=0.5, l1_ratio=0.5)
python app.py

# Run with custom parameters
python app.py 0.1 0.7

# Parameters:
# - First argument: alpha (regularization strength)
# - Second argument: l1_ratio (ElasticNet mixing parameter)
```

### Example Runs
```bash
# Light regularization
python app.py 0.1 0.5

# Heavy regularization  
python app.py 1.0 0.8

# Ridge-like behavior
python app.py 0.5 0.1

# Lasso-like behavior
python app.py 0.5 0.9

## 🔍 Model Details

### ElasticNet Regression
- **Algorithm**: Linear regression with L1 and L2 regularization
- **Parameters**:
  - `alpha`: Controls overall regularization strength
  - `l1_ratio`: Balances L1 (Lasso) vs L2 (Ridge) regularization
- **Random State**: 42 (for reproducibility)

### Feature Engineering
- **Input Features**: All wine physicochemical properties
- **Target**: Wine quality scores
- **Split**: 75% training, 25% testing (random split)

## 📈 MLflow Tracking

### Logged Parameters
- `alpha`: ElasticNet regularization strength
- `l1_ratio`: L1 vs L2 regularization balance

### Logged Metrics  
- `rmse`: Root Mean Square Error
- `mae`: Mean Absolute Error
- `r2`: R-squared score

### Model Registry
- **Model Name**: `ElasticnetWineModel`
- **Automatic Registration**: Enabled for remote tracking servers
- **Versioning**: Automatic model versioning

## 🌐 Accessing MLflow UI

1. Open browser and navigate to: `http://your-ec2-public-ip:5000`
2. View experiments, compare runs, and manage models
3. Monitor training metrics and parameters
4. Download or deploy registered models

## 🔧 Troubleshooting

### Common Issues

1. **Connection Refused Error**
   ```bash
   # Check if MLflow server is running
   ps aux | grep mlflow
   
   # Restart MLflow server if needed
   mlflow server -h 0.0.0.0 --default-artifact-root s3://your-bucket
   ```

2. **AWS Credentials Error**
   ```bash
   # Verify AWS configuration
   aws sts get-caller-identity
   
   # Reconfigure if needed
   aws configure
   ```

3. **S3 Permission Error**
   - Ensure IAM user has S3 full access
   - Check bucket name and region

4. **Security Group Issues**
   - Verify port 5000 is open in EC2 security group
   - Check source IP restrictions

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- MLflow team for the excellent MLOps platform
- UCI ML Repository for the wine quality dataset
- AWS for cloud infrastructure services

## 📞 Contact

- **GitHub**: [@Bharath2805](https://github.com/Bharath2805)
- **Project Link**: [https://github.com/Bharath2805/mlflow_aws](https://github.com/Bharath2805/mlflow_aws)

---

⭐ **Star this repository if you found it helpful!** ⭐