---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-08-29T23:15:19.146Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

> [!info] Visual Studio Code (VS Code)
> Install Visual Studio Code on your primary computer. It provides an easy way to connect to your server over SSH and manage files without relying entirely on the terminal.

1. Install [VS Code](https://code.visualstudio.com/download)
2. Open VS Code and click the "Remote Exlporer" icon in the left column
3. Enter the following SSH connection string to remotely connect:
   - Replace **username** with the username you created during installation
   - Replace **server-IPv4** with the server's IPv4

```
username@server-IPv4
```

4. Enter the server password when prompted
   - Once connected, VS Code will open a new window that is connected directly to your server. You can browse files, edit them, and use the integrated terminal as though you were sitting at the server itself.
5. Use CTRL or ⌘ + \` _(the key above tab)_ to show the terminal

# Back Matter

---

Next Step: [[Docker Installation and Folder Structure]]
Previous Step: [[Ubuntu Server Installation]]
Parent Page: [[Home Server Build Guide]]
