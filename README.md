[Official release is here: 3.24-2026.06.1 ](https://github.com/home-assistant/docker-base/pkgs/container/base/948801341?tag=3.24-2026.06.1)

# THIS IS NOT OFFICIAL RELEASE !

---
⚠️ **IMPORTANT DISCLAIMER**

  Unofficial Build: This repository is not created or supported by the official Home Assistant team. Please do not submit issue reports or complaints to Home Assistant developers.

  32-bit Deprecation: Official support for 32-bit systems (armv7) has ended. This repository was created strictly for experimental/testing purposes following official build instructions.

  No Warranty & No Support: This repository is untested and unmaintained. Do not run this in a production environment.

  Limitation of Liability: The creator of this repository assumes no responsibility or liability for any failures, data loss, or damage to hardware. No claims or demands for damages will be entertained.

USE AT YOUR OWN RISK.
---
![Docker Image Version](https://img.shields.io/github/v/release/home-assistant/docker-base?label=Home%20Assistant%20Core&color=blue)
![Architecture](https://img.shields.io/badge/Architecture-ARMv6%20%7C%20ARMv7-orange)
![Build Status](https://img.shields.io/github/actions/workflow/status/villgzs/basic-alpine/docker-build.yml?label=Build)

### STEP No.1 - 2026.SEP.2.

# Alpine Home Assistant Base Image - for arm 32 bit platforms

Multi-stage Docker image based on Alpine Linux with:

- **jemalloc** (memory allocator)
- **s6-overlay** (process supervisor)
- **bashio** (Home Assistant bash helpers)
- **tempio** (templating tool)

## Supported platforms

- `linux/arm/v7`
- `linux/arm/v6`

## Quick start

### Local build (single architecture)

```bash
docker buildx build \
  --platform linux/arm/v7 \
  -t my-base:local \
  --load \
  .
```

### Multi-arch build + push to GHCR

A GitHub Actions workflow is already included (`.github/workflows/docker-build.yml`).

1. Push the repository to GitHub.
2. Enable GitHub Packages (or just use the default GITHUB_TOKEN permissions).
3. On every push to `main`/`master` or on tags (`v*`) the image is automatically built and pushed to:

```
ghcr.io/villgzs/basic-alpine
```

### Manual trigger

You can also run the workflow manually from the **Actions** tab and choose:

- which platforms to build
- whether to push the image or not

## Image tags

| Tag pattern              | Description                          |
|--------------------------|--------------------------------------|
| `latest`                 | Latest build from `main`/`master`    |
| `sha-<commit>`           | Specific commit                      |
| `v1.2.3` / `1.2` / `1`   | Semantic version tags                |
| branch name              | Branch builds                        |

## Usage example

```dockerfile
FROM ghcr.io/ghcr.io/villgzs/basic-alpine:latest

# your addon / application layers...
```

## Root filesystem

Place any files you want in the final image under the `rootfs/` directory.
They will be copied into the image root (`/`).

## Notes

- The Dockerfile requires **Docker BuildKit** (enabled by default in modern Docker and GitHub Actions).
- `TARGETARCH` and `TARGETVARIANT` are automatically provided by Buildx.
- Cache is shared via GitHub Actions cache for faster rebuilds.
