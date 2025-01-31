# 将 Docker 镜像同步到 ghcr.io

### 已同步 Docker 镜像

|   | 源镜像 | 用途 | pull 命令 | docker-compose |
| ---- | -------- | ---- | --------- | -------------- |
| 1   | nginx                         | web 服务器  | `docker pull ghcr.nju.edu.cn/sqing33/nginx`             |                |
| 2   | linuxserver/speedtest-tracker | 网速测试    | `docker pull ghcr.nju.edu.cn/sqing33/speedtest-tracker` |                |
| 3   | dpanel/dpanel                 | docker 管理 | `docker pull ghcr.nju.edu.cn/sqing33/dpanel`            |                |
| 4   | hello-world                   |             | `docker pull ghcr.nju.edu.cn/sqing33/hello-world`       |                |
| 5 | 6053537/portainer-ce | docker 管理 | `docker pull ghcr.nju.edu.cn/sqing33/portainer` |  |
| 6 | lscr.io/linuxserver/qbittorrent | bt 下载 | `docker pull ghcr.nju.edu.cn/sqing33/qbittorrent` |  |
| 7 | mzz2017/v2raya | 魔法 | `docker pull ghcr.nju.edu.cn/sqing33/v2raya` | [v2raya.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/v2raya.yaml) |
| 8 | dreamacro/clash | 魔法 | `docker pull ghcr.nju.edu.cn/sqing33/clash` | [clash.yaml](https://github.com/sqing33/docker-image-sync/blob/main/docker-compose/clash.yaml) |
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
