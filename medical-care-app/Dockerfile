# Uses a small and secure base image (python:3.13-alpine)
FROM python:3.13-alpine AS builder1

# Sets the working directory inside the container to /app
WORKDIR /app

# Copies only the requirements file into the container for better caching
COPY requirements.txt .

# Installs all required Python packages into the /install directory to isolate them from system paths
RUN pip install --upgrade pip setuptools wheel && \
    pip install --no-cache-dir --prefix=/install -r requirements.txt

#     Copies all other application files into the container
COPY . .

# Starts a new stage with a clean base image for smaller final size
FROM python:3.13-alpine

# Sets working directory again (this is a fresh container)
WORKDIR /app

# Copy the installed dependencies from the previous stage
COPY --from=builder1 /install /usr/local

# Copy the application source code
COPY --from=builder1 /app .

# Expose port 5000
EXPOSE 5000

# The default command to run when the container starts: launch the Flask app
CMD ["python","app.py"]