# MERN Stack CI/CD Pipeline

This repository contains a MERN (MongoDB, Express, React, Node.js) stack application with a complete CI/CD pipeline using GitHub Actions for automated testing, building, and deployment to an EC2 instance.

## Project Structure

- `frontend/`: React application built with Vite
- `backend/`: Express.js API server with MongoDB connection
- `.github/workflows/`: CI/CD configuration

## CI/CD Pipeline

The CI/CD pipeline consists of three main stages:

### 1. Test Stage
- Runs on every push to main and on pull requests
- Sets up Node.js environment with caching
- Installs dependencies for both frontend and backend
- Creates necessary environment variables
- Runs linting on the frontend code

### 2. Build Stage
- Runs after successful tests
- Builds the frontend application using Vite
- Creates build artifacts for deployment
- Uploads artifacts for the deployment stage

### 3. Deploy Stage
- Runs only on pushes to the main branch
- Downloads build artifacts
- Transfers files to EC2 instance using SCP
- Sets up environment variables on the server
- Restarts the application using PM2
- Verifies deployment success

## Required Secrets

The following secrets need to be configured in your GitHub repository:

- `EC2_HOST`: The hostname or IP address of your EC2 instance
- `EC2_USER`: The username for SSH access (typically 'ubuntu' or 'ec2-user')
- `EC2_KEY`: The private SSH key for accessing your EC2 instance
- `MONGO_URI`: MongoDB connection string

## Local Development

### Backend
```bash
cd backend
npm install
# Create a .env file with MONGO_URI and PORT
npm start
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

## Deployment

Deployment happens automatically when changes are pushed to the main branch. The workflow:

1. Builds the React frontend
2. Copies the backend code and frontend build to the EC2 instance
3. Installs dependencies on the server
4. Sets up environment variables
5. Starts/restarts the application using PM2

## Server Requirements

- Node.js 20+
- PM2 (Process Manager)
- MongoDB access (via connection string)
