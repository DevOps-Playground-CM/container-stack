# Use the official Node.js 20 Alpine image as the base
FROM node:23-alpine AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

FROM node:23-alpine

WORKDIR /app

# Copy built app from builder stage to final image
COPY --from=builder /app ./

# Expose port 3000 to the host
EXPOSE 3000

# Define the command to run the application
CMD ["node","app.js"]