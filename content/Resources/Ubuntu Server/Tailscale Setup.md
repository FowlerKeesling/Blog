---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-09-02T17:45:55.671Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!info] Tailscale
> Tailscale is a VPN that allows devices to connect to each other securely over the internet, as if they were on the same local network.

1. Create a free [Tailscale](https://login.tailscale.com/start) account.
2. Click "add machine".
3. Select linux server.
4. Generate an install script.
5. Copy the script and paste it into the VSCode terminal.
6. Start Tailscale.

```bash
sudo tailscale up
```

7. Copy the server IP from the Tailscale website.
8. Save the server's Tailscale IP in the [[Server Administration]] note.

# Back Matter

---

Next Step: [[Domain Acquisition and DNS Management]]
Previous Step: [[NGINX Installation]]
Parent Page: [[Home Server Build Guide]]
