# 🚀 Docker 镜像工具箱：构建与同步

本项目是一个 GitHub Actions 工作流集合，旨在提供一站式的 Docker 镜像管理方案。

它主要包含两大核心功能：

1. **从 Git 仓库构建多架构镜像**：拉取任意 Git 仓库的源代码，自动构建支持多种 CPU 架构（如 `amd64`, `arm64`）的 Docker 镜像，并将其推送到 Docker Hub 和 GitHub Packages (`ghcr.io`)。
2. **同步公共镜像以加速下载**：将 Docker Hub 等公共仓库的镜像同步到自己的 `ghcr.io` 仓库，以加速在中国大陆等地区的镜像拉取速度。如果 `ghcr.io` 速度仍不理想，可配合南京大学加速站 `ghcr.nju.edu.cn` 使用。

## ✨ 主要功能

- **双重核心**：集镜像的 **构建** 与 **同步** 功能于一身，满足不同场景的需求。
- **手动触发**：所有工作流均可在 Actions 页面通过简单的表单手动启动。
- **多架构支持**：轻松构建 `linux/amd64`, `linux/arm64`, `linux/arm/v7` 等多种 CPU 架构的镜像。
- **多仓库推送**：一次构建，自动将镜像推送到 GitHub Packages (`ghcr.io`) 和 Docker Hub。
- **自动更新**：为已同步的镜像提供每日自动更新机制，确保您使用的版本始终最新。
- **结果自动化**：工作流执行成功后，会自动更新本 `README.md` 文件中的镜像列表。
- **安全可靠**：通过 GitHub 的加密 Secrets 安全管理您的私人凭证，避免硬编码风险。

## 🛠️ 首次安装与配置

为了让所有功能正常工作，最安全、最推荐的使用方式是 **Fork 本项目**到您自己的 GitHub 账户下，然后完成以下一次性配置。

### 步骤 1: Fork 本项目

🍴 点击本项目页面右上角的 **"Fork"** 按钮，将此仓库复制一份到您自己的账户下。后续所有操作都将在您 Fork 后的仓库中进行。

### 步骤 2: 配置仓库权限

🔐 这是让 Actions 能够自动修改 `README.md` 和管理镜像的关键。

1. 在您 Fork 后的仓库页面，点击 **"Settings"** -> **"Actions"** -> **"General"**。
2. 在 `Workflow permissions` 区域，选择 **"Read and write permissions"**。
3. 勾选 **"Allow GitHub Actions to create and approve pull requests"**。
4. 点击 **"Save"** 保存设置。

### 步骤 3: 设置 Docker Hub 凭证

🔑 此步骤是**可选的**，但如果您希望使用**构建功能**并将镜像推送到 Docker Hub，则必须完成此设置。

1. 在您 Fork 后的仓库页面，点击 **"Settings"** -> **"Secrets and variables"** -> **"Actions"**。
2. 点击 **"New repository secret"** 按钮，创建以下两个 Secrets：

   - **`DOCKERHUB_USERNAME`**

     - **值**: 您的 Docker Hub 用户名。

   - **`DOCKERHUB_TOKEN`**

     - **值**: 您的 Docker Hub 访问令牌 (Access Token)。**强烈建议使用 Access Token 而非账户密码**。
     - _如何获取 Access Token？_ 登录 [Docker Hub](https://hub.docker.com/)，进入 **"Account Settings"** -> **"Security"** -> **"New Access Token"** 来生成一个。

---

## 🏗️ 功能一：从 Git 仓库构建多架构镜像

此功能会拉取一个指定的 Git 仓库，将其构建为 Docker 镜像，并推送到 `ghcr.io` 和 Docker Hub。

### 如何触发

1. 在您的仓库页面，点击顶部的 **"Actions"** 标签页。
2. 在左侧列表中，点击 **`构建 Docker 镜像 → ghcr.io, DockerHub`** 工作流。
3. 点击右侧的 **"Run workflow"** 下拉按钮，填写参数后即可开始构建。

### ⚙️ 输入参数

| 参数 (Parameter) | 描述 (Description)                                                              | 是否必需 | 默认值                                 |
| :--------------- | :------------------------------------------------------------------------------ | :------- | :------------------------------------- |
| `repo_url`       | 包含 `Dockerfile` 的 Git 仓库克隆链接。例如：`https://github.com/user/repo.git` | 是       |                                        |
| `repo_ref`       | 要克隆的仓库的分支、标签或 Commit SHA。例如：`main`, `v1.2.0`                   | 是       | `main`                                 |
| `image_name`     | 您希望为镜像设定的名称。例如：`my-web-app`                                      | 是       | `my-app`                               |
| `tags`           | 要为镜像打上的标签，多个标签用逗号 `,` 分隔。例如：`latest,v1.0`                | 是       | `latest`                               |
| `platforms`      | 要构建的 CPU 架构列表，用逗号 `,` 分隔。                                        | 是       | `linux/amd64,linux/arm64,linux/arm/v7` |

## 🔄 功能二：同步公共镜像以加速下载

此功能用于将 Docker Hub 等公共仓库的镜像同步到你的 `ghcr.io`，方便国内网络环境快速拉取。

### 如何触发

1. 在您的仓库页面，点击顶部的 **"Actions"** 标签页。
2. 在左侧列表中，点击 **`将 Docker 镜像同步到 ghcr.io`** 工作流。
3. 点击右侧的 **"Run workflow"** 下拉按钮，填写参数后即可开始同步。

### ⚙️ 输入参数

| 参数 (Parameter)       | 描述 (Description)                                                | 是否必需 | 默认值 |
| :--------------------- | :---------------------------------------------------------------- | :------- | :----- |
| `images`               | 要同步的 Docker 镜像列表，用逗号 `,` 分隔。格式为 `镜像名:标签`。 | 是       |        |
| `ghcr_names`           | （可选）为同步后的镜像指定新名称，用逗号 `,` 分隔。               | 否       |        |
| `change_tag_to_latest` | 是否将同步后的镜像标签强制改为 `latest`。                         | 是       | `是`   |

## 📊 查看结果与镜像管理

- **查看列表**: 任何成功的构建或同步任务都会自动更新下方的镜像列表。
- **管理镜像**: 若要查看或删除已同步或构建的镜像，可访问您的 GitHub 个人首页（例如 `https://github.com/user`），点击 **"Packages"** 即可查看和管理所有镜像。

## ⏰ 自动更新机制

本仓库设置了自动更新机制，每天 UTC 时间下午 4 点（北京时间午夜 12 点）会自动从源镜像仓库拉取最新版本。

**请注意：此自动更新功能仅对 `本仓库已同步的 Docker 镜像` 表格中，`同步` 列被标记为 `✔️` 的镜像有效。**

## 🗂️ 本仓库的镜像列表

### 已构建的 Docker 镜像

|     | 源仓库                                                     | 镜像名称                                                                                     |   构建时间 |
| --- | ---------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------: |
| 1   | https://github.com/sqing33/docker-docsify                  | ` ghcr.io/sqing33/docsify`<br>`sqing33/docsify `                                             | 2025-05-15 |
| 2   | https://github.com/sqing33/docker-image-sync-to-registry   | ` ghcr.io/sqing33/docker-image-sync-to-registry`<br>`sqing33/docker-image-sync-to-registry ` | 2025-06-03 |
| 3   | https://github.com/sqing33/Docker.pt-nexus.git             | ` ghcr.io/sqing33/pt-nexus`<br>`sqing33/pt-nexus `                                           | 2025-09-12 |
| 4   | https://github.com/sqing33/Docker.Code-dev-env.git         | ` ghcr.io/sqing33/code-dev-env`<br>`sqing33/code-dev-env `                                   | 2025-10-01 |

| 5   | https://github.com/sqing33/Doraemon.git | `ghcr.io/sqing33/doraemon`<br>`sqing33/doraemon` | 2026-01-03 |
| 6   | https://github.com/sqing33/SqingBlog.git | `ghcr.io/sqing33/SQBlog`<br>`sqing33/SQBlog` | 2026-01-21 |
| 7   | https://github.com/zeroclaw-labs/zeroclaw | `ghcr.io/sqing33/zeroclaw`<br>`sqing33/zeroclaw` | 2026-02-21 |
| 8   | https://github.com/libaxuan/cursor2api-go | `ghcr.io/sqing33/gogogo`<br>`sqing33/gogogo` | 2026-03-08 |
| 9   | https://github.com/7836246/cursor2api | `ghcr.io/sqing33/apap`<br>`sqing33/apap` | 2026-03-08 |
| 10  | https://github.com/sqing33/job-interview-prep | `ghcr.io/sqing33/job-interview-prep`<br>`sqing33/job-interview-prep` | 2026-03-20 |
### 已同步的 Docker 镜像

|   | 源镜像 | pull 镜像 | docker-compose | 同步 | 更新时间 |
| ---- | -------- | --------- | -------------- | ---- | -------- |
| 1   | adminer                                               | `ghcr.io/sqing33/adminer`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/adminer.yaml)                  | ✔️   | 2026-04-16 |
| 2   | justlikemaki/aiclient-2-api | `ghcr.io/sqing33/aiclient2api` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/aiclient2api.yaml) | ✔️ | 2026-04-24 |
| 3   | sqing33/argb-fan-esp32                                | `ghcr.io/sqing33/argb-fan-esp32`           | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/argb-fan-esp32.yaml)           | ✔️   | 2025-08-25 |
| 4   | jauderho/docker-autocompose                           | `ghcr.io/sqing33/autocompose`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml)              | ✔️   | 2026-04-25 |
| 5   | garethgeorge/backrest                                 | `ghcr.io/sqing33/backrest`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/backrest.yaml)                 | ✔️   | 2026-03-11 |
| 6   | henrygd/beszel                                        | `ghcr.io/sqing33/beszel`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml)                   | ✔️   | 2026-04-06 |
| 7   | amtoaer/bili-sync-rs | `ghcr.io/sqing33/bili-sync-rs` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bili-sync-rs.yaml) | ✔️ | 2026-03-26 |
| 8   | vaultwarden/server                                    | `ghcr.io/sqing33/bitwardenrs`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bitwardenrs.yaml)              | ✔️   | 2026-04-14 |
| 9   | moby/buildkit                                         | `ghcr.io/sqing33/buildkit`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml)                 | ✔️   | 2026-03-31 |
| 10  | oven/bun | `ghcr.io/sqing33/bun` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bun.yaml) | ✔️ | 2026-04-20 |
| 11  | tindy2013/subconverter                                | `ghcr.io/sqing33/clash-subconverter`       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash-subconverter.yaml)       | ✔️   | 2026-02-27 |
| 12  | metacubex/clash-meta                                  | `ghcr.io/sqing33/clash`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml)                    | ❌   |            |
| 13  | linuxserver/code-server | `ghcr.io/sqing33/code-server` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/code-server.yaml) | ✔️ | 2026-04-24 |
| 14  | ghcr.io/coracoo/dockports | `ghcr.io/sqing33/convertx` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/convertx.yaml) | ✔️ |  |
| 15  | easychen/cookiecloud                                  | `ghcr.io/sqing33/cookiecloud`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cookiecloud.yaml)              | ✔️   | 2025-08-25 |
| 16  | jeessy/ddns-go                                        | `ghcr.io/sqing33/ddns-go`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml)                  | ✔️   | 2026-04-20 |
| 17  | langgenius/dify-api                                   | `ghcr.io/sqing33/dify-api`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dify-api.yaml)                 | ✔️   | 2026-03-25 |
| 18  | langgenius/dify-plugin-daemon:latest-local            | `ghcr.io/sqing33/dify-plugin-daemon`       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dify-plugin-daemon.yaml)       | ❌   |            |
| 19  | langgenius/dify-sandbox                               | `ghcr.io/sqing33/dify-sandbox`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dify-sandbox.yaml)             | ✔️   | 2026-03-25 |
| 20  | langgenius/dify-web                                   | `ghcr.io/sqing33/dify-web`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dify-web.yaml)                 | ✔️   | 2026-03-25 |
| 21  | 0nlylty/dockercopilot | `ghcr.io/sqing33/docker-copilot` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docker-copilot.yaml) | ✔️ |  |
| 22  | ihmily/douyin-live-recorder | `ghcr.io/sqing33/douyin-live-recorder` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/douyin-live-recorder.yaml) | ✔️ |  |
| 23  | leishi1313/downloader-exporter                        | `ghcr.io/sqing33/downloader-exporter`      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/downloader-exporter.yaml)      | ✔️   |            |
| 24  | dpanel/dpanel                                         | `ghcr.io/sqing33/dpanel`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml)                   | ✔️   | 2026-04-08 |
| 25  | lscr.io/linuxserver/duplicati                         | `ghcr.io/sqing33/duplicati`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml)                | ✔️   | 2026-04-24 |
| 26  | registry.cn-shanghai.aliyuncs.com/rustc/easynvr_amd64 | `ghcr.io/sqing33/easynvr` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/easynvr.yaml) | ✔️ |  |
| 27  | lscr.io/linuxserver/emby                              | `ghcr.io/sqing33/emby`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/emby.yaml)                     | ✔️   | 2026-04-24 |
| 28  | quay.io/coreos/etcd:v3.5.18                           | `ghcr.io/sqing33/etcd`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/etcd.yaml)                     | ❌   |            |
| 29  | linuxserver/firefox                                   | `ghcr.io/sqing33/firefox`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/firefox.yaml)                  | ✔️   | 2026-04-25 |
| 30  | lscr.io/linuxserver/flexget                           | `ghcr.io/sqing33/flexget`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/flexget.yaml)                  | ✔️   | 2026-04-22 |
| 31  | forgejoclone/forgejo:13                               | `ghcr.io/sqing33/forgejo`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/forgejo.yaml)                  | ❌   |            |
| 32  | ghcr.io/snailyp/gemini-balance                        | `ghcr.io/sqing33/gemini-balance`           | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gemini-balance.yaml)           | ✔️   | 2025-09-23 |
| 33  | liwei2633/gopeed                                      | `ghcr.io/sqing33/gopeed`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gopeed.yaml)                   | ✔️   | 2026-03-18 |
| 34  | gotify/server                                         | `ghcr.io/sqing33/gotify`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gotify.yaml)                   | ✔️   | 2026-03-01 |
| 35  | ghcr.io/tbphp/gpt-load                                | `ghcr.io/sqing33/gpt-load`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gpt-load.yaml)                 | ✔️   | 2026-03-29 |
| 36  | grafana/grafana                                       | `ghcr.io/sqing33/grafana`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/grafana.yaml)                  | ✔️   | 2026-04-17 |
| 37  | registry.fit2cloud.com/halo/halo-pro:2.22 | `ghcr.io/sqing33/halo` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/halo.yaml) | ❌ |  |
| 38  | haproxy                                               | `ghcr.io/sqing33/haproxy`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/haproxy.yaml)                  | ✔️   | 2026-04-22 |
| 39  | homeassistant/home-assistant                          | `ghcr.io/sqing33/homeassistant`            | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml)            | ✔️   | 2026-04-18 |
| 40  | ghcr.io/gethomepage/homepage                          | `ghcr.io/sqing33/homepage`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homepage.yaml)                 | ✔️   | 2026-04-01 |
| 41  | corentinth/it-tools                                   | `ghcr.io/sqing33/it-tools`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/it-tools.yaml)                 | ✔️   |            |
| 42  | iyuucn/iyuuplus | `ghcr.io/sqing33/iyuu` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/iyuu.yaml) | ✔️ | 2026-04-24 |
| 43  | lscr.io/linuxserver/jackett                           | `ghcr.io/sqing33/jackett`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jackett.yaml)                  | ✔️   | 2026-04-24 |
| 44  | jellyfin/jellyfin                                     | `ghcr.io/sqing33/jellyfin`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jellyfin.yaml)                 | ✔️   | 2026-04-06 |
| 45  | jupyter/scipy-notebook                                | `ghcr.io/sqing33/jupyterlab`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyterlab.yaml)               | ✔️   | 2025-08-25 |
| 46  | bytelang/kplayer                                      | `ghcr.io/sqing33/kplayer`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml)                  | ✔️   |            |
| 47  | dko0/lsky-pro | `ghcr.io/sqing33/lsky` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lsky.yaml) | ✔️ |  |
| 48  | gdy666/lucky                                          | `ghcr.io/sqing33/lucky`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml)                    | ✔️   | 2025-11-11 |
| 49  | woodchen/lxmusicsyncserver | `ghcr.io/sqing33/lxmusic-sync-server` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lxmusic-sync-server.yaml) | ✔️ |  |
| 50  | mariadb | `ghcr.io/sqing33/mariadb` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mariadb.yaml) | ✔️ | 2026-04-16 |
| 51  | docker/mcp-gateway | `ghcr.io/sqing33/mcp-gateway` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mcp-gateway.yaml) | ✔️ | 2026-04-21 |
| 52  | ghcr.io/metacubex/metacubexd                          | `ghcr.io/sqing33/metacubexd`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/metacubexd.yaml)               | ✔️   | 2026-04-22 |
| 53  | idootop/migpt-next | `ghcr.io/sqing33/migpt` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/migpt.yaml) | ✔️ |  |
| 54  | metacubex/mihomo                                      | `ghcr.io/sqing33/mihomo`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mihomo.yaml)                   | ✔️   | 2026-04-20 |
| 55  | continuumio/miniconda3                                | `ghcr.io/sqing33/miniconda3`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/miniconda3.yaml)               | ✔️   | 2026-03-07 |
| 56  | minio/minio:RELEASE.2023-03-20T20-16-18Z              | `ghcr.io/sqing33/minio`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/minio.yaml)                    | ❌   |            |
| 57  | l429609201/misaka_danmu_server | `ghcr.io/sqing33/misaka_danmu_server` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/misaka_danmu_server.yaml) | ✔️ | 2026-04-24 |
| 58  | mongodb/mongodb-community-server                      | `ghcr.io/sqing33/mongodb`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml)                  | ✔️   | 2026-04-24 |
| 59  | jxxghp/moviepilot-v2 | `ghcr.io/sqing33/moviepilot` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/moviepilot.yaml) | ✔️ | 2026-04-22 |
| 60  | mysql:9.3.0                                           | `ghcr.io/sqing33/mysql`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml)                    | ❌   |            |
| 61  | mlikiowa/napcat-docker                                | `ghcr.io/sqing33/napcat`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/napcat.yaml)                   | ✔️   | 2026-04-16 |
| 62  | calciumion/new-api                                    | `ghcr.io/sqing33/new-api`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/new-api.yaml)                  | ✔️   | 2026-04-24 |
| 63  | tiangolo/nginx-rtmp                                   | `ghcr.io/sqing33/nginx-rtmp`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml)               | ✔️   | 2026-04-20 |
| 64  | nginx:alpine                                          | `ghcr.io/sqing33/nginx:alpine`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml)                    | ✔️   | 2026-04-24 |
| 65  | nginx                                                 | `ghcr.io/sqing33/nginx`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml)                    | ✔️   | 2026-04-24 |
| 66  | prom/node-exporter                                    | `ghcr.io/sqing33/node-exporter`            | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node-exporter.yaml)            | ✔️   | 2026-04-07 |
| 67  | node:alpine                                           | `ghcr.io/sqing33/node:alpine`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                     | ✔️   | 2026-04-24 |
| 68  | node                                                  | `ghcr.io/sqing33/node`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                     | ✔️   | 2026-04-24 |
| 69  | lampon/omnibox | `ghcr.io/sqing33/omnibox` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/omnibox.yaml) | ✔️ | 2026-04-17 |
| 70  | xiguanle/openlist                                     | `ghcr.io/sqing33/openlist`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/openlist.yaml)                 | ✔️   | 2025-11-26 |
| 71  | openspeedtest/latest                                  | `ghcr.io/sqing33/openspeedtest`            | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/openspeedtest.yaml)            | ✔️   | 2025-08-25 |
| 72  | pgvector/pgvector:0.8.0-pg17                          | `ghcr.io/sqing33/postgres`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/postgres.yaml)                 | ❌   |            |
| 73  | prom/prometheus                                       | `ghcr.io/sqing33/prometheus`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/prometheus.yaml)               | ✔️   | 2026-04-13 |
| 74  | lscr.io/linuxserver/prowlarr | `ghcr.io/sqing33/prowlarr` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/prowlarr.yaml) | ✔️ | 2026-04-22 |
| 75  | linuxserver/qbittorrent                               | `ghcr.io/sqing33/qbittorrent`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml)              | ✔️   | 2026-04-19 |
| 76  | qdtoday/qd                                            | `ghcr.io/sqing33/qd`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qd.yaml)                       | ✔️   | 2025-08-25 |
| 77  | whyour/qinglong                                       | `ghcr.io/sqing33/qinglong`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml)                 | ✔️   | 2026-03-01 |
| 78  | redis:7.2-alpine                                      | `ghcr.io/sqing33/redis:alpine`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml)                    | ✔️   | 2026-04-24 |
| 79  | redis                                                 | `ghcr.io/sqing33/redis`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml)                    | ✔️   | 2026-04-24 |
| 80  | quiq/registry-ui                                      | `ghcr.io/sqing33/registry-ui`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry-ui.yaml)              | ✔️   | 2026-02-16 |
| 81  | registry:2                                            | `ghcr.io/sqing33/registry`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry.yaml)                 | ❌   |            |
| 82  | szzhoubanxian/reseed-puppy                            | `ghcr.io/sqing33/reseed-puppy`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/reseed-puppy.yaml)             | ✔️   |            |
| 83  | steefdebruijn/docker-roonserver                       | `ghcr.io/sqing33/roonserver`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/roonserver.yaml)               | ✔️   | 2025-12-29 |
| 84  | rustfs/rustfs | `ghcr.io/sqing33/rustfs` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/rustfs.yaml) | ✔️ | 2026-04-22 |
| 85  | dperson/samba                                         | `ghcr.io/sqing33/samba`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/samba.yaml)                    | ✔️   |            |
| 86  | ccf2012/seedcross                                     | `ghcr.io/sqing33/seedcross`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/seedcross.yaml)                | ✔️   |            |
| 87  | apkdv/siyuan-unlock | `ghcr.io/sqing33/siyuan` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/siyuan.yaml) | ✔️ | 2026-04-21 |
| 88  | ghostry/smartdns                                      | `ghcr.io/sqing33/smartdns`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/smartdns.yaml)                 | ✔️   |            |
| 89  | metacubex/subconverter | `ghcr.io/sqing33/subconverter` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/subconverter.yaml) | ✔️ | 2026-02-10 |
| 90  | stilleshan/subweb | `ghcr.io/sqing33/subweb` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/subweb.yaml) | ✔️ |  |
| 91  | hslr/sun-panel                                        | `ghcr.io/sqing33/sun-panel`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/sun-panel.yaml)                | ✔️   | 2025-12-31 |
| 92  | syncthing/syncthing                                   | `ghcr.io/sqing33/syncthing`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml)                | ✔️   | 2026-04-07 |
| 93  | linuxserver/transmission:4.0.5 | `ghcr.io/sqing33/transmission` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/transmission.yaml) | ❌ |  |
| 94  | mzz2017/v2raya                                        | `ghcr.io/sqing33/v2raya`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml)                   | ✔️   | 2026-01-25 |
| 95  | ghcr.io/vert-sh/vert | `ghcr.io/sqing33/vert` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/vert.yaml) | ✔️ | 2026-04-01 |
| 96  | ghcr.io/vert-sh/vertd | `ghcr.io/sqing33/vertd` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/vertd.yaml) | ✔️ |  |
| 97  | lswl/vertex                                           | `ghcr.io/sqing33/vertex`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/vertex.yaml)                   | ✔️   | 2026-04-13 |
| 98  | containrrr/watchtower                                 | `ghcr.io/sqing33/watchtower`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/watchtower.yaml)               | ✔️   |            |
| 99  | wiznote/wizserver                                     | `ghcr.io/sqing33/wizserver`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/wizserver.yaml)                | ✔️   | 2025-10-30 |
| 100 | hanxi/xiaomusic                                       | `ghcr.io/sqing33/xiaomusic`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/xiaomusic.yaml)                | ✔️   | 2026-04-20 |
| 101 | haishanh/yacd                                         | `ghcr.io/sqing33/yacd`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yacd.yaml)                     | ✔️   | 2025-08-26 |
| 102 | siguremo/yutto                                        | `ghcr.io/sqing33/yutto-bilibili_downloads` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yutto-bilibili_downloads.yaml) | ✔️   | 2026-03-28 |
| 103 | ghcr.io/zephyruso/zashboard | `ghcr.io/sqing33/zashboard` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/zashboard.yaml) | ✔️ | 2026-04-23 |
