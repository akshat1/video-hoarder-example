# Video Hoarder Example
This repository illustrates a sample docker container set up using the VideoHoarder image.

We are going to be using the release candidate 0.1.0-rc1.

## docker-compose.yml

```yaml
version: '3'

services:
  vhoarder-a:
    image: simiacode/video-hoarder:release-0.1.0-rc1
    container_name: video-hoarder
    restart: unless-stopped
    tty: false
    network_mode: bridge
    volumes:
      # This is where the download queue, and users etc. live.
      - /data/video-hoarder:/app/db-data
      # This is where we want our downloads to go.
      - /data/downloads/videos/:/app/download
      # WebApp settings; port, URL etc.
      - ./config.json:/app/config.json
    ports:
      # Should match settings in config.json.
      - 7200:7200

```

## config.json
You need this file to describe your server set-up. The following config will cause the web app to be available at port 7200 (which matches our container description in docker-compose), and at the URL path `/video-hoarder` (so you will access it at https://<your server address>/video-hoarder).

```json
{
  "serverPath": "/video-hoarder",
  "serverPort": 7200
}
```

Checkout [r/VideoHoarderApp](https://www.reddit.com/r/VideoHoarderApp) for updates and help.
