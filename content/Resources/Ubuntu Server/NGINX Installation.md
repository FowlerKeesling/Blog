---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-09-02T17:45:12.000Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!info] Nginx Proxy Manager (npm)\
> This application secures remote connections and provides certifications (https). Without this, the server's applications would not work on iphone or other devices that require https certificates.

1. Create the docker compose file.

```Bash
cd npm
mkdir data
nano docker-compose.yml
```

> [!info] Code Breakdown
>
> - `cd npm` change directory to npm
> - `mkdir data` make a new directory titled data
> - `nano docker-compose.yml` create a new file titled docker-compose.yml and open it in the editor

2. Nano will open an empty file in the main window of VS Code. Paste following the configuration into the this file then save using CTRL or ⌘ + S.

```YAML
services:
  nginx_proxy_manager:
    image: "jc21/nginx-proxy-manager:latest"
    container_name: nginx_proxy_manager
    restart: unless-stopped
    network_mode: "host"
    ports:
      - "80:80"    # HTTP
      - "443:443"  # HTTPS
      - "81:81"    # Admin Panel
    volumes:
      - ./data/npm_data:/data
      - ./data/npm_letsencrypt:/etc/letsencrypt
      - ./data/npm_logs:/var/log/nginx  
    environment:
      DB_SQLITE_FILE: "/data/database.sqlite" # Using SQLite instead of MySQL for simplicity
      INITIAL_ADMIN_EMAIL: admin@example.com #Change me
      INITIAL_ADMIN_PASSWORD: changeme #Change me
```

3. Start the docker container.

```bash
sudo docker compose up -d  
```

> [!info] Command Breakdown
> `sudo docker compose up -d` starts the docker container in the background using the information outlined in the docker-compose.yml

4. Verify the container is running. If the application is running, it should appear in the list.

```bash
sudo docker ps
```

> [!info] Command Breakdown
> `docker ps` process status shows the status of all running docker containers

5. Record the port 81 in the [[Server Administration]] under NGINX proxy manager.

# Back Matter

---

Next Step: [[Tailscale Setup]]
Previous Step: [[Docker Installation and Folder Structure]]
Parent Page: [[Home Server Build Guide]]
