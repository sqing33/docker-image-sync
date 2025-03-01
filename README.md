# 将 Docker 镜像同步到 ghcr.io

### 已同步 Docker 镜像

|   | 源镜像 | 用途 | pull 命令 | docker-compose |
| ---- | -------- | ---- | --------- | -------------- |
| 1    | hello-world                      | hello-world                                       | `docker pull ghcr.nju.edu.cn/sqing33/hello-world`            | [example.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/example.yaml) |
| 2    | nginx                            | web 服务器                                        | `docker pull ghcr.nju.edu.cn/sqing33/nginx`                  | [nginx.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml) |
| 3    | dpanel/dpanel                    | docker 管理                                       | `docker pull ghcr.nju.edu.cn/sqing33/dpanel`                 | [dpanel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml) |
| 4    | lscr.io/linuxserver/qbittorrent  | bt 下载                                           | `docker pull ghcr.nju.edu.cn/sqing33/qbittorrent`            | [qbittorrent.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml) |
| 5    | mzz2017/v2raya                   | 魔法                                              | `docker pull ghcr.nju.edu.cn/sqing33/v2raya`                 | [v2raya.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml) |
| 6    | 6053537/portainer-ce             | docker 管理                                       | `docker pull ghcr.nju.edu.cn/sqing33/portainer`              | [portainer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/portainer.yaml) |
| 7    | mysql/mysql-server               | mysql 数据库                                      | `docker pull ghcr.nju.edu.cn/sqing33/mysql`                  | [mysql.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml) |
| 8    | whyour/qinglong                  | 青龙面板                                          | `docker pull ghcr.nju.edu.cn/sqing33/qinglong`               | [qinglong.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml) |
| 9    | ghcr.io/imagegenius/immich       | 相册                                              | `docker pull ghcr.nju.edu.cn/sqing33/immich`                 | [immich.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/immich.yaml) |
| 10   | quay.io/jupyter/pyspark-notebook | 基于网页的用于交互计算的编辑器                    | `docker pull ghcr.nju.edu.cn/sqing33/jupyter-notebook`       | [jupyter-notebook.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyter-notebook.yaml) |
| 11   | redis                            | redis 数据库                                      | `docker pull ghcr.nju.edu.cn/sqing33/redis`                  | [redis.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/redis.yaml) |
| 12   | tiangolo/nginx-rtmp              | 直播推流服务器                                    | `docker pull ghcr.nju.edu.cn/sqing33/nginx-rtmp`             | [nginx-rtmp.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx-rtmp.yaml) |
| 13   | bytelang/kplayer                 | 直播推流                                          | `docker pull ghcr.nju.edu.cn/sqing33/kplayer`                | [kplayer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/kplayer.yaml) |
| 14   | networkstatic/iperf3             | 带宽测试                                          | `docker pull ghcr.nju.edu.cn/sqing33/iperf3`                 | [iperf3.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/iperf3.yaml) |
| 15   | xhofe/alist                      | 多存储挂载工具                                    | `docker pull ghcr.nju.edu.cn/sqing33/alist`                  | [alist.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alist.yaml) |
| 16   | johngong/baidunetdisk            | docker 版百度网盘                                 | `docker pull ghcr.nju.edu.cn/sqing33/baidunetdisk`           | [baidunetdisk.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/baidunetdisk.yaml) |
| 17   | cnk3x/xunlei                     | docker 版迅雷                                     | `docker pull ghcr.nju.edu.cn/sqing33/xunlei`                 | [xunlei.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/xunlei.yaml) |
| 18   | henrygd/beszel                   | 多服务器监控面板                                  | `docker pull ghcr.nju.edu.cn/sqing33/beszel`                 | [beszel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/beszel.yaml) |
| 19   | lscr.io/linuxserver/duplicati    | 备份                                              | `docker pull ghcr.nju.edu.cn/sqing33/duplicati`              | [duplicati.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/duplicati.yaml) |
| 20   | homeassistant/home-assistant     | Home Assistant 家庭助理                           | `docker pull ghcr.nju.edu.cn/sqing33/homeassistant`          | [homeassistant.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/homeassistant.yaml) |
| 21   | jauderho/docker-autocompose      | 将现有的Docker容器转换为docker-compose.yaml       | `docker pull ghcr.nju.edu.cn/sqing33/autocompose`            | [autocompose.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/autocompose.yaml) |
| 22   | azukaar/cosmos-server            | NAS 系统                                          | `docker pull ghcr.nju.edu.cn/sqing33/cosmos`                 | [cosmos.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/cosmos.yaml) |
| 23   | jmal/jmalcloud                   | 私有云存储                                        | `docker pull ghcr.nju.edu.cn/sqing33/jmalcloud`              | [jmalcloud.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jmalcloud.yaml) |
| 24   | photoprism/photoprism            | ai 相册                                           | `docker pull ghcr.nju.edu.cn/sqing33/photoprism`             | [photoprism.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/photoprism.yaml) |
| 25   | mongodb/mongodb-community-server | mongodb 文档型数据库                              | `docker pull ghcr.nju.edu.cn/sqing33/mongodb`                | [mongodb.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mongodb.yaml) |
| 26   | pihole/pihole                    | 广告拦截器                                        | `docker pull ghcr.nju.edu.cn/sqing33/pihole`                 | [pihole.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/pihole.yaml) |
| 27   | linuxserver/resilio-sync         | 同步                                              | `docker pull ghcr.nju.edu.cn/sqing33/resilio-sync`           | [resilio-sync.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/resilio-sync.yaml) |
| 28   | jeessy/ddns-go                   | 自动获取公网 IPv4 或 IPv6并解析到对应的域名服务器 | `docker pull ghcr.nju.edu.cn/sqing33/ddns-go`                | [ddns-go.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ddns-go.yaml) |
| 29   | ghcr.io/noipcom/noip-duc         | noip 动态更新客户端                               | `docker pull ghcr.nju.edu.cn/sqing33/noip-duc`               | [noip-duc.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/noip-duc.yaml) |
| 30   | cym1102/nginxwebui               |                                                   | `docker pull ghcr.nju.edu.cn/sqing33/nginxwebui`             | [nginxwebui.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginxwebui.yaml) |
| 31   | node                             | Node.js 服务器                                    | `docker pull ghcr.nju.edu.cn/sqing33/node`                   | [node.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/node.yaml) |
| 32 | alpine | Alpine Linux，大小仅为 5 MB 的 Linux 发行版 | `docker pull ghcr.nju.edu.cn/sqing33/alpine` | [alpine.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/alpine.yaml) |
| 33 | moby/buildkit | Dockerfile 构建 | `docker pull ghcr.nju.edu.cn/sqing33/buildkit` | [buildkit.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/buildkit.yaml) |
| 34 | ollama/ollama | 启动和运行大型语言模型的最简单方法 | `docker pull ghcr.nju.edu.cn/sqing33/ollama` | [ollama.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/ollama.yaml) |
| 35 | python | 包含python的3.8、3.9、3.12、3.13的完整版本、slim、alpine版本,python:3.14.0a4,python:3.14-rc | `docker pull ghcr.nju.edu.cn/sqing33/python` | [python.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/python.yaml) |
| 36 | laoyutang/clash-and-dashboard | 魔法 | `docker pull ghcr.nju.edu.cn/sqing33/clash` | [clash.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml) |
| 37 | star7th/showdoc | 云文档 | `docker pull ghcr.nju.edu.cn/sqing33/showdoc:arm-latest` | [showdoc.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/showdoc.yaml) |
### 使用方法

1. 

