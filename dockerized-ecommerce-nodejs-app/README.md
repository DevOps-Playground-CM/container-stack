# Dockerized Node.js Starter App

This project is a starter template for building and deploying a Node.js application using Docker. It provides a simple Express.js server setup and demonstrates how to containerize the application for consistent development and deployment environments.

## Project Structure

dockerized-nodejs-starter-app/
├── app.js       
├── node_modules
├── piblic
├── views    
├── package.json          
├── Dockerfile            
├── package-lock.json
├── README.md

## Prerequisites
Ensure you have the following installed on your system:

Node.js (v14 or higher)

npm (comes with Node.js)

Docker

## 1. Install Dependencies

```npm install```
## 2. Run the Application Locally
```node app.js```
The application will start on http://localhost:3000

## Dockerizing the Application
FROM node:20-alpine:
Specifies the base image. Here, we're using the official Node.js version 20 image based on Alpine Linux, which is lightweight and suitable for production environments.

WORKDIR /app:
Sets the working directory inside the container to /app. All subsequent commands will be run from this directory.

COPY package*.json ./:
Copies both package.json and package-lock.json to the working directory. The asterisk (*) ensures both files are copied if they exist.

RUN npm install:
Installs the project dependencies defined in package.json.

COPY . .:
Copies the rest of the application code to the working directory inside the container.

EXPOSE 3000:
Informs Docker that the container listens on port 3000. This is the port our Node.js application uses.

CMD ["node", "app.js"]:
Defines the command to run the application when the container starts.

## Building the Docker Image
To build the Docker image, run the following command in the project root directory:

```docker build -t nodejs-starter-app .```

## Running the Docker Container
After building the image, you can run the container:

```docker run -p 3000:3000 nodejs-starter-app```
This maps port 3000 of the container to port 3000 on your host machine. Access the application at http://localhost:3000.

## Stopping the Container
To stop the running container, first find the container ID:

```docker ps```
Then stop it using:

```docker stop <container_id>```
Replace <container_id> with the actual ID of your running container.