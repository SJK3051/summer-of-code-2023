# Use official Python image
FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set work directory
WORKDIR /backend

# Install system dependencies for PostgreSQL & build tools
RUN apt-get update && apt-get install -y \
    libpq-dev gcc python3-dev musl-dev \
    && rm -rf /var/lib/apt/lists/*

# Install dependencies
COPY requirements.txt /backend/
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy project files
COPY . /backend/

# Run database migrations + collect static
RUN python manage.py collectstatic --noinput || true

# Expose backend port
EXPOSE 8000

# Start Django using Gunicorn
CMD ["gunicorn", "app.wsgi:application", "--bind", "0.0.0.0:8000"]
