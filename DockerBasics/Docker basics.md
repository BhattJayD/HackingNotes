##### Installation guide

https://docs.docker.com/engine/install/ubuntu/

#### Steps to run and stop

##### create Dockerfile

```bash
touch Dockerfile
```

```bash
nano Dockerfile
```

```
# Use an official Node.js runtime as a parent image
FROM node:18

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install Node.js dependencies
RUN npm install

# Copy the rest of your application code to the container
COPY . .

# Expose the port your app will run on (e.g., 3000)
EXPOSE 3000

# Define the command to run your Node.js application
CMD ["node", "app.js"]

```

##### Build the Docker Image

```bash
sudo docker build -t rce .
```

##### Run the Docker Container

```bash
docker run -p 3000:3000 rce
```


##### Stop the Docker Container

```bash
docker ps
```

```bash
sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                       NAMES
d8162fd1ab99   rce       "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   funny_mestorf
```

```bash
docker stop d8162fd1ab99
```


##### Remove the Docker Container

```bash
docker ps
```

```bash
sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                       NAMES
d8162fd1ab99   rce       "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   funny_mestorf
```

```bash
docker stop d8162fd1ab99
```

```bash
docker rm d8162fd1ab99
```
