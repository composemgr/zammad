## 👋 Welcome to zammad 🚀

Web-based helpdesk and support ticket system

## 📋 Description

Zammad is a helpdesk system for email, web, and social media tickets. Its
official container image runs each process as its own service, so this stack
ships the nginx front end, the Rails server, the scheduler, the websocket
server, and the backup job, backed by PostgreSQL, Elasticsearch, Redis, and
Memcached.

## 🚀 Services

- **app**: ghcr.io/zammad/zammad:latest (zammad-nginx, published)
- **zammad-railsserver**: ghcr.io/zammad/zammad:latest
- **zammad-scheduler**: ghcr.io/zammad/zammad:latest
- **zammad-websocket**: ghcr.io/zammad/zammad:latest
- **zammad-backup**: ghcr.io/zammad/zammad:latest
- **zammad-init**: ghcr.io/zammad/zammad:latest

### Infrastructure Components

- **zammad-postgresql**: Postgres database
- **zammad-elasticsearch**: Elasticsearch index
- **zammad-redis**: Redis
- **zammad-memcached**: Memcached

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/zammad/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/zammad" ~/.local/srv/docker/zammad
cd ~/.local/srv/docker/zammad
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install zammad
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
DB_USER_NAME=zammad
DB_USER_PASS=replace-with-a-random-password
DB_CREATE_DATABASE_NAME=zammad_production
ZAMMAD_HTTP_TYPE=http
ZAMMAD_AUTOWIZARD_JSON=
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64396` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

Only the `zammad-nginx` service carries the proxy labels and joins the
external network. The Rails, scheduler, and websocket services stay on the
internal project network, and Traefik reaches the websocket upgrade through
the nginx front end.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64396

## 📂 Volumes

- `./volumes/data/zammad/storage` - Zammad file storage, attachments and logos
- `./volumes/data/zammad/backup` - Scheduled backup output
- `./volumes/db/postgres` - Database data
- `./volumes/db/elasticsearch` - Search index
- `./volumes/db/redis` - Redis data

## 🔐 Security

- Change all default passwords before deploying to production
- Elasticsearch runs with `xpack.security.enabled=false` and is only
  reachable on the internal project network, do not publish it
- Use HTTPS via the reverse proxy in production and set `ZAMMAD_HTTP_TYPE`
  to match
- Regular users are created by the admin panel or the auto wizard
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- At least 4 GB of memory, Elasticsearch is the largest consumer

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
