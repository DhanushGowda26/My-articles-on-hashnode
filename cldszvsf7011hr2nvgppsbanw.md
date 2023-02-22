# Introduction to Docker

Docker:Docker is an open-source platform that enables developers to easily package, deploy, and manage applications.

Docker File:Docker file is a script that contains instructions on how to build a Docker image. It specifies the base image, the files that need to be copied into the image, the commands that need to be executed, and any environment variables that need to be set. The Docker file serves as the blueprint for building the Docker image.

Example:Create a Docker file for your Flask application

\# Use an official Python runtime as the base image FROM python:3.9-slim-buster

\# Set the working directory in the container WORKDIR /app

\# Copy the application code to the containe COPY . .

\# Install the required packages RUN pip install --no-cache-dir -r requirements.txt

\# Specify the command to run the application CMD \["python", "app.py"\]

Docker Image:Docker image is a lightweight, stand-alone, and executable software package that includes everything needed to run a piece of software, including the code, a runtime, system tools, libraries, and settings. Docker images are stored in a registry, such as Docker Hub, where they can be easily accessed and shared. Once an image is created, you can use it to create Docker containers and you can also push your daughter cker images to it.

Example:To create an Docker Image docker build -t myflaskapp

Docker Container:Docker container is a runtime instance of a Docker image. It runs in a completely isolated environment, with its own file system, networking, and environment variables. Each container has its own unique identity, and it can be started, stopped, and restarted independently of other containers. Containers can be run on any system that supports Docker, making it easy to deploy applications consistently across different environments.

Example:To create and run an container docker run -d -p 5000:5000 myflaskapp

If you run 'docker run python' on a system that does not have the Python interpreter installed, Docker will search for an image named "python" in your local image cache, and if it's not found, it will attempt to download it from a Docker registry (such as Docker Hub).So it's not necessary to create docker image, you can even get it from Docker Hub. If there is no image available with the name "python", Docker will return an error saying that the image cannot be found.

Now you got to know what docker is, so it's time to learn few commands and practice hands on.

Annalogy:Docker file is an recipe to make an particular dish and using this you make a dish nothing but docker image and your dish is inside a bowl which is nothing but container irrespective of what happens outside the bowl does not matter. The same applies for plant growth inside a pot.

Install docker for your windows from here (offical website) https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe