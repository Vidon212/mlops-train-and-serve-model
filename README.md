# mlops-train-and-serve-model
This project implements a Continuous Training (CT) pipeline using GitHub Actions.

## Continuous Training
Every time a commit is pushed to the repository, the CI workflow is triggered to:
1. **Train**: Run `train_model.py` to retrain the model on the latest code/data.
2. **Package**: Save the trained model and metadata in the `artifacts` directory.
3. **Upload**: Store the build artifacts for future use or deployment.

This ensures the model is always up-to-date with the latest changes in the codebase.

## Continuous Deployment
Upon successful completion of the training workflow on the `main` branch, the CD pipeline is automatically triggered to:
1. **Fetch**: Download the freshly trained model artifact.
2. **Build**: Create a Docker image containing the application and the new model.
3. **Push**: Publish the Docker image to the GitHub Container Registry (ghcr.io).

## Docker
To run the container manually:
```bash
docker run -p 5001:5001 ghcr.io/YOUR_USERNAME/mlops-train-and-serve-model:latest
```

## Usage

### Train the model
```bash
python train_model.py
```

### Predict with the model
```bash
python predict_model.py --input "[5.1, 3.5, 1.4, 0.2]"
```
