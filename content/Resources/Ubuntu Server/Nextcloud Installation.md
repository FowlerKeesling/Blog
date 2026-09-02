---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-09-02T17:50:34.207Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!info] Nextcloud
> Nextcloud is a self-hosted application for storing, syncing, and managing files, calendars, contacts, and other information. Its functionality can be expanded through additional apps and configuration.

1. Open VSCode.
2. Create a nextcloud folder and navigate into it.

```bash
mkdir nextcloud
cd nextcloud
```

3. Create a docker compose file.

```bash
nano docker-compose.yml
```

4. Nano will open an empty file in the main window of VS Code. Paste following the configuration into the this file, **change the overwritecliurl to your domain**, then save using CTRL or ⌘ + S.

```yaml
services:
  db:
    image: mariadb:11.8
    container_name: nextcloud-db
    restart: unless-stopped
    command:
      - --transaction-isolation=READ-COMMITTED
      - --binlog-format=ROW
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: ${DB_USER}
      MYSQL_PASSWORD: ${DB_PASSWORD}
    volumes:
      - ./mariadb:/var/lib/mysql
    healthcheck:
      test: ["CMD", "healthcheck.sh", "--connect", "--innodb_initialized"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:8-alpine
    container_name: nextcloud-redis
    restart: unless-stopped
    command: redis-server --appendonly yes
    volumes:
      - ./redis:/data

  app:
    image: nextcloud:31-apache
    container_name: nextcloud
    restart: unless-stopped
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    ports:
      - "${NEXTCLOUD_PORT}:80"
    environment:
      MYSQL_HOST: db
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: ${DB_USER}
      MYSQL_PASSWORD: ${DB_PASSWORD}
      REDIS_HOST: redis
      NEXTCLOUD_TRUSTED_DOMAINS: ${TRUSTED_DOMAINS}
      OVERWRITECLIURL: ${OVERWRITECLIURL}
      OVERWRITEPROTOCOL: https
      PHP_MEMORY_LIMIT: 1G
      PHP_UPLOAD_LIMIT: 16G
      NEXTCLOUD_DEFAULT_PHONE_REGION: US
    volumes:
      - ./nextcloud:/var/www/html
```

5. Create a .env file.

```bash
nano .env
```

> [!info] Command Breakdown
> `nano .env` creates a .env file used to define environment variables such as usernames, passwords, file locations, and domain names. Docker Compose uses these variables when reading the docker-compose.yml file.

6. Nano will open an empty file in the main window of VS Code. Paste following the configuration into the this file, **fill in the username, passwords, and trusted domains**, save the login credentials to a password manager, then save using CTRL or ⌘ + S.

```env
NEXTCLOUD_PORT=8080

DB_ROOT_PASSWORD=
DB_USER=
DB_PASSWORD=

TRUSTED_DOMAINS=nextcloud.domain.org
OVERWRITECLIURL=https://nextcloud.domain.org
```

7. Start the docker containers.

```bash
sudo docker compose up -d
```

8. Log into https://npm.domain.org
9. Click "Host".
10. Click "Proxy Hosts".
11. Click "Add Proxy Host" and fill out the following:
    - **Domain Names:** nextcloud.domain.org
    - **Scheme:** http
    - **Forward Hostname / IP:** server's IPv4
    - **Forward Port:** 8080
12. Enable "Block Common Exploits".
13. Enable "Websockets Support".
14. Click on "SSL" .
15. Select "\*.domain.org" from the drop down.
16. Enable all 4 options.
17. Click "Save".
18. Record the port 8080 in the [[Server Administration]] note under Nextcloud.

> [!Check] Congratulations! The Server is Live
> **Check if everything is working**
>
> 1. Visit https://nextcloud.domain.org

# Back Matter

---

Next Step: [[Immich Installation]]
Previous Step: [[Actual Budget Installation]]
Parent Page: [[Home Server Build Guide]]
