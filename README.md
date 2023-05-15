# compose.yml
```yaml
version: '3'

services:
  vaultwarden:
    container_name: vaultwarden
    restart: unless-stopped
    image: vaultwarden/server
    volumes:
      - ./:/data
    environment:
      - DOMAIN=https://pass.dev.run
      - SROCKET_WORKERS=1
      - WEBSOCKET_ENABLED=true
      - SIGNUPS_ALLOWED=false
      - SHOW_PASSWORD_HINT=false
      # - ADMIN_TOKEN=88888888
      - SMTP_HOST=smtp.gmail.com
      - SMTP_PORT=587
      - SMTP_FROM=xxxxxxxx@gmail.com
      - SMTP_USERNAME=xxxxxxxx@gmail.com
      - SMTP_PASSWORD=xxxxxxxxxxxxxxxx
      # - DATABASE_URL=postgresql://xxxxxxxx:xxxxxxxx@db.bit.io:5432/xxxxxxxx.vaultwarden
    labels:
      - traefik.enable=true
      - traefik.http.routers.vaultwarden.entrypoints=https
      - traefik.http.routers.vaultwarden.tls=true
      - traefik.http.routers.vaultwarden.rule=Host(`pass.dev.run`)
      - traefik.http.services.vaultwarden.loadbalancer.server.port=80
    networks:
      - traefik

networks:
  traefik:
    external: true
```
