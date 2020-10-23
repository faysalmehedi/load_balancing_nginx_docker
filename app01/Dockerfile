FROM python:3.8-slim

WORKDIR /app

COPY requirements.txt .
COPY app.py .

RUN pip install -r requirements.txt


Expose 5000

CMD ["python" , "app.py"]