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

|   | 源镜像 | pull 镜像 | docker-compose |
| ---- | -------- | --------- | -------------- |
| 1   | hello-world                      | `ghcr.nju.edu.cn/sqing33/hello-world`            | [example.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/example.yaml)                               |
| 2   | nginx                            | `ghcr.nju.edu.cn/sqing33/nginx`                  | [nginx.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml)                                   |
| 3   | dpanel/dpanel                    | `ghcr.nju.edu.cn/sqing33/dpanel`                 | [dpanel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml)                                 |
| 4   | lscr.io/linuxserver/qbittorrent  | `ghcr.nju.edu.cn/sqing33/qbittorrent`            | [qbittorrent.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml)                       |
| 5   | mzz2017/v2raya                   | `ghcr.nju.edu.cn/sqing33/v2raya`                 | [v2raya.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml)                                 |
| 6   | 6053537/portainer-ce             | `ghcr.nju.edu.cn/sqing33/portainer`              | [portainer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/portainer.yaml)                           |
| 7   | mysql/mysql-server               | `ghcr.nju.edu.cn/sqing33/mysql`                  | [mysql.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml)                                   |
| 8   | whyour/qinglong                  | `ghcr.nju.edu.cn/sqing33/qinglong`               | [qinglong.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml)                             |
| 9   | ghcr.io/imagegenius/immich       | `ghcr.nju.edu.cn/sqing33/immich`                 | [immich.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/immich.yaml)                                 |
| 10  | quay.io/jupyter/pyspark-notebook | `ghcr.nju.edu.cn/sqing33/jupyter-notebook`       | [jupyter-notebook.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyter-notebook.yaml)             |
| 11  | redis                            | `ghcr.nju.edu.cn/sqing33/redis`                  | [redis.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml)                                   |
| 12  | tiangolo/nginx-rtmp              | `ghcr.nju.edu.cn/sqing33/nginx-rtmp`             | [nginx-rtmp.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml)                         |
| 13  | bytelang/kplayer                 | `ghcr.nju.edu.cn/sqing33/kplayer`                | [kplayer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml)                               |
| 14  | xhofe/alist                      | `ghcr.nju.edu.cn/sqing33/alist`                  | [alist.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml)                                   |
| 15  | henrygd/beszel                   | `ghcr.nju.edu.cn/sqing33/beszel`                 | [beszel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml)                                 |
| 16  | lscr.io/linuxserver/duplicati    | `ghcr.nju.edu.cn/sqing33/duplicati`              | [duplicati.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml)                           |
| 17  | homeassistant/home-assistant     | `ghcr.nju.edu.cn/sqing33/homeassistant`          | [homeassistant.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml)                   |
| 18  | jauderho/docker-autocompose      | `ghcr.nju.edu.cn/sqing33/autocompose`            | [autocompose.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml)                       |
| 19  | mongodb/mongodb-community-server | `ghcr.nju.edu.cn/sqing33/mongodb`                | [mongodb.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml)                               |
| 20  | jeessy/ddns-go                   | `ghcr.nju.edu.cn/sqing33/ddns-go`                | [ddns-go.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml)                               |
| 21  | cym1102/nginxwebui               | `ghcr.nju.edu.cn/sqing33/nginxwebui`             | [nginxwebui.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginxwebui.yaml)                         |
| 22  | node                             | `ghcr.nju.edu.cn/sqing33/node`                   | [node.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml)                                     |
| 23  | alpine                           | `ghcr.nju.edu.cn/sqing33/alpine`                 | [alpine.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml)                                 |
| 24  | moby/buildkit                    | `ghcr.nju.edu.cn/sqing33/buildkit`               | [buildkit.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml)                             |
| 25  | python                           | `ghcr.nju.edu.cn/sqing33/python`                 | [python.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/python.yaml)                                 |
| 26  | syncthing/syncthing              | `ghcr.nju.edu.cn/sqing33/syncthing`              | [syncthing.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/syncthing.yaml)                           |
| 27  | phpmyadmin                       | `ghcr.nju.edu.cn/sqing33/phpmyadmin`             | [phpmyadmin.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/phpmyadmin.yaml)                         |
| 28  | continuumio/anaconda3            | `ghcr.nju.edu.cn/sqing33/anaconda3`              | [anaconda3.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/anaconda3.yaml)                           |
| 29  | lscr.io/linuxserver/transmission | `ghcr.nju.edu.cn/sqing33/transmission`           | [transmission.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/transmission.yaml)                     |
| 30  | nastool/nas-tools                | `ghcr.nju.edu.cn/sqing33/nas-tools`              | [nas-tools.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nas-tools.yaml)                           |
| 31  | jxxghp/moviepilot-v2             | `ghcr.nju.edu.cn/sqing33/moviepilot-v2`          | [moviepilot-v2.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/moviepilot-v2.yaml)                   |
| 32  | lscr.io/linuxserver/obsidian     | `ghcr.nju.edu.cn/sqing33/obsidian`               | [obsidian.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/obsidian.yaml)                             |
| 33  | metacubex/mihomo                 | `ghcr.nju.edu.cn/sqing33/mihomo`                 | [mihomo.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mihomo.yaml)                                 |
| 34 | gdy666/lucky | `ghcr.nju.edu.cn/sqing33/lucky` | [lucky.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/lucky.yaml) |
| 35 | dperson/samba | `ghcr.nju.edu.cn/sqing33/samba` | [samba.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/samba.yaml) |
