# Docker Images Sync (Task Module)

This module syncs container images to mirror registries using `image-syncer` running inside the `labnow/docker-kit` container.

## Overview

The workflow reads the source/target mappings from `task-sync-docker-images/images.yaml` and pushes images to the configured mirror registries.

## How the GitHub Actions Workflow Works

The workflow is defined in `.github/workflows/task-sync.yml` and behaves as follows:

- Triggers on push and pull request to `main`, ignoring changes to `*.md`.
- Supports manual runs via `workflow_dispatch`.
- Reads the `AUTH_FILE_CONTENT` secret and writes it to `.github/workflows/auth.json`.
- Runs `labnow/docker-kit` and executes:
  `image-syncer --proc=8 --retries=2 --images /tmp/task-sync-docker-images/images.yaml --auth /tmp/.github/workflows/auth.json`

## Manual Run via GitHub Actions

1. Ensure the repository secret `AUTH_FILE_CONTENT` is set with the content of your auth file (JSON format).
2. Go to the Actions tab and run the `sync-docker-images` workflow using the "Run workflow" button.

## Manual Local Run (or using Github Codespace)

From the repo root, you can run the sync locally with docker-kit:

```shell
docker run -it --rm -v "$(pwd):/root/app" -w /root/app docker.io/labnow/docker-kit \
  image-syncer --proc=8 --retries=2 --images ./task-sync-docker-images/images.yaml --auth ./auth.json
```

Use either `auth.json` or `auth.yaml` and pass the corresponding path with `--auth`.

### images.yaml Example

```yaml
quay.io/labnow/docker-kit:
  - docker.io/labnow/docker-kit
  - registry.cn-hangzhou.aliyuncs.com/labnow/docker-kit
```

### auth.yaml Example

```yaml
docker.io:
  username: ""
  password: ""
  insecure: true
registry.cn-hangzhou.aliyuncs.com:
  username: ""
  password: ""
  insecure: true
```

### auth.json Example

Notice: the `AUTH_FILE_CONTENT` environment variable use this format by compact the JSON string into a single line.

```json
{
  "docker.io": {
    "username": "your-docker-io-username",
    "password": "your-docker-io-password",
    "insecure": true
  },
  "quay.io": {
    "username": "your-quay-io-username",
    "password": "your-quay-io-password",
    "insecure": true
  },
  "registry.cn-beijing.aliyuncs.com": {
    "username": "your-aliyun-acr-username",
    "password": "your-aliyun-acr-password"
  },
  "registry.cn-hangzhou.aliyuncs.com": {
    "username": "your-aliyun-acr-username",
    "password": "your-aliyun-acr-password"
  }
}
```
