#Docker/DockerCompose
#Public/Notta 
## Dashy/Lissy93
```bash
---
# Welcome to Dashy! To get started, run `docker compose up -d`
# You can configure your container here, by modifying this file
version: "3.8"
services:
  dashy:
    container_name: Dashy

    # Pull latest image from DockerHub
    image: lissy93/dashy

    # To build from source, replace 'image: lissy93/dashy' with 'build: .'
    # build: .

    # Or, to use a Dockerfile for your archtecture, uncomment the following
    # context: .
    # dockerfile: ./docker/Dockerfile-arm32v7

    # You can also use an image with a different tag, or pull from a different registry, e.g:
    # image: ghcr.io/lissy93/dashy or image: lissy93/dashy:arm64v8

    # Pass in your config file below, by specifying the path on your host machine
    volumes:
      - /home/spada/docker/dashy/public/conf.yml:/app/public/conf.yml
      - /home/spada/docker/dashy/icons:/app/public/item-icons

    # Set port that web service will be served on. Keep container port as 80
    ports:
      - 8044:80

    # Set any environmental variables
    environment:
      - NODE_ENV=production
    # Specify your user ID and group ID. You can find this by running `id -u` and `id -g`
      - UID=1001
      - GID=1001

    # Specify restart policy
    restart: unless-stopped

    # Configure healthchecks
    healthcheck:
      test: ['CMD', 'node', '/app/services/healthcheck']
      interval: 1m30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

#Public/Notta 
## Caddy + Gitea
```bash
version: "3"
networks:
  gitea:
    external: false
  caddy:
services:
  gitea_server:
    image: gitea/gitea:nightly
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=100
      - GITEA__database__DB_TYPE=mysql
      - GITEA__database__HOST=database_localip
      - GITEA__database__NAME=gitea
      - GITEA__database__USER=gitea
      - GITEA__database__PASSWD=secure_password
    restart: always
    networks:
      - gitea
      - caddy
    volumes:
      - /volume1/docker/gitea/data:/data
      - /volume1/docker/gitea/timezone:/etc/timezone:ro
      - /volume1/docker/gitea/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "222:22"
  caddy:
    image: caddy:latest
    container_name: caddy
    restart: unless-stopped
    security_opt:
     - no-new-privileges:true
    ports:
     - 8024:80
     - 4432:443
    volumes:
     - /volume1/docker/caddy/Caddyfile:/etc/caddy/Caddyfile
     - /volume1/docker/caddy/site:/srv
     - /volume1/docker/caddy/caddy_data:/data
     - /volume1/docker/caddy/caddy_config:/config
    networks:
     - caddy
volumes:
  caddy_data:
   external: true
  caddy_config:
```

#Public/Notta 
## Syncthing
```bash
---
version: "3"
services:
  syncthing:
    image: lscr.io/linuxserver/syncthing:latest
    container_name: syncthing
    hostname: syncthing
    environment:
      - PUID=1000
      - PGID=1000
      - TZ="America/Los_Angeles"
    volumes:
      - /path/to/appdata/config:/config
      - /path/to/data1:/data1
      - /path/to/data2:/data2
    ports:
      - 8384:8384 # Web UI
      - 22000:22000/tcp # TCP file transfers
      - 22000:22000/udp # QUIC file transfers
      - 21027:21027/udp # Receive local discovery broadcasts
    restart: unless-stopped
```

#Public/Notta 
## Plex
```bash
version: '2'
services:
  plex:
    container_name: plex
    image: plexinc/pms-docker
    restart: unless-stopped
    environment:
      - TZ=America/Los_Angeles
      - PLEX_CLAIM=
      - PLEX_UID=1000
      - GROUP_UID=100
    network_mode: host
    volumes:
      - /volume1/docker/plex/database:/config
      - /volume1/plex/Transcode:/transcode
      - /volume1/plex:/data
    devices:
      - /dev/dri:/dev/dri
```

#Public/Notta 
## Homepage
```bash
version: "3.3"
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    environment:
      PUID: 1026
      PGID: 100
    ports:
      - 3300:3000
    volumes:
      - /volume1/docker/homepage/config:/app/config # Make sure your local config directory exists
      - /var/run/docker.sock:/var/run/docker.sock:ro # optional, for docker integrations
    restart: unless-stopped
```

## Homepage Config
```bash
# For configuration options and examples, please see:
# https://gethomepage.dev/latest/configs/services
- Network:
    - Pi-hole-Barra:
        icon: pi-hole.png
        href: http://192.168.1.20/admin
        description: Raspberry Pi4 Adblocker
        winget:
            type: pihole
            url: http://192.168.1.20/admin
            fields: ["queries", "blocked", "blocked_percent", "gravity"]
    - Pi-hole-Noches:
        icon: pi-hole.png
        href: http://192.168.1.18/admin
        description: Raspberry Pi3b+ Adblocker
    - TPLink:
        icon: tp-link.png
        href: http://192.168.1.1
        description: Local Main Router
- Media:
    - Plex:
        icon: plex.png
        href: http://192.168.1.3:32400
        description: Local Plex instance
        winget:
- Selfhosting:
    - Portainer:
        icon: portainer.png
        href: https://192.168.1.3:9443
        description: Syno01 Portainer Bussiness Instance
        widget:
            type: portainer
            url: https://192.168.1.3:9443
            env: 2
            key: ptr_R99lfgmSpt03YPxXM6scZb9m6CfX6MGnqAob+QYSOl4=
    - Syno-01:
        icon: synology-file-station.png
        href: http://192.168.1.3:5000
        description: Syno01 40TB
    - Syno-02:
        icon: synology-file-station.png
        href: http://192.168.1.5:5000
        description: Syno01 40TB
- Backup:
    - Duplicati:
        icon: duplicati.png
        href: http://192.168.1.3:8200
        description: Backup Files
    - Syncthing:
        icon: syncthing.png
        href: http://192.168.1.3:8384
        description: Backup Files    
- Servers:
    - Ben:
        icon: proxmox.png
        href: https://192.168.1.2:8006
        description: Ben Server
    - Jam:
        icon: truenas-scale.png
        href: https://192.168.1.2:8006
        description: Jam Storage/Server
```