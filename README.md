### 本项目用于将 Docker 镜像同步到 GitHub 的仓库 `ghcr.io` 以加速国内 Docker 镜像的下载，若 `ghcr.io`下载速度慢可尝试使用南京大学加速站 `ghcr.nju.edu.cn` 加速下载。

### 使用方法

1. 仓库设置

   首先，将此仓库 `fork` 到个人账号。进入已 `fork` 的仓库后，点击页面顶部的 `Settings` 进入设置页面。接着，依次选择 `Action` > `General`。在 `Actions permissions` 区域，选择 `Allow all actions and reusable workflows`，这将允许所有操作和可复用的工作流运行；在 `Workflow permissions` 区域，选择 `Read and write permissions`，并勾选 `Allow GitHub Actions to create and approve pull requests`，此设置将赋予工作流读写权限，并允许其创建和批准拉取请求。完成上述设置后，点击 `save` 保存更改。

2. 触发镜像同步或构建

   完成设置后，你可以根据需求选择不同的 `Action`:
   - **同步现有镜像**: 从左侧列表中选择 `将 Docker 镜像同步到 ghcr.io`，此功能用于将 DockerHub 等公有仓库的镜像同步到你的 `ghcr.io`。
   - **构建新的镜像**: 从左侧列表中选择 `构建 Docker 镜像 → ghcr.io, DockerHub`，此功能会拉取一个 Git 仓库，将其构建为 Docker 镜像，并推送到 `ghcr.io` 和 `DockerHub`。

3. 结果查看

   - **同步镜像**: `readme.md` 的 `已同步的 Docker 镜像` 表格中会自动添加该镜像的信息。
   - **构建镜像**: `readme.md` 的 `已构建的 Docker 镜像` 表格中会自动添加该镜像的信息。

4. 镜像管理

   若要查看或删除已同步或构建的镜像，可访问 Github 个人首页（例如 `https://github.com/sqing33`），点击 `Packages` 即可查看所有镜像。

5. 自动更新机制

   本仓库设置了自动更新机制，每天晚上 12 点会自动从源镜像获取最新版本，并更新 `ghcr.io` 上的对应镜像。**请注意：此自动更新功能仅对 `已同步的 Docker 镜像` 表格中标记为 `✔️` 的镜像有效。**

### 本仓库已同步的 Docker 镜像

|   | 源镜像 | pull 镜像 | docker-compose | 同步 |
| ---- | -------- | --------- | -------------- | ---- |
| 1   | dpanel/dpanel                            | `ghcr.io/sqing33/dpanel`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml)                     | ✔️   |
| 2   | metacubex/mihomo                         | `ghcr.io/sqing33/mihomo`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mihomo.yaml)                     | ✔️   |
| 3   | mzz2017/v2raya                           | `ghcr.io/sqing33/v2raya`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml)                     | ✔️   |
| 4   | dperson/samba                            | `ghcr.io/sqing33/samba`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/samba.yaml)                      | ✔️   |
| 5   | gdy666/lucky                             | `ghcr.io/sqing33/lucky`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml)                      | ✔️   |
| 6   | nginx                                    | `ghcr.io/sqing33/nginx`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml)                      | ✔️   |
| 7   | tiangolo/nginx-rtmp                      | `ghcr.io/sqing33/nginx-rtmp`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml)                 | ✔️   |
| 8   | node                                     | `ghcr.io/sqing33/node`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                       | ✔️   |
| 9   | node:alpine                              | `ghcr.io/sqing33/node:alpine`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                       | ✔️   |
| 10  | continuumio/miniconda3                   | `ghcr.io/sqing33/miniconda3`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/miniconda3.yaml)                 | ✔️   |
| 11  | continuumio/anaconda3                    | `ghcr.io/sqing33/anaconda3`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/anaconda3.yaml)                  | ✔️   |
| 12  | jupyter/scipy-notebook                   | `ghcr.io/sqing33/jupyterlab`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyterlab.yaml)                 | ✔️   |
| 13  | gitea/gitea                              | `ghcr.io/sqing33/gitea`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gitea.yaml)                      | ✔️   |
| 14  | gotify/server                            | `ghcr.io/sqing33/gotify`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gotify.yaml)                     | ✔️   |
| 15  | ghcr.io/requarks/wiki                    | `ghcr.io/sqing33/wiki`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/wiki.yaml)                       | ✔️   |
| 16  | mysql:9.3.0                              | `ghcr.io/sqing33/mysql`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml)                      | ❌   |
| 17  | milvusdb/milvus:v2.5.10                  | `ghcr.io/sqing33/milvus`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/milvus.yaml)                     | ❌   |
| 18  | quay.io/coreos/etcd:v3.5.18              | `ghcr.io/sqing33/etcd`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/etcd.yaml)                       | ❌   |
| 19  | minio/minio:RELEASE.2023-03-20T20-16-18Z | `ghcr.io/sqing33/minio`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/minio.yaml)                      | ❌   |
| 20  | redis                                    | `ghcr.io/sqing33/redis`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml)                      | ✔️   |
| 21  | pgvector/pgvector:0.8.0-pg17             | `ghcr.io/sqing33/postgres`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/postgres.yaml)                   | ❌   |
| 22  | phpmyadmin                               | `ghcr.io/sqing33/phpmyadmin`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml)                 | ✔️   |
| 23  | adminer                                  | `ghcr.io/sqing33/adminer`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/adminer.yaml)                    | ✔️   |
| 24  | shmilyin/nas-tools:2.9.0                 | `ghcr.io/sqing33/nas-tools`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nas-tools.yaml)                  | ❌   |
| 25  | lscr.io/linuxserver/emby                 | `ghcr.io/sqing33/emby`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/emby.yaml)                       | ✔️   |
| 26  | xiaoyaliu/alist                          | `ghcr.io/sqing33/xiaoya-alist`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml)                      | ❌   |
| 27  | xhofe/alist                              | `ghcr.io/sqing33/alist`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml)                      | ❌   |
| 28  | lscr.io/linuxserver/jackett              | `ghcr.io/sqing33/jackett`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jackett.yaml)                    | ✔️   |
| 29  | henrygd/beszel                           | `ghcr.io/sqing33/beszel`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml)                     | ✔️   |
| 30  | ddsderek/qbittorrent_skip_patch          | `ghcr.io/sqing33/qbittorrent`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml)                | ✔️   |
| 31  | p3terx/aria2-pro                         | `ghcr.io/sqing33/aria2`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/aria2.yaml)                      | ✔️   |
| 32  | p3terx/ariang                            | `ghcr.io/sqing33/aria2-webui`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/aria2-webui.yaml)                | ✔️   |
| 33  | lscr.io/linuxserver/duplicati            | `ghcr.io/sqing33/duplicati`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml)                  | ✔️   |
| 34  | easychen/cookiecloud                     | `ghcr.io/sqing33/cookiecloud`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cookiecloud.yaml)                | ✔️   |
| 35  | homeassistant/home-assistant             | `ghcr.io/sqing33/homeassistant`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml)              | ✔️   |
| 36  | whyour/qinglong                          | `ghcr.io/sqing33/qinglong`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml)                   | ✔️   |
| 37  | qdtoday/qd                               | `ghcr.io/sqing33/qd`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qd.yaml)                         | ✔️   |
| 38  | bytelang/kplayer                         | `ghcr.io/sqing33/kplayer`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml)                    | ✔️   |
| 39  | jauderho/docker-autocompose              | `ghcr.io/sqing33/autocompose`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml)                | ✔️   |
| 40  | mongodb/mongodb-community-server         | `ghcr.io/sqing33/mongodb`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml)                    | ✔️   |
| 41  | jeessy/ddns-go                           | `ghcr.io/sqing33/ddns-go`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml)                    | ✔️   |
| 42  | alpine                                   | `ghcr.io/sqing33/alpine`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml)                     | ✔️   |
| 43  | moby/buildkit                            | `ghcr.io/sqing33/buildkit`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml)                   | ✔️   |
| 44  | syncthing/syncthing                      | `ghcr.io/sqing33/syncthing`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml)                  | ✔️   |
| 45  | kuingsmile/piclist                       | `ghcr.io/sqing33/piclist`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/piclist.yaml)                    | ✔️   |
| 46  | dko0/lsky-pro                            | `ghcr.io/sqing33/lsky-pro`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lsky-pro.yaml)                   | ✔️   |
| 47  | linuxserver/code-server                  | `ghcr.io/sqing33/vscode`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/vscode.yaml)                     | ✔️   |
| 48  | ghcr.io/bitmagnet-io/bitmagnet           | `ghcr.io/sqing33/bitmagnet`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bitmagnet.yaml)                  | ✔️   |
| 49  | siguremo/yutto                           | `ghcr.io/sqing33/yutto-bilibili_downloads`   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yutto-bilibili_downloads.yaml)   | ✔️   |
| 50  | chigusa/bililive-go                      | `ghcr.io/sqing33/bililive-go`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/bililive-go.yaml)                | ✔️   |
| 51  | ghcr.io/snailyp/gemini-balance           | `ghcr.io/sqing33/gemini-balance`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gemini-balance.yaml)             | ✔️   |
| 52  | streamrec/stream-rec                     | `ghcr.io/sqing33/stream-rec`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/stream-rec.yaml)                 | ✔️   |
| 53  | streamrec/stream-rec-front               | `ghcr.io/sqing33/stream-rec-front`           | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/stream-rec-front.yaml)           | ✔️   |
| 54  | ghcr.io/metacubex/metacubexd             | `ghcr.io/sqing33/metacubexd`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/metacubexd.yaml)                 | ✔️   |
| 55  | sqing33/docsify                          | `ghcr.io/sqing33/docsify`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docify.yaml)                     | ❌   |
| 56  | sqing33/douyin-live-recorder-webui       | `ghcr.io/sqing33/douyin-live-recorder-webui` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/douyin-live-recorder-webui.yaml) | ❌   |
| 57  | sqing33/docker-image-sync-to-registry | `ghcr.io/sqing33/docker-image-sync-to-registry`  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docker-image-sync-to-registry.yaml) | ❌ |
| 58  | metacubex/clash-meta           | `ghcr.io/sqing33/clash`                          | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml)             | ❌ |
| 59  | haproxy                        | `ghcr.io/sqing33/haproxy`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/haproxy.yaml)           | ✔️ |
| 60  | haishanh/yacd                  | `ghcr.io/sqing33/yacd`                           | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/yacd.yaml)              | ✔️ |
| 61  | registry:2                     | `ghcr.io/sqing33/registry`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry.yaml)          | ❌ |
| 62  | idootop/migpt-next             | `ghcr.io/sqing33/migpt-next`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/migpt-next.yaml)        | ✔️ |
| 63  | quiq/registry-ui               | `ghcr.io/sqing33/registry-ui`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/registry-ui.yaml)       | ✔️ |
| 64  | ghcr.io/lukegus/termix         | `ghcr.io/sqing33/termix`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/termix.yaml)            | ✔️ |
| 65  | hanxi/xiaomusic                | `ghcr.io/sqing33/xiaomusic`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/xiaomusic.yaml)         | ✔️ |
| 66  | iyuucn/iyuuplus                | `ghcr.io/sqing33/iyuuplus`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/iyuuplus.yaml)          | ✔️ |
| 67  | sqing33/argb-fan-esp32         | `ghcr.io/sqing33/argb-fan-esp32`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/argb-fan-esp32.yaml)    | ✔️ |
| 68  | jellyfin/jellyfin              | `ghcr.io/sqing33/jellyfin`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jellyfin.yaml)          | ✔️ |
| 69  | b3log/siyuan                   | `ghcr.io/sqing33/siyuan`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/siyuan.yaml)            | ✔️ |
| 70  | openspeedtest/latest           | `ghcr.io/sqing33/openspeedtest`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/openspeedtest.yaml)     | ✔️ |
| 71  | grafana/grafana                | `ghcr.io/sqing33/grafana`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/grafana.yaml)           | ✔️ |
| 72  | busybox                        | `ghcr.io/sqing33/busybox`                        | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/busybox.yaml)           | ✔️ |

### 已构建的 Docker 镜像

|   | 源仓库 | 镜像名称 | 构建平台 | 构建时间 |
|---|---|---|---|---|
