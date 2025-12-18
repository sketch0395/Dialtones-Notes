# 🌩️ Cloudflare Tunnel Setup for Xenosphere

  

This guide walks through creating a Cloudflare Tunnel, linking multiple subdomains (`app`, `srtm`, and `sonar`), and setting up a working configuration file.

  

---

  

## 🧱 Step 1. Create or Identify Your Tunnel

  

If you don’t already have a tunnel, create one:

  

```bash

cloudflared tunnel create xenosphere-tunnel

```

  

This will:

- Create a new tunnel in your Cloudflare account.

- Output a **tunnel ID** (UUID).

- Store credentials in a file like:

  ```

  /home/dialtone/.cloudflared/<TUNNEL-ID>.json

  ```

  

If you already have the tunnel, confirm it:

  

```bash

cloudflared tunnel list

```

  

Example output:

  

```

NAME                 TUNNEL-ID                                CREATED

xenosphere-tunnel    291de853-ceb0-45f7-858e-89a5e221e90d    2024-09-22T16:14:41Z

```

  

> Keep the **tunnel ID** handy — you’ll use it for DNS routes.

  

---

  

## 🌐 Step 2. Create DNS Routes for Each Hostname

  

Link each subdomain to your tunnel:

  

```bash

# Main app

cloudflared tunnel route dns xenosphere-tunnel app.dialtone.cc

  

# Secondary app

cloudflared tunnel route dns xenosphere-tunnel srtm.dialtone.cc

  

# SonarQube

cloudflared tunnel route dns xenosphere-tunnel sonar.dialtone.cc

```

  

✅ This automatically creates **CNAME records** in your Cloudflare DNS:

  

```

app   → <tunnel-id>.cfargotunnel.com

srtm  → <tunnel-id>.cfargotunnel.com

sonar → <tunnel-id>.cfargotunnel.com



```

  

Confirm under **Cloudflare Dashboard → DNS → Records**.

  

---

  

## ⚙️ Step 3. Create or Update the Cloudflared Config

  

Edit your config file:

  

```bash

sudo nano /home/dialtone/.cloudflared/config.yml

```

  

Paste the following:

  

```yaml

# Cloudflare Tunnel Configuration for Xenosphere

tunnel: xenosphere-tunnel

credentials-file: /home/dialtone/.cloudflared/291de853-ceb0-45f7-858e-89a5e221e90d.json

  

ingress:

  # API endpoints (specific paths first)

  - hostname: app.dialtone.cc

    path: /api/*

    service: http://localhost:80

  

  # Static assets

  - hostname: app.dialtone.cc

    path: /_next/*

    service: http://localhost:80

  

  # Main application

  - hostname: app.dialtone.cc

    service: http://localhost:80

    originRequest:

      httpHostHeader: app.dialtone.cc

  

  # Secondary app

  - hostname: srtm.dialtone.cc

    service: http://localhost:4000

  

  # SonarQube

  - hostname: sonar.dialtone.cc

    service: http://localhost:9000

  

  # Catch-all rule

  - service: http_status:404

```

  

Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).

  

---

  

## ✅ Step 4. Validate the Config

  

Run:

  

```bash

cloudflared tunnel ingress validate

```

  

Expected output:

  

```

Validation successful!

```

  

---

  

## 🚀 Step 5. Start or Restart the Tunnel

  

If using `systemd`:

  

```bash

sudo systemctl restart cloudflared

sudo systemctl status cloudflared

```

  

If running manually:

  

```bash

cloudflared tunnel run xenosphere-tunnel --loglevel info

```

  

---

  

## 🧪 Step 6. Test Each Hostname

  

Test locally to ensure services respond:

  

```bash

curl -I http://localhost:80

curl -I http://localhost:4000

curl -I http://localhost:9000

```

  

Then test externally:

  

```bash

curl -I https://app.dialtone.cc

curl -I https://srtm.dialtone.cc

curl -I https://sonar.dialtone.cc

```

  

✅ You should see a valid response (`200`, `302`, or app-specific).

  

---

  

## 🧠 Troubleshooting

  

Check logs for errors:

  

```bash

sudo journalctl -u cloudflared -f

```

  

or run with debug logs:

  

```bash

cloudflared tunnel run xenosphere-tunnel --loglevel debug

```

  

Common issues:

- `invalid ingress rule` → YAML formatting error.

- `could not connect to service` → backend app not running.

- `hostname not configured in DNS` → missing CNAME route.