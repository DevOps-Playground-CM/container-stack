#  Dockerized Flask Medical Care App

This project is a  production-ready Flask application designed for deployment in a Docker container using a multi-stage build. It serves as a boilerplate for lightweight Python web applications.

## 📁 Project Structure

dockerized-flask-app/
├── static/ # Static assets (CSS, images, JS)
├── templates/ # HTML templates (e.g., index.html)
├── app.py # Main Flask application
├── requirements.txt # Python dependencies
├── Dockerfile # Docker build instructions
└── README.md # Project documentation


---

##  Prerequisites

- [Python 3.x](https://www.python.org/)
- [Docker](https://www.docker.com/get-started)
- [pip](https://pip.pypa.io/en/stable/)

## Create a virtual environment and install dependencies:

python3 -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt

## Start the Flask app:

python app.py
Access the app at: http://localhost:5000

## Run with Docker
### Dockerfile Command-by-Command 
#### Stage 1: Build Dependencies

```FROM python:3.13-alpine AS builder1```
Uses a small and secure base image (python:3.13-alpine)

AS builder1 gives this stage a name for later reference (multi-stage builds)

```WORKDIR /app```
Sets the working directory inside the container to /app

```COPY requirements.txt .```
Copies only the requirements file into the container for better caching

```RUN pip install --upgrade pip setuptools wheel && \```
    ```pip install --no-cache-dir --prefix=/install -r requirements.txt```
Installs pip, setuptools, and wheel

Installs all required Python packages into the /install directory to isolate them from system paths

```COPY . .```
Copies all other application files into the container

#### Stage 2: Final Runtime Image

```FROM python:3.13-alpine```
Starts a new stage with a clean base image for smaller final size

```WORKDIR /app```
Sets working directory again (this is a fresh container)

```COPY --from=builder1 /install /usr/local```
Copies only the installed Python dependencies from the builder stage into the final container

``COPY --from=builder1 /app .```
Copies the actual application source code from the builder stage

```EXPOSE 5000```
Tells Docker that the container will listen on port 5000 (Flask’s default)

```CMD ["python", "app.py"]```
The default command to run when the container starts: launch the Flask app

## Build the Docker Image

```docker build -t flask-medical-app .```
## Run the Docker Container
 
```docker run -p 5000:5000 flask-medical-app```
Open in your browser: http://localhost:5000
