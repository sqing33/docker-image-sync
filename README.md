# 将 Docker 镜像同步到 ghcr.io

### 已同步 Docker 镜像

|   | 源镜像 | 用途 | pull 命令 | docker-compose |
| ---- | -------- | ---- | --------- | -------------- |
| 1 | hello-world                   | hello-world | `docker pull ghcr.nju.edu.cn/sqing33/hello-world`       | [example.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/example.yaml) |
| 2 | nginx                         | web 服务器  | `docker pull ghcr.nju.edu.cn/sqing33/nginx`             | [nginx.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/nginx.yaml) |
| 3 | dpanel/dpanel                 | docker 管理 | `docker pull ghcr.nju.edu.cn/sqing33/dpanel`            | [dpanel.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/dpanel.yaml) |
| 4 | lscr.io/linuxserver/qbittorrent | bt 下载 | `docker pull ghcr.nju.edu.cn/sqing33/qbittorrent` | [qbittorrent.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qbittorrent.yaml) |
| 5 | mzz2017/v2raya | 魔法 | `docker pull ghcr.nju.edu.cn/sqing33/v2raya` | [v2raya.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml) |
| 6 | 6053537/portainer-ce | docker 管理 | `docker pull ghcr.nju.edu.cn/sqing33/portainer` | [portainer.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/portainer.yaml) |
| 7 | mysql/mysql-server | mysql 数据库 | `docker pull ghcr.nju.edu.cn/sqing33/mysql` | [mysql.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/mysql.yaml) |
| 8 | whyour/qinglong | 青龙面板 | `docker pull ghcr.nju.edu.cn/sqing33/qinglong` | [qinglong.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/qinglong.yaml) |
| 9 | ghcr.io/imagegenius/immich | 相册 | `docker pull ghcr.nju.edu.cn/sqing33/immich` | [immich.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/immich.yaml) |
| 10 | quay.io/jupyter/pyspark-notebook | 基于网页的用于交互计算的编辑器 | `docker pull ghcr.nju.edu.cn/sqing33/jupyter-notebook` | [jupyter-notebook.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/jupyter-notebook.yaml) |
### 使用方法

1. 使用 GitHub 将项目克隆到自己的仓库

   GitHub 导入页面：https://github.com/new/import

   ```ini
   # 在“The URL for your source repository”字段中输入
   https://codeberg.org/fossandroid/dockerhub2ghcr.git
   ```

2. 同步镜像

   - 进入 GitHub 仓库，点击`Actions`标签
   - 点击`DockerHub 镜像复制到 ghcr.io`
   - 点击右上角的`Run workflow`按钮输入参数

3. 在中国加速拉取镜像

   只需在拉取镜像时将`ghcr.io`替换为`ghcr.nju.edu.cn`（南京大学加速站）

### 修改

更新`main.yml`与`README.md`文件以方便查看已同步的镜像目录以及部分容器部署命令

```yaml
- name: 更新 README.md 文件
        run: |
          # 克隆仓库
          git clone https://github.com/${{ github.repository }} repo
          cd repo

          # 将镜像名称添加到 README.md
          echo "更新镜像：${{ env.REGISTRY }}/${{ env.ACTOR_LOWER }}/${{ env.IMAGE_NAME }}:${{ inputs.tag }}" >> README.md

          # 配置 Git 用户信息
          git config --global user.name "GitHub Actions"
          git config --global user.email "actions@github.com"

          # 使用 GITHUB_TOKEN 推送更改
          git remote set-url origin https://x-access-token:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}.git
          git add README.md
          git commit -m "更新README.md，添加新的镜像名称"
          git push origin main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
