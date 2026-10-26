# runtime-tools · 运行组件

PingAI 桌面端的**运行组件**字节（ADR-0143）：ffmpeg / ffprobe / hyperframes。

- **这里只放不可变的 Release 附件。** 真源是网关库里的 `runtime_components` 表 ——
  客户端按 `GET /api/runtime-components` 拿「去哪下、多大、sha256 多少、上没上架」。
- 附件按 `<id>-<version>-<platform>.zip` 命名；**同一个版本不许换字节**，要改就发新版本号。
- 客户端下载后**强制校验 sha256**，再按 `exe`（以及 `prefixArgs`）解析出可执行入口。

## 当前批次

Tag：**`tools-2026-10-26`**（win64）

| 组件 | 版本 | 附件 | 说明 |
|---|---|---|---|
| ffmpeg / ffprobe | 2026.10.25 | `ffmpeg-2026.10.25-win64.zip` | BtbN FFmpeg-Builds（GPL），两条清单行共用一个附件 |
| hyperframes | 0.8.202 | `hyperframes-0.8.202-win64.zip` | Apache-2.0；含生产依赖与自带 Node v22.15.0 |

清单：见同目录 [`manifest.json`](manifest.json)（可直接粘进 admin「运行组件 → 从清单导入」）。

`hyperframes` 的入口是 `node.exe hyperframes/bin/hyperframes.mjs` —— 客户端必须带
`prefixArgs`，否则执行的是 `node.exe` 本身（那会开一个 REPL，看起来像卡死）。

## 这一批是怎么做的

不是纯自动流水线，两处**手工重组**（下次换版本照这个来，或把这两步接进脚本）：

1. **ffmpeg**：上游 zip 里只取 `bin/ffmpeg.exe`、`bin/ffprobe.exe`、`LICENSE.txt`
   （去掉 `ffplay` / `doc/` / `presets/`，191 MB → 126 MB）。
2. **hyperframes**：`npm install hyperframes@<ver> --omit=dev` 拿到生产依赖，
   再把 `node_modules/hyperframes` 提到 `hyperframes/`、`node.exe` 放根 ——
   因为 **npm 包里不含依赖**，直接打包会在用户机上 `ERR_MODULE_NOT_FOUND`。

打包后都做过冒烟：`node.exe hyperframes/bin/hyperframes.mjs --version` → `0.8.202`。

哈希由发布方下载后现算、并写进清单；GitHub 侧对上传的附件独立算了一次，两者一致。

## 许可

- **ffmpeg / ffprobe**：GPL，构建来自 [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds)，包内附 `LICENSE.txt`。
- **hyperframes**：Apache-2.0，[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)。
- **Node.js**：MIT，包内 `node.exe` 取自 Node v22.15.0 官方构建。

上游二进制**未修改**（仅去掉无关文件、补入依赖与 Node 后重新打包）。
