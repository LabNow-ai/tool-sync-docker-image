# Task Sync Docker Images

This repository provides an automated GitHub Actions workflow to sync container images from source registries to mirror registries. It is designed for teams that need repeatable, auditable image mirroring using a simple YAML configuration.

中文介绍: `README-zh_CN.md`

## What This Project Does

- Defines image mappings in `task-sync-docker-images/images.yaml`.
- Runs a GitHub Actions workflow that uses `image-syncer` inside `labnow/docker-kit`.
- Pushes images to target registries based on the mappings.

## How to Use (Fork + Customize)

1. Fork this repository to your own GitHub org or account.
2. Edit `task-sync-docker-images/images.yaml` to add or update the images and target registries you want to mirror.
3. Create a repository secret named `AUTH_FILE_CONTENT` containing your registry credentials in JSON format (see `task-sync-docker-images/README.md` for an example).
4. Trigger the workflow:
   - Manually via the Actions tab using the `sync-docker-images` workflow.
   - Or by pushing changes to `main` (the workflow ignores `*.md` changes).

## Manual Local Run

If you want to run the sync locally (or in GitHub Codespaces), follow the instructions in `task-sync-docker-images/README.md`.
