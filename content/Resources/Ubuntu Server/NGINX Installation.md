---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-08-29T23:52:19.041Z
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

4. Verify the container is running. If the application is running, it should appear in the list.

```bash
sudo docker ps
```

# Back Matter

---

Next Step: [[Tailscale Setup]]
Previous Step: [[Docker Installation and Folder Structure]]
Parent Page: [[Home Server Build Guide]]
