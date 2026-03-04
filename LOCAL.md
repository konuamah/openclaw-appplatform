# Running OpenClaw Locally (Mac/PC)

You can run OpenClaw on your local machine as a personal AI assistant using Docker. This setup keeps your data private and your environment isolated.

## 🛠 Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running.
- Terminal access.

## 🚀 Quick Start

1. **Prepare Environment**:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` and set:
   - `OPENCLAW_GATEWAY_TOKEN`: Your login password.
   - `STABLE_HOSTNAME`: e.g., `my-assistant`.
   - Set feature flags (`ENABLE_NGROK`, `TAILSCALE_ENABLE`, `ENABLE_SPACES`) to `false`.

2. **Launch**:
   ```bash
   docker compose up -d --build
   ```

3. **Access**:
   Open **[http://localhost:18789](http://localhost:18789)** in your browser and log in.

## 🦞 Commands 

| Task | Command |
| :--- | :--- |
| **View Logs** | `docker compose logs -f openclaw-gateway` |
| **Shell Access** | `docker exec -it my-local-assistant bash` |
| **WhatsApp Login** | `openclaw channels login --channel whatsapp` |
| **Restart** | `docker compose restart openclaw-gateway` |

## 💾 Saving Your Data

By default, data inside the container is lost if the container is removed. To persist your assistant's "brain" on your hard drive, add a volume to your `compose.yaml`:

```yaml
services:
  openclaw-gateway:
    # ...
    volumes:
      - ./openclaw_data:/data
```

## 🔒 Security Note

In local mode, the gateway is configured to bind to `0.0.0.0` (all interfaces) within the container, but it is only reachable from your Mac via the port mapping in `compose.yaml`. Access to the web interface is protected by your `OPENCLAW_GATEWAY_TOKEN`.
