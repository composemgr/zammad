## 👋 Welcome to zammad 🚀

Web-based helpdesk and support ticket system

## 📋 Description

Web-based helpdesk and support ticket system

## 🚀 Services

- **elasticsearch**: elasticsearch:8.15.2
- **memcached**: memcached:1.6.31-alpine
- **backup**: ghcr.io/zammad/zammad:latest
- **init**: ghcr.io/zammad/zammad:latest
- **nginx**: ghcr.io/zammad/zammad:latest
- **railsserver**: ghcr.io/zammad/zammad:latest
- **scheduler**: ghcr.io/zammad/zammad:latest
- **websocket**: ghcr.io/zammad/zammad:latest

### Infrastructure Components

- **postgresql**: Postgres database
- **redis**: Redis database


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/zammad/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/zammad" ~/.local/srv/docker/zammad
cd ~/.local/srv/docker/zammad
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install zammad
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8080

## 📂 Volumes

- `./rootfs/data/db/elasticsearch` - Data storage
- `./rootfs/data/db/postgres` - Data storage
- `./rootfs/data/db/redis` - Data storage
- `./rootfs/data/zammad/backup` - Data storage
- `./rootfs/data/zammad/storage` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f elasticsearch
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
