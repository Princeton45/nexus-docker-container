# My Journey Deploying Nexus as a Docker Container on DigitalOcean

This is a summary of my experience deploying Nexus Repository Manager as a Docker container on a DigitalOcean Droplet. I'll outline the key steps I took to get everything up and running.

![Diagram](https://github.com/Princeton45/nexus-docker-container/blob/main/images/diagram.jpg)

## Technologies I Used

*   **Docker:** To containerize the Nexus application, making it portable and easy to deploy.
*   **Nexus Repository Manager:** The artifact repository I wanted to deploy.
*   **DigitalOcean:** The cloud provider I used to host the server (Droplet).
*   **Linux:** The operating system running on my Droplet (specifically, Ubuntu).

## Steps I Took to Deploy Nexus

### 1. Created a DigitalOcean Droplet

First, I needed a server to work with. I created a new Droplet on DigitalOcean, which is essentially a virtual server. I chose Ubuntu as the operating system and selected a Droplet size suitable for running Nexus.

![droplet](https://github.com/Princeton45/nexus-docker-container/blob/main/images/droplet.png)

I also needed to configure the proper firewall settings on the droplet.

![firewall](https://github.com/Princeton45/nexus-docker-container/blob/main/images/firewall.png)

### 2. Set Up Docker on the Droplet

With the Droplet ready, I installed Docker on it. This allowed me to run containerized applications, including Nexus.

```bash
apt update
snap install docker
```
![version](https://github.com/Princeton45/nexus-docker-container/blob/main/images/docker-version.png)

### 3. Ran Nexus as a Docker Container

Finally, I used Docker to pull the official Nexus image from Docker Hub and started it as a container. I also made sure to map the necessary ports and volumes so that Nexus could function correctly and its data would persist.

```bash
docker volume create --name nexus-data
docker run -d -p 8081:8081 --name nexus -v nexus-data:/nexus-data sonatype/nexus3
```

The container is now running:

![running](https://github.com/Princeton45/nexus-docker-container/blob/main/images/running.png)

### 4. Accessed the Nexus UI

After starting the container, I accessed the Nexus web interface through my browser using the Droplet's IP address and the port I mapped during the container setup.

![nexus](https://github.com/Princeton45/nexus-docker-container/blob/main/images/nexus_ui.png)
