---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-09-02T16:12:44.625Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

# Docker Installation

---

> [!info] Docker
> Docker is a containerization platform that allows self-hosted applications to run in isolated environments called containers. It makes deploying, managing, updating, and backing up self-hosted applications much easier. It does not include a graphical interface and is primarily administered through terminal commands.

1. Using the terminal in VS Code, install the prerequisites using the following command

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings  
```

> [!info] Command Breakdown
>
> - `sudo apt update` Updates the list of available software.
> - `sudo apt install ca-certificates curl` Installs tools for secure downloads.
> - `sudo install -m 0755 -d /etc/apt/keyrings` Creates a folder for software security keys.

2. Add the Docker GPG key

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc  
```

> [!info] Command Breakdown
>
> - `sudo curl ...` Downloads Docker’s security key and saves it to the system.
> - `sudo chmod a+r ...` Allows all users to read the Docker security key.

3. Add Docker repository

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF  
```

4. Install Docker

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  
```

5. Verify Docker installation was successful

```bash
docker --version
sudo docker run hello-world
```

# Folder Structure

---

> [!tip] Folder Structure
> Maintaining a neat folder structure helps tremendously when it comes to problem-solving and server backups. This folder structure will be essential as you expand your server in the future.

1. Click the add folder icon in the explorer column
2. Name the folder "docker"
3. Navigate to the folder by entering the following into the terminal

```bash
cd docker
code .
```

> [!todo] Command Breakdown
>
> - `cd docker` Moves into the docker folder.
> - `code .` Opens the current folder in Visual Studio Code.

4. Create a new folder in the docker folder named "npm"
   - NGINX Proxy Manager container
5. Create a new folder in the docker folder named "actual"
   - Actual Budget container

**The directory structure should look like this:**

> /home/username/docker/\
> ├── actual/
> └── npm/

# Back Matter

---

Next Step: [[NGINX Installation]]
Previous Step: [[Visual Studio Code Installation]]
Parent Page: [[Home Server Build Guide]]
