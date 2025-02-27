# nginx.proxy

Nginx reverse proxy for personal home server. This server provides ssl termination and proxying for web requests coming into my personal server.

## Table of Contents

1. [Local Development](#local-development)
2. [Certificates](#certificates)

### Local Development

Start the nginx proxy container

```bash
docker compose up -d
```

Tear down the nginx proxy

```bash
docker compose down
```

### Certificates

Certbot and the cloudflare plugin need to be installed on the host machine

```bash
sudo dnf install certbot python3-certbot-dns-cloudflare
```

Make sure the `cloudflare.ini` is present in the current directory.

```ini
dns_cloudflare_email = your-email@example.com
dns_cloudflare_api_key = your-cloudflare-api-key
```

Set properties

```bash
sudo chmod 600 /etc/letsencrypt/cloudflare.ini
```

Manually renew certs

```bash
sudo certbot certonly \
    --dns-cloudflare \
    --dns-cloudflare-credentials cloudflare.ini \
    -d "*.betlab.app" -d "betlab.app" -d "*.collinkleest.com" -d "collinkleest.com" \
    -d "api.liteproxy.collinkleest.com" \
    --email collinkleest@gmail.com --agree-tos --non-interactive
```

Check cert

```bash
sudo certbot certificates
```

**Note:** Certificate expiration notifications are managed at redsift https://app.redsift.cloud/