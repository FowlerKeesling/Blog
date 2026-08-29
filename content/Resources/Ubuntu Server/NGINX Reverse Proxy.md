---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-08-29T23:16:52.906Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!Info] Reverse Proxy
> A reverse proxy is a intermediary between the internet and webservices. It provides HTTPS certificates and encryption and routes requests through the domain.

##### Adding a Record:

1. Open Cloudflare
2. Click the "Domains" drop down and click "Overview"
3. Click on the server domain name
4. Click on the DNS drop down and click "Records"
5. Click "Add record", fill out the following:
   - **Type:** A
   - **Name:** \*._example-domain-name_.org
   - **IPv4 address:** Server Tailscale IP
6. Click "Save"

##### Generating an API Token:

1. Quick search "API Tokens"
2. Click "+ Create Token"
3. Use the "Edit zone DNS" template
4. In the "Zone Resources" category, click the "Select..." drop down
5. Select the server domain name
6. Click "Continue to summary"
7. Copy the API Token and save it in the [[Server Administration]] note.

> [!danger] API Token
> NEVER share or post this token. Save it to a locally-stored note or write it down on paper.

##### Set up a https Certificate:

1. In a web browser open the NGINX application (replace the IPv4)

```
http://serverIPv4:81
```

2. Log in using the default credentials outline in the NPM docker compose YAML

**Username:**

```
admin@example.com
```

**Password:**

```
changeme
```

3. Click on the account icon
4. Change username, email, and password
5. Save the information to the [[Server Administration]] note.
6. Click on "Certificates"
7. Click "Add Certificate"
8. Select "Let's Encrypt via DNS"
9. Fill out the following information:
   - **Domain Names:** \*.domain.org
   - **Key Type:** ECDSA 256
   - **DNS Provider:** Cloudflare
   - **Credential File Content:** After the "=" delete and paste in the API token from Cloudflare

##### Set up a Proxy for NGINX Proxy Manager:

1. Click "Hots"
2. Click "Proxy Hosts"
3. Click "Add Proxy Host" and fill out the following:
   - **Domain Names:** npm.domain.org
   - **Scheme:** http
   - **Forward Hostname / IP:** server's IPv4
   - **Forward Port:** 81
4. Enable "Block Common Exploits"
5. Click on "SSL"
6. Select "\*.domain.org" from the drop down
7. Enable all 4 options
8. Click "Save"

> [!Check] Congratulations! The Server is Live
> **Check if everything is working**
>
> 1. On a mobile device using cell service, visit https://npm.domain.org
> 2. Nothing should load
> 3. Install the Tailscale application on the mobile device
> 4. Sign into Tailscale and connect
> 5. Visit https://npm.domain.org
> 6. Success!!!

# Back Matter

---

Next Step: [[Actual Budget Installation]]
Previous Step: [[Domain Acquisition and DNS Management]]
Parent Page: [[Home Server Build Guide]]
