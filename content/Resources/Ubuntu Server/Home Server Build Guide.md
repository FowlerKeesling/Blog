---
publish: true
created: 1970-01-01T00:00:00.000Z
modified: 2026-08-29T22:25:20.575Z
---

> **Themes:** [[Data Ownership]], [[Server]]
> **Status:** [[Sprouts|🌱]]
> **Tags:** #Resource

# Introduction

---

This resource is a step-by-step guide for building a home server from scratch. I recommend you use the note taking application, [Obsidian](https://obsidian.md/download), to keep track of credentials, important commands and configuration changes throughout the build. Obsidian uses Markdown, a simple formatting language that makes it easy to organize reference material and quickly copy commands when troubleshooting later.

> [!danger] Disclaimer
> This guide documents the process I used to build my own server. I am not a professional or systems administrator, and everything here is based on my own research, experimentation, and troubleshooting. While I have done my best to ensure the information is accurate, mistakes are always possible. Treat this guide as a reference rather than definitive documentation, verify commands before running them, supplement it with your own research, and make sure you understand each step before proceeding. Incorrect configuration can lead to data loss, security vulnerabilities, or service outages, so maintain reliable backups, follow good security practices, and proceed with caution.

When making this resource, I have included instructions for a select set of applications. I personally use these applications on a day to day basis, however, know that this list, and by extension, this resource, is far from exhaustive. The goal of this guide is to provide a solid foundation that will allow you to confidently install and manage additional applications on your own. If you are completely new to building a server, I recommend that you follow it from start to finish in the order I have outlined below.

**By the end of this guide, you will have:**

- An Ubuntu Server installation
- Docker running your applications
- A reverse proxy
- A registered domain
- Secure remote access with Tailscale
- Automated backups
- A dashboard for managing your services
- Several self-hosted applications

# Chapters

---

#### Part One: The Foundation

> 1. [[Home Server Hardware Requirements]]
> 2. [[Ubuntu Server Installation]]
> 3. [[Visual Studio Code Installation]]

#### Part Two: Networking

> 1. [[Docker Installation and Folder Structure]]
> 2. [[NGINX Installation]]
> 3. [[Tailscale Setup]]
> 4. [[Domain Acquisition and DNS Management]]
> 5. [[NGINX Reverse Proxy]]

#### Part Three: Self-Hosted Applications

> 1. [[Actual Budget Installation]]
> 2. [[Nextcloud Installation]]
> 3. [[Immich Installation]]
> 4. [[Homarr Installation]]

#### Part Five: Back Up Strategy

> 1. [[External Drive Backup]]
