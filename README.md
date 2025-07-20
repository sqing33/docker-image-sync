# 🚀 Docker 镜像工具箱：构建与同步

本项目是一个 GitHub Actions 工作流集合，旨在提供一站式的 Docker 镜像管理方案。

它主要包含两大核心功能：

1.  **从 Git 仓库构建多架构镜像**：拉取任意 Git 仓库的源代码，自动构建支持多种 CPU 架构（如 `amd64`, `arm64`）的 Docker 镜像，并将其推送到 Docker Hub 和 GitHub Packages (`ghcr.io`)。
2.  **同步公共镜像以加速下载**：将 Docker Hub 等公共仓库的镜像同步到自己的 `ghcr.io` 仓库，以加速在中国大陆等地区的镜像拉取速度。如果 `ghcr.io` 速度仍不理想，可配合南京大学加速站 `ghcr.nju.edu.cn` 使用。

## ✨ 主要功能

*   **双重核心**：集镜像的 **构建** 与 **同步** 功能于一身，满足不同场景的需求。
*   **手动触发**：所有工作流均可在 Actions 页面通过简单的表单手动启动。
*   **多架构支持**：轻松构建 `linux/amd64`, `linux/arm64`, `linux/arm/v7` 等多种 CPU 架构的镜像。
*   **多仓库推送**：一次构建，自动将镜像推送到 GitHub Packages (`ghcr.io`) 和 Docker Hub。
*   **自动更新**：为已同步的镜像提供每日自动更新机制，确保您使用的版本始终最新。
*   **结果自动化**：工作流执行成功后，会自动更新本 `README.md` 文件中的镜像列表。
*   **安全可靠**：通过 GitHub 的加密 Secrets 安全管理您的私人凭证，避免硬编码风险。

## 🛠️ 首次安装与配置

为了让所有功能正常工作，最安全、最推荐的使用方式是 **Fork 本项目**到您自己的 GitHub 账户下，然后完成以下一次性配置。

### 步骤 1: Fork 本项目

:fork_and_knife: 点击本项目页面右上角的 **"Fork"** 按钮，将此仓库复制一份到您自己的账户下。后续所有操作都将在您 Fork 后的仓库中进行。

### 步骤 2: 配置仓库权限

:closed_lock_with_key: 这是让 Actions 能够自动修改 `README.md` 和管理镜像的关键。

1.  在您 Fork 后的仓库页面，点击 **"Settings"** -> **"Actions"** -> **"General"**。
2.  在 `Workflow permissions` 区域，选择 **"Read and write permissions"**。
3.  勾选 **"Allow GitHub Actions to create and approve pull requests"**。
4.  点击 **"Save"** 保存设置。

### 步骤 3: 设置 Docker Hub 凭证

:key: 此步骤是**可选的**，但如果您希望使用**构建功能**并将镜像推送到 Docker Hub，则必须完成此设置。

1.  在您 Fork 后的仓库页面，点击 **"Settings"** -> **"Secrets and variables"** -> **"Actions"**。
2.  点击 **"New repository secret"** 按钮，创建以下两个 Secrets：

    *   **`DOCKERHUB_USERNAME`**
        *   **值**: 您的 Docker Hub 用户名。

    *   **`DOCKERHUB_TOKEN`**
        *   **值**: 您的 Docker Hub 访问令牌 (Access Token)。**强烈建议使用 Access Token 而非账户密码**。
        *   *如何获取 Access Token？* 登录 [Docker Hub](https://hub.docker.com/)，进入 **"Account Settings"** -> **"Security"** -> **"New Access Token"** 来生成一个。

---

## 🏗️ 功能一：从 Git 仓库构建多架构镜像

此功能会拉取一个指定的 Git 仓库，将其构建为 Docker 镜像，并推送到 `ghcr.io` 和 Docker Hub。

### 如何触发

1.  在您的仓库页面，点击顶部的 **"Actions"** 标签页。
2.  在左侧列表中，点击 **`构建 Docker 镜像 → ghcr.io, DockerHub`** 工作流。
3.  点击右侧的 **"Run workflow"** 下拉按钮，填写参数后即可开始构建。

### ⚙️ 输入参数

| 参数 (Parameter) | 描述 (Description)                                           | 是否必需 | 默认值                                 |
| :--------------- | :----------------------------------------------------------- | :------- | :------------------------------------- |
| `repo_url`       | 包含 `Dockerfile` 的 Git 仓库克隆链接。例如：`https://github.com/user/repo.git` | 是       |                                        |
| `repo_ref`       | 要克隆的仓库的分支、标签或 Commit SHA。例如：`main`, `v1.2.0` | 是       | `main`                                 |
| `image_name`     | 您希望为镜像设定的名称。例如：`my-web-app`                   | 是       | `my-app`                               |
| `tags`           | 要为镜像打上的标签，多个标签用逗号 `,` 分隔。例如：`latest,v1.0` | 是       | `latest`                               |
| `platforms`      | 要构建的 CPU 架构列表，用逗号 `,` 分隔。                     | 是       | `linux/amd64,linux/arm64,linux/arm/v7` |

## 🔄 功能二：同步公共镜像以加速下载

此功能用于将 Docker Hub 等公共仓库的镜像同步到你的 `ghcr.io`，方便国内网络环境快速拉取。

### 如何触发

1.  在您的仓库页面，点击顶部的 **"Actions"** 标签页。
2.  在左侧列表中，点击 **`将 Docker 镜像同步到 ghcr.io`** 工作流。
3.  点击右侧的 **"Run workflow"** 下拉按钮，填写参数后即可开始同步。

### ⚙️ 输入参数

| 参数 (Parameter)       | 描述 (Description)                                           | 是否必需 | 默认值 |
| :--------------------- | :----------------------------------------------------------- | :------- | :----- |
| `images`               | 要同步的 Docker 镜像列表，用逗号 `,` 分隔。格式为 `镜像名:标签`。 | 是       |        |
| `ghcr_names`           | （可选）为同步后的镜像指定新名称，用逗号 `,` 分隔。          | 否       |        |
| `change_tag_to_latest` | 是否将同步后的镜像标签强制改为 `latest`。                    | 是       | `是`   |

## 📊 查看结果与镜像管理

*   **查看列表**: 任何成功的构建或同步任务都会自动更新下方的镜像列表。
*   **管理镜像**: 若要查看或删除已同步或构建的镜像，可访问您的 GitHub 个人首页（例如 `https://github.com/user`），点击 **"Packages"** 即可查看和管理所有镜像。

## ⏰ 自动更新机制

本仓库设置了自动更新机制，每天 UTC 时间下午 4 点（北京时间午夜 12 点）会自动从源镜像仓库拉取最新版本。

**请注意：此自动更新功能仅对 `本仓库已同步的 Docker 镜像` 表格中，`同步` 列被标记为 `✔️` 的镜像有效。**

## 🗂️ 本仓库的镜像列表

### 已构建的 Docker 镜像

|   | 源仓库 | 镜像名称 | 构建平台 | 构建时间 |
|---|---|---|---|---:|
| 1    | [sqing33/test](https://github.com/sqing33/test.git) | `ghcr.io/sqing33/my-app`<br>`sqing33/my-app` | `linux/amd64,linux/arm64,linux/arm/v7` | 2025-07-20 |
| 2   | [sqing33/test](https://github.com/sqing33/test.git) | `ghcr.io/sqing33/my-app2`<br>`sqing33/my-app2` | `linux/amd64,linux/arm64,linux/arm/v7` | 2025-07-20 15:36:14 |
### 本仓库已同步的 Docker 镜像

|      | 源镜像                                   | pull 镜像                                       | docker-compose                                               | 同步 |
| ---- | ---------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------ | ---- |
| 1    | dpanel/dpanel                            | `ghcr.io/sqing33/dpanel`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml) | ✔️    |
| 2    | metacubex/mihomo                         | `ghcr.io/sqing33/mihomo`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mihomo.yaml) | ✔️    |
| 3    | mzz2017/v2raya                           | `ghcr.io/sqing33/v2raya`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml) | ✔️    |
| 4    | dperson/samba                            | `ghcr.io/sqing33/samba`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/samba.yaml) | ✔️    |
| 5    | gdy666/lucky                             | `ghcr.io/sqing33/lucky`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml) | ✔️    |
| 6    | nginx                                    | `ghcr.io/sqing33/nginx`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml) | ✔️    |
| 7    | tiangolo/nginx-rtmp                      | `ghcr.io/sqing33/nginx-rtmp`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml) | ✔️    |
| 8    | node                                     | `ghcr.io/sqing33/node`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml) | ✔️    |
| 9    | node:alpine                              | `ghcr.io/sqing33/node:alpine`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml) | ✔️    |
| 10   | continuumio/miniconda3                   | `ghcr.io/sqing33/miniconda3`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/miniconda3.yaml) | ✔️    |
| 11   | continuumio/anaconda3                    | `ghcr.io/sqing33/anaconda3`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/anaconda3.yaml) | ✔️    |
| 12   | jupyter/scipy-notebook                   | `ghcr.io/sqing33/jupyterlab`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyterlab.yaml) | ✔️    |
| 13   | gitea/gitea                              | `ghcr.io/sqing33/gitea`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gitea.yaml) | ✔️    |
| 14   | gotify/server                            | `ghcr.io/sqing33/gotify`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gotify.yaml) | ✔️    |
| 15   | ghcr.io/requarks/wiki                    | `ghcr.io/sqing33/wiki`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/wiki.yaml) | ✔️    |
| 16   | mysql:9.3.0                              | `ghcr.io/sqing33/mysql`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml) | ❌    |
| 17   | milvusdb/milvus:v2.5.10                  | `ghcr.io/sqing33/milvus`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/milvus.yaml) | ❌    |
| 18   | quay.io/coreos/etcd:v3.5.18              | `ghcr.io/sqing33/etcd`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/etcd.yaml) | ❌    |
| 19   | minio/minio:RELEASE.2023-03-20T20-16-18Z | `ghcr.io/sqing33/minio`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/minio.yaml) | ❌    |
| 20   | redis                                    | `ghcr.io/sqing33/redis`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml) | ✔️    |
| 21   | pgvector/pgvector:0.8.0-pg17             | `ghcr.io/sqing33/postgres`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/postgres.yaml) | ❌    |
| 22   | phpmyadmin                               | `ghcr.io/sqing33/phpmyadmin`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml) | ✔️    |
| 23   | adminer                                  | `ghcr.io/sqing33/adminer`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/adminer.yaml) | ✔️    |
| 24   | shmilyin/nas-tools:2.9.0                 | `ghcr.io/sqing33/nas-tools`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nas-tools.yaml) | ❌    |
| 25   | lscr.io/linuxserver/emby                 | `ghcr.io/sqing33/emby`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/emby.yaml) | ✔️    |
| 26   | xiaoyaliu/alist                          | `ghcr.io/sqing33/xiaoya-alist`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml) | ❌    |
| 27   | xhofe/alist                              | `ghcr.io/sqing33/alist`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml) | ❌    |
| 28   | lscr.io/linuxserver/jackett              | `ghcr.io/sqing33/jackett`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jackett.yaml) | ✔️    |
| 29   | henrygd/beszel                           | `ghcr.io/sqing33/beszel`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml) | ✔️    |
| 30   | ddsderek/qbittorrent_skip_patch          | `ghcr.io/sqing33/qbittorrent`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml) | ✔️    |
| 31   | p3terx/aria2-pro                         | `ghcr.io/sqing33/aria2`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/aria2.yaml) | ✔️    |
| 32   | p3terx/ariang                            | `ghcr.io/sqing33/aria2-webui`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/aria2-webui.yaml) | ✔️    |
| 33   | lscr.io/linuxserver/duplicati            | `ghcr.io/sqing33/duplicati`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml) | ✔️    |
| 34   | easychen/cookiecloud                     | `ghcr.io/sqing33/cookiecloud`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cookiecloud.yaml) | ✔️    |
| 35   | homeassistant/home-assistant             | `ghcr.io/sqing33/homeassistant`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml) | ✔️    |
| 36   | whyour/qinglong                          | `ghcr.io/sqing33/qinglong`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml) | ✔️    |
| 37   | qdtoday/qd                               | `ghcr.io/sqing33/qd`                            | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qd.yaml) | ✔️    |
| 38   | bytelang/kplayer                         | `ghcr.io/sqing33/kplayer`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml) | ✔️    |
| 39   | jauderho/docker-autocompose              | `ghcr.io/sqing33/autocompose`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml) | ✔️    |
| 40   | mongodb/mongodb-community-server         | `ghcr.io/sqing33/mongodb`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml) | ✔️    |
| 41   | jeessy/ddns-go                           | `ghcr.io/sqing33/ddns-go`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml) | ✔️    |
| 42   | alpine                                   | `ghcr.io/sqing33/alpine`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml) | ✔️    |
| 43   | moby/buildkit                            | `ghcr.io/sqing33/buildkit`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml) | ✔️    |
| 44   | syncthing/syncthing                      | `ghcr.io/sqing33/syncthing`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml) | ✔️    |
| 45   | kuingsmile/piclist                       | `ghcr.io/sqing33/piclist`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/piclist.yaml) | ✔️    |
| 46   | dko0/lsky-pro                            | `ghcr.io/sqing33/lsky-pro`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lsky-pro.yaml) | ✔️    |
| 47   | linuxserver/code-server                  | `ghcr.io/sqing33/vscode`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/vscode.yaml) | ✔️    |
| 48   | ghcr.io/bitmagnet-io/bitmagnet           | `ghcr.io/sqing33/bitmagnet`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bitmagnet.yaml) | ✔️    |
| 49   | siguremo/yutto                           | `ghcr.io/sqing33/yutto-bilibili_downloads`      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yutto-bilibili_downloads.yaml) | ✔️    |
| 50   | chigusa/bililive-go                      | `ghcr.io/sqing33/bililive-go`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bililive-go.yaml) | ✔️    |
| 51   | ghcr.io/snailyp/gemini-balance           | `ghcr.io/sqing33/gemini-balance`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gemini-balance.yaml) | ✔️    |
| 52   | streamrec/stream-rec                     | `ghcr.io/sqing33/stream-rec`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/stream-rec.yaml) | ✔️    |
| 53   | streamrec/stream-rec-front               | `ghcr.io/sqing33/stream-rec-front`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/stream-rec-front.yaml) | ✔️    |
| 54   | ghcr.io/metacubex/metacubexd             | `ghcr.io/sqing33/metacubexd`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/metacubexd.yaml) | ✔️    |
| 55   | sqing33/docsify                          | `ghcr.io/sqing33/docsify`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docify.yaml) | ❌    |
| 56   | sqing33/douyin-live-recorder-webui       | `ghcr.io/sqing33/douyin-live-recorder-webui`    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/douyin-live-recorder-webui.yaml) | ❌    |
| 57   | sqing33/docker-image-sync-to-registry    | `ghcr.io/sqing33/docker-image-sync-to-registry` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docker-image-sync-to-registry.yaml) | ❌    |
| 58   | metacubex/clash-meta                     | `ghcr.io/sqing33/clash`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml) | ❌    |
| 59   | haproxy                                  | `ghcr.io/sqing33/haproxy`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/haproxy.yaml) | ✔️    |
| 60   | haishanh/yacd                            | `ghcr.io/sqing33/yacd`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yacd.yaml) | ✔️    |
| 61   | registry:2                               | `ghcr.io/sqing33/registry`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry.yaml) | ❌    |
| 62   | idootop/migpt-next                       | `ghcr.io/sqing33/migpt-next`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/migpt-next.yaml) | ✔️    |
| 63   | quiq/registry-ui                         | `ghcr.io/sqing33/registry-ui`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry-ui.yaml) | ✔️    |
| 64   | ghcr.io/lukegus/termix                   | `ghcr.io/sqing33/termix`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/termix.yaml) | ✔️    |
| 65   | hanxi/xiaomusic                          | `ghcr.io/sqing33/xiaomusic`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/xiaomusic.yaml) | ✔️    |
| 66   | iyuucn/iyuuplus                          | `ghcr.io/sqing33/iyuuplus`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/iyuuplus.yaml) | ✔️    |
| 67   | sqing33/argb-fan-esp32                   | `ghcr.io/sqing33/argb-fan-esp32`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/argb-fan-esp32.yaml) | ✔️    |
| 68   | jellyfin/jellyfin                        | `ghcr.io/sqing33/jellyfin`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jellyfin.yaml) | ✔️    |
| 69   | b3log/siyuan                             | `ghcr.io/sqing33/siyuan`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/siyuan.yaml) | ✔️    |
| 70   | openspeedtest/latest                     | `ghcr.io/sqing33/openspeedtest`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/openspeedtest.yaml) | ✔️    |
| 71   | grafana/grafana                          | `ghcr.io/sqing33/grafana`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/grafana.yaml) | ✔️    |
| 72   | busybox                                  | `ghcr.io/sqing33/busybox`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/busybox.yaml) | ✔️    |
