---
publish: true
---
>**Themes:** [[Data Ownership]], [[Server]]
>**Status:** [[Sprouts|🌱]] 
>**Tags:** #Resource>**Themes:** 

# Docker Installation
---
>[!info] Docker
>Docker is a containerization platform that allows self-hosted applications to run in isolated environments called containers. It makes deploying, managing, updating, and backing up self-hosted applications much easier. It does not include a graphical interface and is primarily administered through terminal commands.

1. Using the terminal in VS Code, install the prerequisites using the following command

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings  
```

>[!todo]- Command Breakdown  
>**Why:** This command prepares Ubuntu for installing Docker. It updates the list of available software, installs tools needed to securely download Docker files, and creates a protected location where Docker's verification key will be stored.
>
>**sudo:** Runs the command with administrative (superuser) privileges. This is required because these commands modify system software and create directories in protected locations.
>
>**apt:** The Advanced Package Tool (APT) is Ubuntu's package manager. It is used to install, update, and remove software packages.
>
>**update:** Refreshes the local package index so your computer has the latest information about available software packages and updates.
>
>**apt install:** Downloads and installs one or more software packages from Ubuntu's repositories.
>
>**ca-certificates:** A package containing trusted Certificate Authority (CA) certificates. These certificates allow your computer to securely verify the identity of websites and software repositories that use HTTPS.
>
>**curl:** A command-line tool used to download or transfer files over the internet. It will be used later to download Docker's GPG key.
>
>**install:** A separate Linux command used to create directories or copy files while setting permissions. In this case, it is being used to create the `/etc/apt/keyrings` directory.
>
>**-m 0755:** Sets the permissions of the newly created directory. The owner has full permissions (read, write, and execute), while other users have read and execute permissions.
>
>**-d:** Tells the `install` command to create a directory instead of copying a file.
>
>**/etc/apt/keyrings:** The directory where APT stores trusted cryptographic keys used to verify software repositories, such as Docker's repository.

2. Add the Docker GPG key

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc  
```

>[!todo]- Command Breakdown  
>**Why:** This command downloads Docker's official GPG key and saves it on your server. The GPG key allows Ubuntu to verify that Docker packages come from Docker's official repository and have not been modified by a third party.
>
>**sudo:** Runs the command with administrative (superuser) privileges. This is required because the command writes files to protected system directories.
>
>**curl:** A command-line tool used to download or transfer files over the internet.
>
>**-f:** Causes `curl` to fail if the server returns an error (such as a 404 page) instead of saving an invalid file.
>
>**-s:** Runs `curl` in silent mode, hiding the progress meter and unnecessary output.
>
>**-S:** When used with `-s`, displays an error message if the download fails.
>
>**-L:** Tells `curl` to follow redirects if the requested URL points to a different location.
>
>**https://download.docker.com/linux/ubuntu/gpg:** The web address of Docker's official GPG public key. This key is used by Ubuntu to verify that Docker packages downloaded from Docker's repository are authentic and have not been altered.
>
>**-o:** Saves the downloaded file to the specified location instead of displaying it in the terminal.
>
>**/etc/apt/keyrings/docker.asc:** The location where Docker's GPG key is stored. APT uses this key to verify packages downloaded from Docker's repository.
>
>**chmod:** A command used to change the permissions of a file or directory.
>
>**a+r:** Grants **read permission** (`r`) to **all users** (`a` = owner, group, and everyone else). This allows APT to access and read the GPG key when verifying Docker packages.
>
>**/etc/apt/keyrings/docker.asc:** The same Docker GPG key file whose permissions are being updated.

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

>[!todo]- Command Breakdown  
>**Why:** This command adds Docker's official software repository to Ubuntu. By default, Ubuntu only knows about software from its own repositories. Adding Docker's repository allows Ubuntu to download the latest Docker packages directly from Docker and verify that they are authentic.
>
>**sudo:** Runs the command with administrative (superuser) privileges. This is required because the command creates a file inside `/etc/apt`, which is a protected system directory.
>
>**tee:** Reads text from the terminal and writes it to a file. It is used here because `sudo` needs to apply to the file-writing operation, not just the command that generates the text.
>
>**/etc/apt/sources.list.d/docker.sources:** The location where Docker's repository configuration file is created. Files in this directory tell Ubuntu where to find additional software repositories.
>
>**<<EOF:** Starts a "here document." Everything between this line and the ending `EOF` is treated as text input and written into the file. The ending `EOF` must appear by itself on a new line.
>
>**Types: deb:** Specifies that this repository contains Debian-based packages (`.deb` files), which are the type of packages used by Ubuntu.
>
>**URIs:** Defines the web address where Ubuntu can download Docker packages.
>
>**https://download.docker.com/linux/ubuntu:** The official Docker repository containing Docker packages for Ubuntu.
>
>**Suites:** Defines which Ubuntu release repository should be used.
>
>**\$(. /etc/os-release && echo "\${UBUNTU_CODENAME:-$VERSION_CODENAME}"):** Automatically detects the Ubuntu version codename (such as `jammy` or `noble`) so the correct Docker repository is selected.
>
>**Components: stable:** Selects Docker's stable release channel. This ensures Ubuntu downloads the officially released version of Docker rather than experimental builds.
>
>**Architectures:** Specifies which computer architecture packages should be downloaded.
>
>**$(dpkg --print-architecture):** Automatically detects the system's CPU architecture, such as `amd64` or `arm64`, so Ubuntu downloads compatible software.
>
>**Signed-By:** Specifies which cryptographic key Ubuntu should use to verify packages from this repository.
>
>**/etc/apt/keyrings/docker.asc:** The location of Docker's GPG key downloaded earlier. Ubuntu uses this key to verify that packages from Docker's repository are authentic and have not been altered.

4. Install Docker

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  
```

>[!todo]- Command Breakdown  
>**Why:** This command installs Docker Engine and its related tools on your Ubuntu server. Docker allows you to run applications inside isolated containers. The additional packages provide the Docker command-line tools, container runtime, image building capabilities, and Docker Compose support.
>
>**sudo:** Runs the command with administrative (superuser) privileges. This is required because the command updates system software and installs packages that affect the entire operating system.
>
>**apt:** The Advanced Package Tool (APT) is Ubuntu's package manager. It is used to install, update, and remove software packages.
>
>**update:** Refreshes the local package index so your computer has the latest information about available software packages and updates.
>
>**install:** Downloads and installs one or more software packages from configured software repositories.
>
>**docker-ce:** Stands for Docker Community Edition. This is the main Docker Engine package that allows your server to create and run containers.
>
>**docker-ce-cli:** Installs the Docker command-line interface (CLI). This allows you to interact with Docker using terminal commands such as `docker run`, `docker ps`, and `docker images`.
>
>**containerd.io:** Installs `containerd`, the container runtime used by Docker. It manages the basic lifecycle of containers, including starting, stopping, and storing container images.
>
>**docker-buildx-plugin:** Installs Docker Buildx, an extended build tool that improves Docker image building capabilities and supports advanced features such as multi-platform builds.
>
>**docker-compose-plugin:** Installs Docker Compose as a Docker CLI plugin. Docker Compose allows you to define and manage multiple containers using a configuration file called `compose.yaml` or `docker-compose.yml`.

5. Verify Docker installation was successful

```bash
docker --version
sudo docker run hello-world
```

>[!todo]- Command Breakdown  
>**Why:** These commands verify that Docker was installed correctly. The first command displays the installed Docker version, while the second command downloads and runs a small test container to confirm that Docker can communicate with the Docker service and successfully run containers.
>
>**docker:** The Docker command-line interface (CLI). It allows you to interact with the Docker Engine from the terminal.
>
>**--version:** Displays the installed Docker version number. This confirms that Docker is installed and accessible from the command line.
>
>**sudo:** Runs the command with administrative (superuser) privileges. This is required because the current user may not yet have permission to communicate with the Docker daemon.
>
>**run:** Creates and starts a new Docker container from a specified image.
>
>**hello-world:** A small Docker image created by Docker that is used to test whether Docker is functioning correctly. When run, it downloads the image (if it is not already available), creates a container, runs it, and displays a confirmation message.

# Folder Structure
---

>[!tip] Folder Structure
>Maintaining a neat folder structure helps tremendously when it comes to problem-solving and server backups. This folder structure will be essential as you expand your server in the future.

1. Click the add folder icon in the explorer column  
2. Name the folder "docker"  
3. Navigate to the folder by entering the following into the terminal
  
```bash
cd docker
code .
```

>[!todo]- Command Breakdown  
>**Why:** These commands open your Docker project folder in Visual Studio Code. This allows you to manage Docker files, configuration files, and project folders using a graphical editor instead of modifying everything directly from the terminal.
>
>**cd:** Stands for "change directory." This command is used to navigate between folders in the terminal.
>
>**docker:** The name of the directory you are moving into. In this setup, this folder contains your Docker-related files and projects.
>
>**code:** The command-line launcher for Visual Studio Code. It allows you to open files and folders in VS Code directly from the terminal.
>
>**.** Represents the current directory. When used with `code`, it tells Visual Studio Code to open the folder you are currently inside.

4. Create a new folder in the docker folder named "npm" 
	- NGINX Proxy Manager container
5. Create a new folder in the docker folder named "actual"  
	- Actual Budget container
  
>[!info] The structure should look like this:  
>/home/username/docker/  
>├── actual/ 
>└── npm/ 

Parent Page: [[Home Server Build Guide]]
Next Step: [[NGINX Installation]]
Previous Step: [[Visual Studio Code Installation]]