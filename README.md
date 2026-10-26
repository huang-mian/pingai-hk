# runtime-tools

PingAI 桌面端的**运行组件**字节（ADR-0143）：ffmpeg / ffprobe / hyperframes。

- **这里只放不可变的 Release 附件。** 真源是网关库里的 `runtime_components` 表 ——
  客户端按 `GET /api/runtime-components` 拿「去哪下、多大、sha256 多少、上没上架」。
- 附件按 `<id>-<version>-<platform>.zip` 命名；**同一个版本不许换字节**，要改就发新版本号。
- 客户端下载后**强制校验 sha256**，再按 `exe`（以及 `prefixArgs`）解析出可执行入口。

## 当前批次

`tools-2026-10-26`（win64）

| 组件 | 版本 | 附件 | 说明 |
|---|---|---|---|
| ffmpeg / ffprobe | 2026.10.25 | `ffmpeg-2026.10.25-win64.zip` | BtbN FFmpeg-Builds（GPL），两条清单行共用一个附件 |
| hyperframes | 0.8.202 | `hyperframes-0.8.202-win64.zip` | Apache-2.0；含生产依赖与自带 Node v22.15.0 |

`hyperframes` 的入口是 `node.exe hyperframes/bin/hyperframes.mjs` —— 客户端必须带
`prefixArgs`，否则执行的是 `node.exe` 本身（那会开一个 REPL，看起来像卡死）。

## 许可

- **ffmpeg / ffprobe**：GPL，构建来自 [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds)，包内附 `LICENSE.txt`。
- **hyperframes**：Apache-2.0，[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)。
- **Node.js**：MIT，包内 `node.exe` 取自 Node v22.15.0 官方构建。

上游二进制**未修改**（仅去掉无关文件、补入依赖与 Node 后重新打包）；
sha256 由发布方下载后现算，写进清单，不采信任何手填值。
