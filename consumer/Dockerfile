FROM python:2.7-slim

ENV PYTHONPATH=/usr/src/app
WORKDIR /app

COPY requirements.txt /app/

# Install necessary tools before installing your requirements
RUN pip install --upgrade pip setuptools wheel && \
    pip install --no-cache-dir -r requirements.txt

COPY consumer.py /app/

EXPOSE 9422
