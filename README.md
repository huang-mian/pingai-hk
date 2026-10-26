# pingai-hk

PingAI 的**公开可分发产物**。一个仓，按项目分目录；每个项目的字节放**它自己的 Release tag**。

| 项目 | 目录 | Release tag | 说明 |
|---|---|---|---|
| 运行组件 | [`runtime-tools/`](runtime-tools/) | `tools-*` | ffmpeg / ffprobe / hyperframes（ADR-0143） |
| 宿主软件 | [`desktop-releases/`](desktop-releases/) | — | 预留；旧仓暂不迁（见该目录 README） |

> ⚠️ **GitHub 的仓库是平的** —— 仓下面不能再建仓。所以这里的「子仓」= **目录 + 各自的 tag**：
> 每个项目有独立的版本号与独立的附件，但共用这一份 issue、权限与 Release 列表。
> 若将来需要每个项目独立权限/星标/issue，那时的正解是建一个组织（Free 计划即可，公开仓免费）。

## 为什么字节放 Release 不放 git

- git 树单文件硬限 100 MB，且 blob **永久留存** —— 每换一版都把历史撑大一次。
- Release 附件单文件上限 2 GB，且**发完不可变**（正好符合「同一版本不许换字节」）。

## 许可

各项目目录的 README 里写各自的许可与上游出处。
