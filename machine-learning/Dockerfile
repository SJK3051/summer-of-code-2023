FROM python:3.10-slim

# Set workdir
WORKDIR /machine-learning

# Copy requirements first for caching
COPY requirements.txt .

# Install dependencies with verbose logs (avoids Jenkins silent timeout)
RUN pip install --no-cache-dir -r requirements.txt -v

# Copy app code
COPY . .

# Expose port
EXPOSE 5000

# Run app
CMD ["python", "app.py"]
