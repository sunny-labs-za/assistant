# Sunny ZeroClaw

A fuller-featured [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw/) image for Home Assistant OS
and unRAID.

The upstream `ghcr.io/zeroclaw-labs/zeroclaw:debian` image ships without all optional packages. This
build enables them (agent runtime, WhatsApp, RAG/PDF, browser, WASM plugins) and publishes
multi-arch (`amd64` / `arm64`) Ubuntu 24.04 images.

## Image

```text
ghcr.io/sunny-labs-za/zeroclaw:latest
```

Also tagged with the upstream ZeroClaw release version.

## Usage

Pull and run like any other container. On unRAID, use the Docker Compose Community app.

## Credits

- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw/)
- Inspired by [docker-harnesses](https://github.com/ilteoood/docker-harnesses)
