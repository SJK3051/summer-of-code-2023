FROM python:3.10-slim

WORKDIR /ml
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "model.py"]

