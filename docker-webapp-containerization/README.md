# How to Containerize a Web App Using Docke

Follow these steps to containerize your web app using Docker and serve it locally.

## Pre-requisites
Docker installed and running
Git installed
A simple web app (HTML, CSS, JS or similar)

## Steps to Follow
Clone Your Web App Repository 

git clone https://github.com/your-username/your-web-app.git cd your-web-app 

Create a Dockerfile in the Project Root

Use a base image like nginx:alpine

Copy your app files to /usr/share/nginx/html
Expose port 80

### Build the Docker Image
docker build -t portfolio . 
### Check if the Image Was Created
docker images 
### Run the Container
docker run -d -p 8080:80 "portfolio image id"
### Verify the Container is Running
docker ps 

### Open Your Browser
Go to: http://localhost:8080 to see your app live.
Done