# mlops-train-and-serve-model
This project implements a Continuous Training (CT) and Continuous Deployment (CD) pipeline using GitHub Actions.

## Continuous Training
Every time a commit is pushed to the repository, the CT workflow is triggered to:
1. **Train**: Run `train/train_model.py` to retrain the model on the latest code/data.
2. **Package**: Save the trained model and metadata in the `artifacts` directory.
3. **Upload**: Store the build artifacts for future use or deployment.

## Continuous Deployment
Upon successful completion of the training workflow on the `main` branch, the CD pipeline is automatically triggered to:
1. **Fetch**: Download the freshly trained model artifact.
2. **Build**: Create a Docker image containing the application and the new model.
3. **Push**: Publish the Docker image to the GitHub Container Registry (ghcr.io).

## Usage

### Train the model
```bash
python train/train_model.py
```

### Local Prediction Test
```bash
python train/test_predict_model.py --input "[5.1, 3.5, 1.4, 0.2]"
```

### Serve Locally (Flask)
```bash
python serve/app.py
```

### Run with Docker
```bash
docker run -p 5001:5001 ghcr.io/vidon/mlops-train-and-serve-model:latest
```
