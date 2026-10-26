# desktop-releases（预留）

宿主软件（Claude Desktop / ChatGPT Desktop / Claude Code / Codex CLI）的安装包分发，将来落在这里。

**现在什么都没放，而且旧仓不会迁过来** —— 理由是硬的（ADR-0028 补记四 / ADR-0143 补记一）：

- 已发布客户端把旧仓名写死在常量里（`DIST_REPO = 'huang-mian/desktop-releases'`）；
- jsDelivr 与 `raw.githubusercontent.com` **都不跟随仓库重定向** —— 迁走 = 断掉老客户端的更新链。

⇒ 2.0.0 退役之前，那一份留在 `huang-mian/desktop-releases`。这里预留给**新的**客户端线。
