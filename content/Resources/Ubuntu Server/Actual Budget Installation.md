---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-08-29T23:26:32.067Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!info] Actual
> Actual is a budgeting applicaiton with functionality similar to YNAB.

1. Open VSCode.
2. Navigate to the actual folder and create a docker compose file.

```bash
cd actual
nano docker-compose.yml
```

3. Nano will open an empty file in the main window of VS Code. Paste following the configuration into the this file then save using CTRL or ⌘ + S.

```
services:  
actual_server:  
image: docker.io/actualbudget/actual-server:latest  
ports:  
- "5006:5006"  
volumes:  
- ./actual-data:/data  
restart: unless-stopped
```

4. Start the docker container.

```bash
sudo docker compose up -d
```

5. Nagivate to the NGINX admin page using a web browser https://npm.domain.org
6. Click "Hots"
7. Click "Proxy Hosts"
8. Click "Add Proxy Host" and fill out the following:
   - **Domain Names:** actual.domain.org
   - **Scheme:** http
   - **Forward Hostname / IP:** server's IPv4
   - **Forward Port:** 5006
9. Enable "Block Common Exploits"
10. Click on "SSL"
11. Select "\*.domain.org" from the drop down
12. Enable all 4 options
13. Click "Save"

> [!Check] Congratulations! The Server is Live
> **Check if everything is working**
>
> 1. Visit https://actual.domain.org

# Back Matter

---

Next Step: [[Nextcloud Installation]]
Previous Step: [[NGINX Installation]]
Parent Page: [[Home Server Build Guide]]
