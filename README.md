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

|   | 源镜像 | pull 镜像 | docker-compose | 同步 |
| ---- | -------- | --------- | -------------- | ---- |
| 2   | mysql                          | `ghcr.nju.edu.cn/sqing33/mysql`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml)             | ✔️ |
| 2   | phpmyadmin                     | `ghcr.nju.edu.cn/sqing33/phpmyadmin`             | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml)        | ✔️ |

### 本仓库已同步的 Docker 镜像

|   | 源镜像 | pull 镜像 | docker-compose | 同步 |
| ---- | -------- | --------- | -------------- | ---- |
| 1   | nginx                                  | `ghcr.nju.edu.cn/sqing33/nginx`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml)                      | ✔️   |
| 2   | dpanel/dpanel                          | `ghcr.nju.edu.cn/sqing33/dpanel`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml)                     | ✔️   |
| 3   | lscr.io/linuxserver/qbittorrent        | `ghcr.nju.edu.cn/sqing33/qbittorrent`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml)                | ✔️   |
| 4   | mzz2017/v2raya                         | `ghcr.nju.edu.cn/sqing33/v2raya`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml)                     | ✔️   |
| 5   | whyour/qinglong                        | `ghcr.nju.edu.cn/sqing33/qinglong`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml)                   | ✔️   |
| 6   | redis                                  | `ghcr.nju.edu.cn/sqing33/redis`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml)                      | ✔️   |
| 7   | tiangolo/nginx-rtmp                    | `ghcr.nju.edu.cn/sqing33/nginx-rtmp`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml)                 | ✔️   |
| 8   | bytelang/kplayer                       | `ghcr.nju.edu.cn/sqing33/kplayer`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml)                    | ✔️   |
| 9  | xhofe/alist                            | `ghcr.nju.edu.cn/sqing33/alist`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml)                      | ✔️   |
| 10  | henrygd/beszel                         | `ghcr.nju.edu.cn/sqing33/beszel`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml)                     | ✔️   |
| 11  | lscr.io/linuxserver/duplicati          | `ghcr.nju.edu.cn/sqing33/duplicati`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml)                  | ✔️   |
| 12  | homeassistant/home-assistant           | `ghcr.nju.edu.cn/sqing33/homeassistant`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml)              | ✔️   |
| 13  | jauderho/docker-autocompose            | `ghcr.nju.edu.cn/sqing33/autocompose`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml)                | ✔️   |
| 14  | mongodb/mongodb-community-server       | `ghcr.nju.edu.cn/sqing33/mongodb`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml)                    | ✔️   |
| 15  | jeessy/ddns-go                         | `ghcr.nju.edu.cn/sqing33/ddns-go`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml)                    | ✔️   |
| 16  | node                                   | `ghcr.nju.edu.cn/sqing33/node`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                       | ✔️   |
| 17  | alpine                                 | `ghcr.nju.edu.cn/sqing33/alpine`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml)                     | ✔️   |
| 18  | moby/buildkit                          | `ghcr.nju.edu.cn/sqing33/buildkit`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml)                   | ✔️   |
| 19  | syncthing/syncthing                    | `ghcr.nju.edu.cn/sqing33/syncthing`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml)                  | ✔️   |
| 20  | phpmyadmin                             | `ghcr.nju.edu.cn/sqing33/phpmyadmin`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml)                 | ✔️   |
| 21  | continuumio/anaconda3                  | `ghcr.nju.edu.cn/sqing33/anaconda3`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/anaconda3.yaml)                  | ✔️   |
| 22  | lscr.io/linuxserver/transmission       | `ghcr.nju.edu.cn/sqing33/transmission`               | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/transmission.yaml)               | ✔️   |
| 23  | nastool/nas-tools                      | `ghcr.nju.edu.cn/sqing33/nas-tools`                  | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nas-tools.yaml)                  | ✔️   |
| 24  | jxxghp/moviepilot-v2                   | `ghcr.nju.edu.cn/sqing33/moviepilot-v2`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/moviepilot-v2.yaml)              | ✔️   |
| 25  | metacubex/mihomo                       | `ghcr.nju.edu.cn/sqing33/mihomo`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mihomo.yaml)                     | ✔️   |
| 26  | gdy666/lucky                           | `ghcr.nju.edu.cn/sqing33/lucky`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml)                      | ✔️   |
| 27  | dperson/samba                          | `ghcr.nju.edu.cn/sqing33/samba`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/samba.yaml)                      | ✔️   |
| 28  | gdy666/lucky                           | `ghcr.nju.edu.cn/sqing33/lucky`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml)                      | ✔️   |
| 29  | gitea/gitea                            | `ghcr.nju.edu.cn/sqing33/gitea`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gitea.yaml)                      | ✔️   |
| 30  | ghcr.io/requarks/wiki                  | `ghcr.nju.edu.cn/sqing33/wiki`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/wiki.yaml)                       | ✔️   |
| 31  | phpmyadmin                             | `ghcr.nju.edu.cn/sqing33/phpmyadmin`                 | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml)                 | ✔️   |
| 32  | adminer                                | `ghcr.nju.edu.cn/sqing33/adminer`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/adminer.yaml)                    | ✔️   |
| 33  | lscr.io/linuxserver/emby               | `ghcr.nju.edu.cn/sqing33/emby`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/emby.yaml)                       | ✔️   |
| 34  | xiaoyaliu/alist                        | `ghcr.nju.edu.cn/sqing33/alist`                      | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml)                      | ✔️   |
| 35  | lscr.io/linuxserver/jackett            | `ghcr.nju.edu.cn/sqing33/jackett`                    | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jackett.yaml)                    | ✔️   |
| 36  | easychen/cookiecloud                   | `ghcr.nju.edu.cn/sqing33/cookiecloud`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cookiecloud.yaml)                | ✔️   |
| 37  | qdtoday/qd                             | `ghcr.nju.edu.cn/sqing33/qd`                         | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qd.yaml)                         | ✔️   |
| 38  | whyour/qinglong                        | `ghcr.nju.edu.cn/sqing33/qinglong`                   | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml)                   | ✔️   |
| 39  | node:alpine                            | `ghcr.nju.edu.cn/sqing33/node:alpine`                | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                       | ✔️   |
| 40  | node                                   | `ghcr.nju.edu.cn/sqing33/node`                       | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                       | ✔️   |
| 41  | gotify/server                          | `ghcr.nju.edu.cn/sqing33/gotify`                     | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/gotify.yaml)                     | ✔️   |
| 42  | sqing33/douyin-live-recorder-webui:0.1 | `ghcr.nju.edu.cn/sqing33/douyin-live-recorder-webui` | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/douyin-live-recorder-webui.yaml) | ❌   |
| 43  | sqing33/docsify                        | `ghcr.nju.edu.cn/sqing33/docsify-sqing`              | [yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/docsify-sqing.yaml)              | ✔️   |
