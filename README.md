### 本项目用于将 Docker 镜像同步到 GitHub 的仓库 `ghcr.io` 以加速国内 Docker 镜像的下载，若`ghcr.io`下载速度慢可尝试使用南京大学加速站 `ghcr.nju.edu.cn` 加速下载。

### 使用方法

1. 仓库设置

   首先，将此仓库 `fork` 到个人账号。进入已 `fork` 的仓库后，点击页面顶部的 `Settings` 进入设置页面。接着，依次选择 `Action` > `General`。在 `Actions permissions` 区域，选择 `Allow all actions and reusable workflows`，这将允许所有操作和可复用的工作流运行；在 `Workflow permissions` 区域，选择 `Read and write permissions`，并勾选 `Allow GitHub Actions to create and approve pull requests`，此设置将赋予工作流读写权限，并允许其创建和批准拉取请求。完成上述设置后，点击 `save` 保存更改。

2. 触发镜像同步

   完成设置后，点击页面顶部的 `Action`，再从左侧列表中选择 `将 Docker 镜像同步到 ghcr.io`。随后，点击右侧的 `Run workflow`，在弹出的界面中填写待同步的镜像信息。


3. 同步结果查看

   镜像同步完成后，`readme.md` 文件中会自动添加该镜像的相关信息条目，内容包括源镜像、用途、`pull` 命令以及 `docker-compose` 文件路径。同时，在项目的 `docker-compose` 目录下，会自动复制 `example.yaml` 文件，并将其重命名为同步镜像的名称。

4. 镜像管理

   若要查看或删除已同步过来的镜像，可访问 Github 个人首页（https://github.com/sqing33），点击 `Packages` 即可查看已同步的所有镜像。点击具体镜像，可查看其包含的所有版本。如需对单个镜像进行管理，可点击右侧的 `Package settings` 进行相关操作。

5. 自动更新机制

   本仓库设置了自动更新机制，每天晚上 12 点会自动从源镜像获取最新版本，并更新 `ghcr.io` 上的对应镜像。在同步过程中指定版本的镜像，更新时系统会保留该指定版本。同时，在更新过程中，系统会自动检索 `readme.md` 中的镜像信息，若发现某个镜像已不存在于仓库内，会自动删除对应的条目。

### 本仓库已同步的 Docker 镜像

|   | 源镜像 | 用途 | pull 命令 | docker-compose |
| ---- | -------- | ---- | --------- | -------------- |
| 1    | hello-world                      | hello-world                                                  | `docker pull ghcr.io/sqing33/hello-world`      | [example.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/example.yaml) |
| 2    | nginx                            | web 服务器                                                   | `docker pull ghcr.io/sqing33/nginx`            | [nginx.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml) |
| 3    | dpanel/dpanel                    | docker 管理                                                  | `docker pull ghcr.io/sqing33/dpanel`           | [dpanel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml) |
| 4    | lscr.io/linuxserver/qbittorrent  | bt 下载                                                      | `docker pull ghcr.io/sqing33/qbittorrent`      | [qbittorrent.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml) |
| 5    | mzz2017/v2raya                   | 魔法                                                         | `docker pull ghcr.io/sqing33/v2raya`           | [v2raya.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml) |
| 6    | 6053537/portainer-ce             | docker 管理                                                  | `docker pull ghcr.io/sqing33/portainer`        | [portainer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/portainer.yaml) |
| 7    | mysql/mysql-server               | mysql 数据库                                                 | `docker pull ghcr.io/sqing33/mysql`            | [mysql.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml) |
| 8    | whyour/qinglong                  | 青龙面板                                                     | `docker pull ghcr.io/sqing33/qinglong`         | [qinglong.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml) |
| 9    | ghcr.io/imagegenius/immich       | 相册                                                         | `docker pull ghcr.io/sqing33/immich`           | [immich.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/immich.yaml) |
| 10   | quay.io/jupyter/pyspark-notebook | 基于网页的用于交互计算的编辑器                               | `docker pull ghcr.io/sqing33/jupyter-notebook` | [jupyter-notebook.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyter-notebook.yaml) |
| 11   | redis                            | redis 数据库                                                 | `docker pull ghcr.io/sqing33/redis`            | [redis.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml) |
| 12   | tiangolo/nginx-rtmp              | 直播推流服务器                                               | `docker pull ghcr.io/sqing33/nginx-rtmp`       | [nginx-rtmp.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml) |
| 13   | bytelang/kplayer                 | 直播推流                                                     | `docker pull ghcr.io/sqing33/kplayer`          | [kplayer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml) |
| 14   | networkstatic/iperf3             | 带宽测试                                                     | `docker pull ghcr.io/sqing33/iperf3`           | [iperf3.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/iperf3.yaml) |
| 15   | xhofe/alist                      | 多存储挂载工具                                               | `docker pull ghcr.io/sqing33/alist`            | [alist.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml) |
| 16   | johngong/baidunetdisk            | docker 版百度网盘                                            | `docker pull ghcr.io/sqing33/baidunetdisk`     | [baidunetdisk.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/baidunetdisk.yaml) |
| 17   | cnk3x/xunlei                     | docker 版迅雷                                                | `docker pull ghcr.io/sqing33/xunlei`           | [xunlei.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/xunlei.yaml) |
| 18   | henrygd/beszel                   | 多服务器监控面板                                             | `docker pull ghcr.io/sqing33/beszel`           | [beszel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml) |
| 19   | lscr.io/linuxserver/duplicati    | 备份                                                         | `docker pull ghcr.io/sqing33/duplicati`        | [duplicati.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml) |
| 20   | homeassistant/home-assistant     | Home Assistant 家庭助理                                      | `docker pull ghcr.io/sqing33/homeassistant`    | [homeassistant.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml) |
| 21   | jauderho/docker-autocompose      | 将现有的Docker容器转换为docker-compose.yaml                  | `docker pull ghcr.io/sqing33/autocompose`      | [autocompose.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml) |
| 22   | azukaar/cosmos-server            | NAS 系统                                                     | `docker pull ghcr.io/sqing33/cosmos`           | [cosmos.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cosmos.yaml) |
| 23   | photoprism/photoprism            | ai 相册                                                      | `docker pull ghcr.io/sqing33/photoprism`       | [photoprism.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/photoprism.yaml) |
| 24   | mongodb/mongodb-community-server | mongodb 文档型数据库                                         | `docker pull ghcr.io/sqing33/mongodb`          | [mongodb.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml) |
| 25   | pihole/pihole                    | 广告拦截器                                                   | `docker pull ghcr.io/sqing33/pihole`           | [pihole.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/pihole.yaml) |
| 26   | jeessy/ddns-go                   | 自动获取公网 IPv4 或 IPv6并解析到对应的域名服务器            | `docker pull ghcr.io/sqing33/ddns-go`          | [ddns-go.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml) |
| 27   | ghcr.io/noipcom/noip-duc         | noip 动态更新客户端                                          | `docker pull ghcr.io/sqing33/noip-duc`         | [noip-duc.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/noip-duc.yaml) |
| 28   | cym1102/nginxwebui               |                                                              | `docker pull ghcr.io/sqing33/nginxwebui`       | [nginxwebui.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginxwebui.yaml) |
| 29   | node                             | Node.js 服务器                                               | `docker pull ghcr.io/sqing33/node`             | [node.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml) |
| 30   | alpine                           | Alpine Linux，大小仅为 5 MB 的 Linux 发行版                  | `docker pull ghcr.io/sqing33/alpine`           | [alpine.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml) |
| 31   | moby/buildkit                    | Dockerfile 构建                                              | `docker pull ghcr.io/sqing33/buildkit`         | [buildkit.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml) |
| 32   | ollama/ollama                    | 启动和运行大型语言模型的最简单方法                           | `docker pull ghcr.io/sqing33/ollama`           | [ollama.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ollama.yaml) |
| 33   | python                           | 包含python的3.8、3.9、3.12、3.13的完整版本、slim、alpine版本,python:3.14.0a4,python:3.14-rc | `docker pull ghcr.io/sqing33/python`           | [python.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/python.yaml) |
| 34   | laoyutang/clash-and-dashboard    | 魔法                                                         | `docker pull ghcr.io/sqing33/clash`            | [clash.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml) |
| 35   | docmost/docmost                  | 云文档                                                       | `docker pull ghcr.io/sqing33/docmost`          | [docmost.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docmost.yaml) |
| 36 | outlinewiki/outline | 云文档 | `docker pull ghcr.io/sqing33/outline` | [outline.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/outline.yaml) |
| 37 | photoview/photoview | 轻量相册 | `docker pull ghcr.io/sqing33/photoview` | [photoview.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/photoview.yaml) |
| 38 | syncthing/syncthing | 同步 | `docker pull ghcr.io/sqing33/syncthing` | [syncthing.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml) |
| 39 | dreamacro/clash | 魔法 | `docker pull ghcr.io/sqing33/clash` | [clash.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml) |
| 40 | chishin/nginx-proxy-manager-zh | nginx 代理管理器 | `docker pull ghcr.io/sqing33/nginx-proxy-manager-zh` | [nginx-proxy-manager-zh.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-proxy-manager-zh.yaml) |
| 41 | phpmyadmin | 数据库管理 | `docker pull ghcr.io/sqing33/phpmyadmin` | [phpmyadmin.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml) |
| 42 | continuumio/anaconda3 | anaconda docker 环境 | `docker pull ghcr.io/sqing33/anaconda3` | [anaconda3.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/anaconda3.yaml) |
| 43 | lscr.io/linuxserver/transmission | bt 下载器 | `docker pull ghcr.io/sqing33/transmission` | [transmission.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/transmission.yaml) |
