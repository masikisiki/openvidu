# OpenVidu Video Conferencing App (Development Setup)

This repository contains a video conferencing application built with OpenVidu and Angular. Follow these steps to set up and run the application in a development environment.

1. **Clone the Repository**

   Clone the repository to your local machine:
   ```bash
   git clone https://github.com/masikisiki/openvidu.git
   cd openvidu
Organize the Repository Structure

Ensure the repository is structured with openvidu-server/ and angular-app/ directories:

# OpenVidu Video Conferencing App (Development Setup)

This repository contains a video conferencing application built with OpenVidu and Angular. It includes the OpenVidu server setup (`openvidu-server/`) and the Angular frontend (`angular-app/`). This `README.md` provides instructions to set up and run the application in a development environment.

## Repository Structure

The repository should be structured as follows:

- `openvidu-server/`: Contains the OpenVidu server configuration files (`docker-compose.yml`, `.env.example`).
- `angular-app/`: Contains the Angular frontend application (`package.json`, `angular.json`, `src/`, etc.).

If the repository isn’t structured this way, organize it by creating the subdirectories with the following commands:


mkdir openvidu-server angular-app
mv docker-compose.yml .env.example .gitignore openvidu-server/
mv package.json angular.json tsconfig.json src proxy.conf.json .gitignore angular-app/

Setup Instructions
Clone the Repository

Clone the repository to your local machine:
git clone https://github.com/masikisiki/openvidu.git
cd openvidu

Set Up the OpenVidu Server

Navigate to the OpenVidu server directory:

cd openvidu-server

Create a .env file from the example and update it:

cp .env.example .env
nano .env

Update the following variables in .env:

DOMAIN_OR_PUBLIC_IP=192.168.0.203
OPENVIDU_SECRET=YOUR_OPENVIDU_SECRET
CERTIFICATE_TYPE=selfsigned
HTTPS_PORT=8443

Run the OpenVidu server using Docker Compose:

docker-compose up -d

Verify the containers are running:

docker ps

Test the server by opening https://192.168.0.203:8443/dashboard in a browser. Log in with username OPENVIDUAPP and password YOUR_OPENVIDU_SECRET. Accept the security warning for the self-signed certificate.
Set Up the Angular App

Navigate to the Angular app directory:

cd ../angular-app

Install the required Node.js dependencies:

npm install

Update the environment file by opening it with:

nano src/environments/environment.ts

Set the following:

openviduServerUrl: 'https://192.168.0.203:8443',
openviduSecret: 'YOUR_OPENVIDU_SECRET',

Configure the Development Proxy

Update the proxy configuration to forward API requests to the OpenVidu server by opening it with:

nano proxy.conf.json

Set the following:

{
  "/openvidu/api/*": {
    "target": "https://192.168.0.203:8443",
    "secure": false,
    "auth": "OPENVIDUAPP:YOUR_OPENVIDU_SECRET",
    "logLevel": "debug",
    "changeOrigin": true
  }
}

Run the Angular App

Start the Angular development server:

npm start

Open http://localhost:4200 in a browser to test the app.

If the Angular app doesn’t connect, verify openviduServerUrl and openviduSecret in environment.ts, check browser console for errors, and ensure proxy.conf.json is correctly configured.
