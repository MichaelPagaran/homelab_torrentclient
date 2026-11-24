# Torrent client (qBittorrent in Docker)

Runs [qBittorrent](https://www.qbittorrent.org/) using the `linuxserver/qbittorrent` image, with a configurable storage path.

## Setup

1. Copy the example config and set your download folder:
   ```sh
   cp .env.example .env
   # edit .env and set DOWNLOADS_PATH (and PUID/PGID: run `id -u` and `id -g`)
   ```
2. Start the container:
   ```sh
   docker compose up -d
   ```
3. Get the temporary admin password:
   ```sh
   docker logs qbittorrent
   ```
   Log in at <http://localhost:8080> as `admin` and change the password under **Tools → Options → Web UI**.
4. Under **Tools → Options → Downloads**, set the default save path to `/downloads`.

## Changing the storage path

Edit `DOWNLOADS_PATH` in `.env`, then recreate the container:

```sh
docker compose up -d
```

If `DOWNLOADS_PATH` isn't set, `docker compose` stops with an error instead of saving files somewhere unexpected.

## macOS notes

Docker Desktop can only mount folders it shares. Paths under `/Users` are shared by default. External drives (`/Volumes/...`) must be added under **Settings → Resources → File sharing**.

## Common commands

```sh
docker compose ps        # status
docker compose logs -f   # follow logs
docker compose down      # stop
docker compose pull && docker compose up -d   # update the image
```
