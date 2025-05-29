FROM python:3.13-alpine AS builder1

WORKDIR /app

COPY requirements.txt .

RUN pip install --upgrade pip setuptools wheel && \
    pip install --no-cache-dir --prefix=/install -r requirements.txt

COPY . .


FROM python:3.13-alpine

WORKDIR /app

# Copy the installed dependencies from the previous stage
COPY --from=builder1 /install /usr/local

# Copy the application source code
COPY --from=builder1 /app .

# Expose port 5000
EXPOSE 5000

CMD ["python","app.py"]