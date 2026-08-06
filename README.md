# Sunny Assistant

A fuller-featured [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw/) image for Home Assistant OS
and unRAID.

The upstream `ghcr.io/zeroclaw-labs/zeroclaw:debian` image ships without all optional packages. This
build enables them (agent runtime, WhatsApp, browser, WASM plugins) and publishes multi-arch
(`amd64` / `arm64`) Ubuntu 24.04 images.

## Image

```text
ghcr.io/sunny-labs-za/zeroclaw:latest
```

Also tagged with the upstream ZeroClaw release version.

## Usage

Pull and run like any other container. On Unraid, use the Docker Compose Community app.

Docker Compose exmaple mapping to **/mnt/user/appdata** on Unraid & port **8080**

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
```

## Credits

- Inspired by [docker-harnesses](https://github.com/ilteoood/docker-harnesses)
