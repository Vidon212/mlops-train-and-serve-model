FROM python:3.12-slim

WORKDIR /app

# Copy requirements from root (build context must be root)
COPY requirements.txt .

RUN python -m pip install --upgrade pip
RUN python -m pip install -r requirements.txt

# Copy the entire project
COPY . .

EXPOSE 5001

# Run the app from the root module path
CMD ["python", "serve/app.py"]
