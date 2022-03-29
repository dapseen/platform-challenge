
# Create a Multi stage build
FROM python:3.9-alpine AS base

WORKDIR /usr/src/app

COPY requirements.txt ./

RUN pip install --no-cache-dir --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY . .



CMD ["python", "./main.py"]

