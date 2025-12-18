# Fix: Docker Remote API Access on 

  

This guide walks through fixing the issue where Docker was not accessible remotely on port **2375/2573**.

  

---

  

## 1. Stop Docker Service

```bash

sudo systemctl stop docker

```

  

---

  

## 2. Create/Update Override Config

Create the override directory if it doesn’t exist:

```bash

sudo mkdir -p /etc/systemd/system/docker.service.d

```

  

Create or edit the override config:

```bash

sudo nano /etc/systemd/system/docker.service.d/override.conf

```

  

Add this content:

```ini

[Service]

ExecStart=

ExecStart=/usr/bin/dockerd --host=fd:// --host=unix:///var/run/docker.sock --host=tcp://0.0.0.0:2375

```

  

Save and exit.

  

---

  

## 3. Reload and Restart Docker

```bash

sudo systemctl daemon-reexec

sudo systemctl daemon-reload

sudo systemctl restart docker

```

  

Check status:

```bash

systemctl status docker

```

  

---

  

## 4. Verify Locally

```bash

curl http://localhost:2375/version

```

  

---

  

## 5. Verify From Another System

Replace `<HOST-IP>` with your Raspberry Pi’s IP:

```bash

curl http://<HOST-IP>:2375/version

```

  

If it works, you should see JSON output with Docker’s version info.

  

---

  

## 6. Security Warning

- Exposing Docker without TLS is dangerous (anyone can control Docker remotely).  

- For production or untrusted networks, configure **TLS certificates** for secure remote access.