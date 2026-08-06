# Assistant

## ZeroClaw

A fuller-featured [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw/) image for Home Assistant OS
and unRAID.

The upstream `ghcr.io/zeroclaw-labs/zeroclaw:debian` image ships without all optional packages. This
build enables them (agent runtime, WhatsApp, browser, WASM plugins) and publishes multi-arch
(`amd64` / `arm64`) Ubuntu 24.04 images.

### Image

```text
ghcr.io/sunny-labs-za/zeroclaw:latest
```

Also tagged with the upstream ZeroClaw release version.

## Evolution Go

A multi-arch (`amd64` / `arm64`) image for
[Evolution Go](https://github.com/evolution-foundation/evolution-go), built from the latest upstream
release.

### Image

```text
ghcr.io/sunny-labs-za/evolution-go:latest
```

Also tagged with the upstream Evolution Go release version.

## Usage

Pull and run like any other container. On Unraid, use the Docker Compose Community app.

Docker Compose example mapping to **/mnt/user/appdata** on Unraid:

```yml
services:
  zeroclaw:
    image: ghcr.io/sunny-labs-za/zeroclaw:latest
    container_name: zeroclaw
    restart: unless-stopped
    ports:
      - "8080:42617"
    environment:
      ZEROCLAW_providers__models__gemini__default__api_key: ${GEMINI_API_KEY}
      ZEROCLAW_gateway__host: "[::]"
      ZEROCLAW_gateway__allow_public_bind: "true"
    volumes:
      - /mnt/user/appdata/zeroclaw-data:/zeroclaw-data
    healthcheck:
      test: ["CMD", "zeroclaw", "status", "--format=exit-code"]
      interval: 60s
      timeout: 10s
      retries: 3
      start_period: 10s

  evolution_go:
    image: ghcr.io/sunny-labs-za/evolution-go:latest
    container_name: evolution-go
    restart: unless-stopped
    ports:
      - "8081:8080"
    environment:
      SERVER_PORT: "8080"
      CLIENT_NAME: evolution
      GLOBAL_API_KEY: ${EVOLUTION_API_KEY}
      WADEBUG: INFO
      LOGTYPE: console
    volumes:
      - /mnt/user/appdata/evolution-go/dbdata:/app/dbdata
      - /mnt/user/appdata/evolution-go/logs:/app/logs
```

Manager UI: `http://<host>:8081/manager/login`

## Credits

- Inspired by [docker-harnesses](https://github.com/ilteoood/docker-harnesses)
