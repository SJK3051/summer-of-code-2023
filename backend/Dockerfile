FROM python:3.10-slim

WORKDIR /backend

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt -v

COPY . .

EXPOSE 8080

CMD ["python", "server.py"]
