FROM python:3.10-slim

# Set work directory
WORKDIR /backend

# Install system dependencies for psycopg2 & Django
RUN apt-get update && apt-get install -y gcc libpq-dev && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt -v

# Copy Django project
COPY . .

# Expose port
EXPOSE 8080

# Run Django with Gunicorn
CMD ["gunicorn", "app.wsgi:application", "--bind", "0.0.0.0:8080"]
