# Task Sync Docker Images（中文版）

本仓库提供一个自动化的 GitHub Actions 工作流，用于将源镜像仓库的镜像同步到镜像仓库（mirror）。适合需要稳定、可审计、可重复的镜像同步流程的团队使用。

## 项目用途

- 使用 `task-sync-docker-images/images.yaml` 定义需要同步的镜像及目标仓库。
- 通过 GitHub Actions 工作流，使用 `labnow/docker-kit` 容器中的 `image-syncer` 执行同步。
- 按配置将镜像推送到目标仓库。

## 使用方式（Fork + 自定义）

1. 将本仓库 Fork 到你自己的 GitHub 账号或组织。
2. 修改 `task-sync-docker-images/images.yaml`，添加或更新需要同步的镜像和目标仓库。
3. 在仓库 Secrets 中创建 `AUTH_FILE_CONTENT`，内容为 JSON 格式的认证信息（示例见 `task-sync-docker-images/README.md`）。
4. 触发工作流：
   - 在 Actions 中手动运行 `sync-docker-images`；
   - 或者向 `main` 分支提交代码（工作流会忽略 `*.md` 变更）。

## 本地手动运行

如需在本地或 GitHub Codespaces 中运行，请参考 `task-sync-docker-images/README.md` 中的本地运行说明。
